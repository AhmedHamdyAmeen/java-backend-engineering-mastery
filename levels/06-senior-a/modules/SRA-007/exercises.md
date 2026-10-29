# SRA-007 · Large-scale performance — Exercises and lab

## Lab
### SRA-007-LAB1 · Three-year forecast
**Outcomes:** 1–4 · **Time:** ~2 h
1. Collect business drivers for Commerce 2030: orders, sellers, listings, countries, campaigns.
2. Measure or assume load ratios per driver and build a workload model including marketplace shapes.
3. Produce a three-year capacity forecast with low, base, and high cases.
4. Compute cost per order at target latency for each year and propose optimizations.
5. Set performance budgets for three teams on the checkout path.
**Acceptance:** assumptions explicit; sensitivity to growth rate shown.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-007-EX01 | 1 | Orders double yearly. Given requests per order for six services, forecast peak requests per second for two years and identify the first bottleneck. |
| SRA-007-EX02 | 1 | Add sensitivity: show the effect of 1.5x and 3x annual growth on the forecast and on cost. |
| SRA-007-EX03 | 2 | Build a workload model for seller bulk uploads and inventory sync and state how you would validate it. |
| SRA-007-EX04 | 2 | Explain why a load test with only buyer traffic would miss risks at marketplace launch. |
| SRA-007-EX05 | 3 | Choose among three optimizations (cache, batching, right-sizing) by cost per order at target latency; justify the pick. |
| SRA-007-EX06 | 4 | Split an 800 ms checkout budget among five teams, define tracking, and describe what happens when a team exceeds its share. |

## Solutions
- **EX01** Multiply orders by ratio per service, apply a peak-to-average factor and headroom; the service with the highest load-to-capacity ratio goes first, often the one that scales worst (state your numbers and assumptions).
- **EX02** Run the same model with each rate; show how the bottleneck date and capacity spend move; highlight the decision that changes first.
- **EX03** Rates by seller count and listing size, burst patterns (batch windows), payload sizes; validate with synthetic load tests, analog data from similar platforms, and early production seller data.
- **EX04** Buyer traffic is read-heavy and spread; sellers add write bursts and indexing load, shifting bottlenecks to ingestion, search indexing, and storage.
- **EX05** Compute savings and latency effect per option; pick the one with lowest cost per order meeting the target and with acceptable complexity; verify by measurement.
- **EX06** Example: gateway 50 ms, pricing 100 ms, inventory 150 ms, payment 350 ms, remaining 150 ms; dashboards per team; exceeding triggers a plan or a budget renegotiation, not blame.

Outcome 4 is also covered by the lab budgets and the quiz.

**Workplace evidence:** a capacity forecast used in budgeting.
