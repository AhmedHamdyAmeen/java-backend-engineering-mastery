# SRC-005 · Performance modeling — Lecture scripts

**Video:** 73 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-005-L01 · Latency budgets (12 min)
**Goal:** split an end-to-end target across the calls on the path.

**Key points**
- Start from the user-facing target, e.g. checkout p99 under 800 ms.
- Allocate to each hop on the critical path; sequential calls add, parallel calls take the maximum.
- Budget percentiles (p99), not averages; leave margin for network and serialization.
- A call without a budget gets a timeout derived from it.

**Show:** a table: gateway 20 ms, order service 120 ms, inventory 150 ms, payment 350 ms, database 100 ms, margin 60 ms.

**Check:** Why budget p99 rather than the average? *(Users and SLOs feel the tail; averages hide it.)*

---

## SRC-005-L02 · Little's Law (12 min)
**Goal:** relate concurrency, throughput, and latency.

**Key points**
- L = lambda x W: items in the system equals arrival rate times time in the system.
- Applies to threads, connections, consumers, queue contents.
- Example: 500 requests/s at 0.2 s latency needs about 100 concurrent in flight.
- Use it to size pools and to predict what happens when latency rises.

**Show:** pool sizing: 300 DB calls/s at 15 ms each gives 4.5 busy connections on average; a pool of 10 is fine until latency grows ten times.

**Check:** 200 requests/s at 0.5 s each: how many in flight? *(About 100.)*

---

## SRC-005-L03 · Queueing and utilization (14 min)
**Goal:** explain why latency explodes near saturation.

**Key points**
- Utilization is busy time over total time; waiting time grows sharply as it nears 100%.
- Intuition: with random arrivals, bursts queue up and the queue drains slowly when there is little spare capacity.
- Rule of thumb: keep utilization well below saturation (often 60-70% for latency-sensitive paths; verify by test).
- Bounded queues and load shedding protect latency.

**Show:** a curve description: wait time flat at 50% utilization, doubling by 80%, exploding past 90%.

**Check:** Why not run a service at 95% utilization? *(Queueing delay grows steeply and tail latency becomes unpredictable.)*

---

## SRC-005-L04 · Tail latency and fan-out (10 min)
**Goal:** see how tails amplify across calls.

**Key points**
- If a request calls N services in parallel, it waits for the slowest.
- With 10 calls each slow 1% of the time, about 10% of requests see a slow call.
- Mitigations: fewer calls, timeouts, hedged requests, caching, removing calls from the critical path.
- Measure percentiles per hop.

**Show:** the calculation 1 - 0.99^10, about 9.6%, and a trace where one slow hop dominates.

**Check:** What happens to tail latency as fan-out grows? *(The chance of hitting a slow call rises, so overall tail gets worse.)*

---

## SRC-005-L05 · Finding the bottleneck on paper (10 min)
**Goal:** locate the limiting resource before testing.

**Key points**
- For each resource compute demand (requests per second x time per request) and capacity.
- The resource with the highest utilization is the bottleneck candidate.
- Candidates: CPU, DB connections, thread pool, lock, network, downstream rate limit.
- Make a prediction you can falsify with a test.

**Show:** a table: resource, demand, capacity, utilization; the connection pool at 92% is highlighted.

**Check:** How do you find the bottleneck on paper? *(Compute utilization per resource; the highest is the candidate.)*

---

## SRC-005-L06 · Demo: predicting pool sizes with Little's Law, then measuring (15 min)
**Goal:** predict, test, and explain the gap; prepares SRC-005-LAB1.

**Steps**
1. Write the checkout budget and the expected load at 10×.
2. Compute required HTTP threads, DB connections, and Kafka consumers with Little's Law.
3. Run a load test (verify tool and setup before recording) and compare predicted with measured concurrency.
4. **Planned mistake:** use the average latency from a quiet run. Fix: use p95 latency under load; the model then matches within 20%.
5. Explain any remaining gap (retries, lock waits, GC).
6. Record the model and the measured error in the capacity plan.
