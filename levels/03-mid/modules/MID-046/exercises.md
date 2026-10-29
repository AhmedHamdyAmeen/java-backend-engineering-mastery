# MID-046 · Performance testing — Exercises and lab

## Lab
### MID-046-LAB1 · Shop under load
**Outcomes:** 1–4 · **Time:** ~3 h
Run load, spike, and 2-hour soak tests of checkout from a separate machine with a realistic traffic mix and data set. Write a report naming the first bottleneck.
**Acceptance:** report with percentiles, graphs, and evidence.

## Exercises (assessment: report review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-046-EX01 | 1 | For four scenarios (flash sale, nightly leak, capacity planning, recovery after overload), pick the test type and justify it. |
| MID-046-EX02 | 2 | Write a k6 script for browse, add to cart, and checkout with think time and thresholds. |
| MID-046-EX03 | 2 | Make the script use varied users and SKUs from a data file. |
| MID-046-EX04 | 3 | Rewrite a closed-loop scenario as an arrival-rate scenario and explain the change in the results. |
| MID-046-EX05 | 3 | Given a latency histogram, report p50, p95, p99 and explain why the average misleads. |
| MID-046-EX06 | 4 | Given a graph of p95 and pool-wait metrics, state the bottleneck hypothesis and the next measurement. |
| MID-046-EX07 | 1–4 | Review a sample report: list what is missing (percentiles, load generator location, data realism, evidence). |

## Solutions
- **EX01** Flash sale: spike; nightly leak: soak; capacity planning: stress or load to saturation; recovery: stress with a drop back to normal.
- **EX02** `options.thresholds` for p95 and failure rate; a default function with three requests and `sleep` calls.
- **EX03** `SharedArray` loaded from JSON/CSV and a random pick per iteration.
- **EX04** `executor: 'constant-arrival-rate'` with `preAllocatedVUs`; the slow system now shows rising latency and dropped iterations instead of hidden lower throughput.
- **EX05** State the three percentiles; the average sits between them and hides the tail.
- **EX06** Hypothesis: connection pool saturation; measure pool wait, active connections, and slow queries; then retest after adjusting one setting.
- **EX07** Missing items are fixed one by one; reject reports that quote only averages or ran on the same machine as the system under test.

**Outcome 1** is also checked by the lab (three test types) and quiz Q01-Q02.
