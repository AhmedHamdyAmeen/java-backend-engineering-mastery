# SRC-005 · Performance modeling — Exercises and lab

## Lab
### SRC-005-LAB1 · Checkout latency budget
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Allocate a p99 budget for checkout across the services and calls on the critical path.
2. Model required HTTP threads, DB connections, and Kafka consumers with Little's Law at the 10× load.
3. Compute utilization per resource on paper and name the predicted bottleneck.
4. Verify with a load test; compare model and measurement.
**Acceptance:** model within 20% of measurement or discrepancy explained.

## Exercises (modeling problem set; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-005-EX01 | 1 | Allocate a 900 ms p99 budget over a path with gateway, order, two parallel calls (inventory, pricing), then payment, then DB write. |
| SRC-005-EX02 | 2 | 800 requests/s at 150 ms: how many in flight? A pool has 60 connections: what is the maximum throughput at 30 ms per query? |
| SRC-005-EX03 | 3 | Explain why a service at 90% utilization shows much higher p99 than at 60%, and propose two protections. |
| SRC-005-EX04 | 3 | Latency of a downstream call rises from 50 ms to 500 ms at constant arrival rate. What happens to threads in flight? |
| SRC-005-EX05 | 4 | From a table of resource demand and capacity, identify the bottleneck and design an experiment to confirm it. |
| SRC-005-EX06 | 1 | A page calls 20 services in parallel, each with p99 100 ms and p50 10 ms. Estimate how often the page sees a slow call and suggest a fix. |

## Solutions
- **EX01** Parallel calls count as the maximum: gateway 20, order 100, parallel max(150, 80) = 150, payment 350, DB 100, margin 70 ms = 790 ms plus reserve; state timeouts per call.
- **EX02** 800 x 0.15 = 120 in flight. Pool throughput = 60 / 0.03 = 2,000 queries/s.
- **EX03** Queueing delay grows steeply near saturation; protections: bounded queues with load shedding, autoscaling or capacity headroom, timeouts.
- **EX04** In flight = rate x latency, so concurrency grows ten times; pools exhaust and requests queue unless timeouts and limits cap it.
- **EX05** Highest utilization resource (for example DB pool at 92%) is the candidate; raise load stepwise, watch pool wait time and CPU, then change pool size and see whether the knee moves.
- **EX06** 1 - 0.99^20 is about 18% of pages see a slow call; fix with fewer calls, caching, timeouts with degraded fallback, hedged requests.

**Workplace evidence:** a performance target you set or met using a model rather than trial and error.
