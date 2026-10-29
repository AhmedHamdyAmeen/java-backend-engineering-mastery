# SRC-016 · Performance engineering — Exercises and lab

## Lab
### SRC-016-LAB1 · Meet the latency target
**Outcomes:** 1–4 · **Time:** ~4.5 h
Bring checkout p99 within the SLO at 10× forecast load. Baseline with a constant-rate load test, profile, remove bottlenecks in order, and stop at the target. Add a performance regression check to CI, then seed a regression.
**Acceptance:** before/after evidence; CI catches a seeded regression.

## Exercises (assessment: performance report review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-016-EX01 | 1 | Review a JMH benchmark with an unused result and constant input; list the traps and rewrite it. |
| SRC-016-EX02 | 1 | Design a load test plan for checkout at 1×, 5×, and 10× forecast: workload mix, arrival model, duration, pass criteria. |
| SRC-016-EX03 | 2 | Given a table of step shares of p99 (45, 25, 15, 10, 5), choose the order of work and the likely maximum gain from the first fix. |
| SRC-016-EX04 | 3 | Design the CI regression check: benchmark set, baseline, tolerance, failure behavior. |
| SRC-016-EX05 | 4 | Rewrite "p99 improved from 800 ms to 400 ms" as an honest report line with context and uncertainty. |
| SRC-016-EX06 | 2 | Case: the team wants to rewrite the JSON library to save 3% of checkout time. Give your recommendation. |

## Solutions
- **EX01** Traps: dead-code elimination and constant folding. Consume via `Blackhole` or return, use `@State` inputs with variety, add forks, warm-up and measurement.
- **EX02** Mix by real traffic proportions, constant arrival rate, steps, long enough for steady state, pass if p99 and error rate meet the SLO at 10×.
- **EX03** Order by share; the first fix at 45% could remove up to 45% at best; re-measure after each since shares change.
- **EX04** Small stable JMH subset plus a smoke load test on dedicated hardware; compare with main baseline; tolerance from measured noise; fail with a report.
- **EX05** For example: "Checkout p99 fell from 800 ms (95% CI 780 to 820) to 400 ms (385 to 415) over five 20-minute runs at 10× forecast, on the staging environment with stubbed payment latency; production may differ in cache hit rates."
- **EX06** Decline: even removing it entirely gains at most 3%; spend effort on the largest remaining bottleneck.
- Outcome 3 is also covered by the lab CI check and Q07-Q08; outcome 4 by Q10.

**Workplace evidence:** a measured performance improvement you delivered.
