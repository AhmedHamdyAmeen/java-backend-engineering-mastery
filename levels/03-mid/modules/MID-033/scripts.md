# MID-033 · Resilience — Lecture scripts

**Video:** 82 min · **Analogy used throughout:** a restaurant kitchen: a slow dishwasher backs up every cook unless you set time limits, add separate stations, and tell customers "no dessert today" honestly.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-033-L01 · How failures cascade (10 min)
**Goal:** see how one slow dependency takes down callers.

**Key points**
- A slow service is worse than a dead one: callers wait, threads pile up, and pools fill.
- Little's law: concurrent requests = arrival rate × latency; latency rising 10× means 10× threads held.
- Once the caller's pool is full it fails for every endpoint, even those not using the slow dependency.
- Retries multiply load on the struggling service (retry storm).
- Defenses: timeouts, bounded retries, circuit breakers, bulkheads, fallbacks.

**Show:** diagram: `checkout` → `payments` (slow). Thread pool of 200 fills with waiting calls; `GET /products` also stalls.

**Check:** Why can a slow dependency break unrelated endpoints? *(Shared threads or connections are all held by waiting calls.)*

---

## MID-033-L02 · Timeouts and latency budgets (10 min)
**Goal:** set a timeout on every remote call from a budget.

**Key points**
- No timeout means waiting forever (or a very long default). Set connect and read timeouts explicitly.
- Start from the user-facing target (for example 1 s) and divide the budget among calls.
- Downstream timeouts must be shorter than upstream ones, or the caller gives up while work continues.
- Prefer a deadline passed along the call chain over independent timeouts.
- Measure p99 latency of the dependency to choose values (verify client settings for your HTTP client before recording).

**Show**
```java
var factory = new JdkClientHttpRequestFactory(); // or your chosen client
factory.setReadTimeout(Duration.ofMillis(300));
RestClient payments = RestClient.builder().requestFactory(factory).build();
```

**Check:** Checkout must answer in 1 s and calls inventory then payments. How do you split? *(For example 300 ms and 500 ms, leaving margin for own work.)*

---

## MID-033-L03 · Retries, backoff, and jitter (10 min)
**Goal:** retry safely and without synchronizing clients.

**Key points**
- Retry only **transient** failures (timeouts, 503, connection reset) on **idempotent** operations.
- Never retry non-idempotent POSTs unless protected by an idempotency key.
- **Exponential backoff:** wait 100 ms, 200 ms, 400 ms, with a cap and a maximum attempt count.
- **Jitter:** add randomness so clients do not all retry at the same moment.
- Retries only inside the latency budget; a retry budget (for example at most 10% extra calls) limits storms.

**Show**
```java
RetryConfig cfg = RetryConfig.custom()
    .maxAttempts(3)
    .intervalFunction(IntervalFunction.ofExponentialRandomBackoff(100, 2.0, 0.5))
    .retryExceptions(IOException.class, TimeoutException.class)
    .build();
```

**Check:** Why add jitter? *(To stop all clients retrying at the same instant and re-overloading the service.)*

---

## MID-033-L04 · Circuit breakers (10 min)
**Goal:** stop calling a failing dependency and probe for recovery.

**Key points**
- States: **closed** (calls pass), **open** (calls fail fast), **half-open** (a few trial calls).
- Open when failure rate or slow-call rate crosses a threshold in a sliding window.
- Failing fast frees threads and gives the dependency room to recover.
- Count only relevant failures (5xx, timeouts), not 4xx business errors.
- Test it: a breaker that was never opened in a test may be misconfigured.

**Show**
```java
CircuitBreakerConfig cfg = CircuitBreakerConfig.custom()
    .slidingWindowSize(20).failureRateThreshold(50)
    .slowCallDurationThreshold(Duration.ofMillis(500)).slowCallRateThreshold(50)
    .waitDurationInOpenState(Duration.ofSeconds(10))
    .permittedNumberOfCallsInHalfOpenState(3).build();
```

**Check:** What does an open breaker do with a new call? *(Rejects it immediately without contacting the dependency.)*

---

## MID-033-L05 · Bulkheads (8 min)
**Goal:** isolate resource pools per dependency.

**Key points**
- Named after ship compartments: a leak floods one section, not the whole ship.
- Give each dependency its own limit on concurrent calls (semaphore) or its own thread pool.
- A slow `reviews` call can then use at most its share, leaving capacity for `payments`.
- Excess calls are rejected quickly rather than queued.
- Size limits from expected concurrency, not guesses; revisit with load tests.

**Show**
```java
BulkheadConfig cfg = BulkheadConfig.custom()
    .maxConcurrentCalls(20).maxWaitDuration(Duration.ZERO).build();
```

**Check:** What does a bulkhead protect? *(Other dependencies and endpoints from one slow dependency using all shared capacity.)*

---

## MID-033-L06 · Fallbacks and degradation (8 min)
**Goal:** keep serving something useful, honestly.

**Key points**
- A **fallback** runs when the call fails: cached value, default, or partial response.
- Degrade optional features first (reviews, recommendations); fail clearly for essential ones (payment).
- Be honest: never show a made-up "payment succeeded". Show "reviews unavailable".
- Mark degraded responses so clients and monitoring know.
- Stale cache is a valid fallback only if stale is acceptable for that data.

**Show**
```java
@CircuitBreaker(name = "reviews", fallbackMethod = "noReviews")
List<Review> reviews(long productId) { ... }
List<Review> noReviews(long productId, Throwable t) { return List.of(); } // UI: "Reviews unavailable"
```

**Check:** Should checkout fall back to "payment OK" if `payments` is down? *(No; fail honestly or leave the order pending.)*

---

## MID-033-L07 · Demo: a cascading failure, then the fix (14 min)
**Goal:** break checkout with a slow `payments`, then contain it. Prepares MID-033-LAB1.

**Steps**
1. Put Toxiproxy between `orders` and `payments`; run a load test on checkout and on `GET /products`.
2. Add 5 s latency to the proxy: checkout hangs and product listing also slows as the pool fills.
3. Add a 500 ms read timeout on the payments client; checkout fails fast but still hammers `payments`.
4. Add a circuit breaker and a bulkhead for `payments`; repeat: failures are fast, product listing stays healthy.
5. **Planned mistake:** configure the breaker to count `400` responses as failures; it opens on validation errors. Fix: record only timeouts and 5xx.
6. Remove the latency and watch the breaker go half-open, then closed.

---

## MID-033-L08 · Demo: retry storms and jitter (12 min)
**Goal:** show how naive retries make an outage worse. Prepares MID-033-LAB1.

**Steps**
1. Run 200 virtual users against `inventory` through Toxiproxy; make the service fail for 10 seconds.
2. Add fixed-interval retries (3 attempts, 100 ms) and watch request volume triple and recovery stall.
3. **Planned mistake:** also retry `POST /payments` automatically; show a customer charged twice in the test data. Fix: retry only idempotent calls or use an idempotency key.
4. Switch to exponential backoff with jitter and a limit; compare the request-rate graphs.
5. Add a retry budget or breaker so retries stop when the failure rate is high.
