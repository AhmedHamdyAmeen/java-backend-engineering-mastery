# SRC-015 · Advanced troubleshooting — Exercises and lab

## Lab
### SRC-015-LAB1 · Mystery outages
**Outcomes:** 1–4 · **Time:** ~4.5 h
Three timed scenarios on Shop Platform with layered causes (for example thread starvation hiding a connection leak, a retry storm, CPU throttling). For each, keep an investigation log, find the root cause, and propose the fix.
**Acceptance:** root cause, evidence chain, and fix for each within the time box.

## Exercises (assessment: live troubleshooting simulation, a graduation gate component)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-015-EX01 | 1 | Given two thread dumps ten seconds apart showing 190 threads in a payment client read, state the diagnosis, evidence, and fixes. |
| SRC-015-EX02 | 1 | Compute pool sizing for 30 pods against a database limit of 400 connections, and explain the failure at 10× scale. |
| SRC-015-EX03 | 1 | Two transactions deadlock updating stock rows. Show how to confirm and fix. |
| SRC-015-EX04 | 2 | Describe the retry multiplication across gateway, orders, and payment client with 3 attempts each and propose a retry budget. |
| SRC-015-EX05 | 3 | Write an investigation log for the scenario "p99 spikes, CPU low, DB healthy" with at least three hypotheses and tests. |
| SRC-015-EX06 | 4 | Case: latency rose after moving to a smaller memory limit. List layers to check and the signal for each. |

## Solutions
- **EX01** Thread starvation due to a slow dependency without a timeout. Evidence: same stack in both dumps, pool active at max, low CPU. Fixes: timeouts, bulkhead, load shedding, circuit breaker.
- **EX02** Pool size multiplied by pod count must stay under the limit with headroom, for example 10 per pod gives 300. Scaling pods 10× multiplies connections beyond the limit, so use a pooler or cap pool sizes and shrink transactions.
- **EX03** Confirm from the database deadlock log or lock views; fix by locking rows in sorted ID order and keeping transactions short.
- **EX04** 3 × 3 × 3 = 27 calls to the payment service per user request. Retry at one layer only, limit retries to a fraction of traffic (budget), backoff with jitter, shrink timeouts down the chain.
- **EX05** Hypotheses: GC pauses (GC logs), CPU throttling (cgroup metrics), network or DNS delay (hop latencies). Run the cheapest test first; log result and next step.
- **EX06** JVM (GC frequency, heap pressure), container (OOM kills, memory limit), OS (swap, page cache), database (connection churn), network. Compare before and after the change.
- Outcome 2 is also covered by the lab and Q05-Q06; outcome 3 by Q01 and the investigation logs.

**Workplace evidence:** a hard production investigation you led, written up.
