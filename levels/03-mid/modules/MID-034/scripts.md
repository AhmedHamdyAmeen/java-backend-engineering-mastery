# MID-034 · Rate limiting — Lecture scripts

**Video:** 52 min · **Analogy used throughout:** a bakery handing out tickets: tokens drip into a jar at a steady pace, each customer takes one, and when the jar is empty they wait a told number of seconds.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-034-L01 · Why limit (6 min)
**Goal:** name the reasons to limit traffic.

**Key points**
- Protect capacity from abusive or buggy clients (a retry loop, a scraper).
- Fairness: one customer must not starve others.
- Cost control and protection of downstream services and paid APIs.
- Security: slows credential stuffing and brute force.
- Limits are keyed by something: API key, user, IP, tenant.

**Show**
| Key | Good for | Weakness |
| --- | --- | --- |
| IP | anonymous traffic | shared NAT, proxies |
| User or API key | fairness per customer | needs authentication |

**Check:** Why not limit only by IP? *(Many users can share one IP and attackers can rotate IPs.)*

---

## MID-034-L02 · Token and leaky buckets (10 min)
**Goal:** explain the main algorithms and their burst behavior.

**Key points**
- **Token bucket:** tokens refill at a rate up to a capacity; each request uses one. Allows bursts up to capacity.
- **Leaky bucket:** requests enter a queue that drains at a fixed rate; smooths output, drops overflow.
- **Fixed window:** count per minute; simple, but allows a double burst at the window edge.
- **Sliding window:** counts over the last N seconds; fairer, costs more memory.
- Choose token bucket for typical APIs: simple and burst-friendly.

**Show**
```java
// token bucket, refill 10/s, capacity 20
double tokens = Math.min(capacity, tokens + elapsedSeconds * 10);
if (tokens >= 1) { tokens -= 1; allow(); } else reject();
```

**Check:** Which algorithm allows a short burst yet limits the average rate? *(Token bucket.)*

---

## MID-034-L03 · Distributed rate limiting (10 min)
**Goal:** make limits correct across several instances.

**Key points**
- An in-memory limiter behind a load balancer gives each instance its own counter: the real limit is multiplied by the instance count.
- Use a shared store (commonly Redis with an atomic script) or enforce at a single edge such as the gateway.
- Atomicity matters: read-modify-write races let extra requests through.
- Accept approximation: local buckets that sync periodically trade accuracy for speed.
- Decide failure behavior when the store is down: fail open (allow) or closed (reject), per endpoint risk.

**Show:** a diagram: three gateway instances sharing one Redis counter per customer; request flow with allow or `429`.

**Check:** Why is a per-instance in-memory limit wrong for a limit of 100/min with 3 instances? *(Each instance allows 100, so up to 300 in total.)*

---

## MID-034-L04 · Quotas and load shedding (8 min)
**Goal:** distinguish three related controls.

**Key points**
- **Rate limit:** short-term speed (requests per second); protects capacity.
- **Quota:** long-term allowance (requests per month or plan); about business terms.
- **Load shedding:** the server deliberately rejects low-priority work when overloaded, regardless of who is calling.
- Shed by priority: keep checkout, drop recommendations first.
- Respond `429 Too Many Requests` for limits and quotas; `503 Service Unavailable` for shedding.

**Show**
| Control | Trigger | Status |
| --- | --- | --- |
| Rate limit | client exceeds rate | 429 |
| Quota | plan allowance used | 429 or 403 (documented) |
| Load shedding | server overloaded | 503 |

**Check:** Which control reacts to server overload, not client behavior? *(Load shedding.)*

---

## MID-034-L05 · Being a good client (6 min)
**Goal:** behave well against someone else's limits.

**Key points**
- Read `429` and honor `Retry-After` (seconds or a date); do not retry sooner.
- Use backoff with jitter if there is no header; cap total retries.
- Respect documented limits proactively: queue and pace outbound calls.
- Batch requests and cache responses to use fewer calls.
- Log and alert on `429`s you receive; they are a design signal.

**Show**
```
HTTP/1.1 429 Too Many Requests
Retry-After: 12
```
Client waits at least 12 seconds, then retries.

**Check:** What should a client do first on a `429` with `Retry-After: 12`? *(Wait at least 12 seconds before retrying.)*

---

## MID-034-L06 · Demo: per-customer limits at the edge (12 min)
**Goal:** limit by customer and prove fairness. Prepares MID-034-LAB1.

**Steps**
1. Add a Redis-backed request rate limiter filter at the gateway (Spring Cloud Gateway offers one; verify version and key resolver before recording).
2. Write a key resolver: authenticated customer id, falling back to IP.
3. Run a load test with an abusive client at 200 requests per second and a normal one at 5; show `429`s only for the abusive one.
4. **Planned mistake:** run two gateway instances with an in-memory limiter; the abuser gets double the allowance. Fix: shared Redis limiter.
5. Add `Retry-After` and a clear JSON error body, and show a client script honoring it.
