# ARC-031 · Resilience architecture — Exercises and lab

## Lab
### ARC-031-LAB1 · Larkspur resilience
**Outcomes:** 1–4 · **Time:** ~3 h
1. List Larkspur's critical business processes and map their dependencies, including third-party and on-premises ones.
2. Build the failure-scenario catalog with impact, detection, and response.
3. Design degradation for offline store sales, payment-provider failover, and ERP outage queueing.
4. Write continuity plans per critical process.
5. Define resilience tests that prove each degraded mode.
**Acceptance:** every critical business process has a documented degraded mode.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-031-EX01 | 1 | Larkspur's web checkout depends on six services (basket, pricing, stock, payment provider, ERP, tax). Enumerate ten failure scenarios across them, including slow and wrong-answer cases. |
| ARC-031-EX02 | 1 | The ERP is down every Sunday 02:00-04:00 for maintenance and sometimes overruns. Add this to the scenario catalog with impact and response. |
| ARC-031-EX03 | 2 | The tax service times out for 30 seconds under load and the checkout threads pile up. Design the isolation. |
| ARC-031-EX04 | 2 | Define the degraded modes for ERP unavailable, recommendations unavailable, and stock service unavailable, and what the customer sees. |
| ARC-031-EX05 | 3 | Write a one-page continuity plan for stores when the central platform is unreachable for four hours. |
| ARC-031-EX06 | 4 | Design three resilience tests for the payment-provider failover design: what you break, what you measure, pass criteria. |

## Solutions
- **EX01** Examples: payment provider down; payment provider slow; tax service wrong rates; stock service stale; ERP unreachable; basket cache loss; bad deployment of pricing; database failover; duplicate callback; region loss. Each with impact and detection.
- **EX02** Planned maintenance window; orders queued durably; stock shown from platform's last-known view; postings replayed after; alert if the window overruns; capacity plan for the catch-up burst.
- **EX03** Timeout of a couple of seconds; circuit breaker; bulkhead so tax calls cannot take all threads; fallback to cached rates with flag for review; alert on open breaker.
- **EX04** ERP down: accept orders, queue postings, show "last known" stock. Recommendations down: hide the block. Stock down: show availability from cache with "confirm at checkout" or limit to in-stock-by-default items; message honest and short.
- **EX05** Trigger, authority to declare, offline selling steps and limits, manual receipts if needed, cash-only fallback, communication to stores, reconnection and reconciliation, owner and after-action review.
- **EX06** Block the primary provider endpoint: failover within target time, success rate recovers; inject elevated latency: breaker opens; restore primary: traffic returns without duplicate charges. Measure error rate, time to switch, duplicate payments.

**Workplace evidence:** a continuity plan or degraded mode you designed that was used or tested.
