# ARC-021 · Cost architecture — Exercises and lab

## Lab
### ARC-021-LAB1 · Larkspur cost model
**Outcomes:** 1–4 · **Time:** ~3.5 h (use current provider prices; verify before recording)
1. Write the sizing and pricing assumptions with source and confidence.
2. Build monthly cost by component for a normal month and a peak month, including data transfer, logging, non-prod, and DR.
3. Compute cost per order and its sensitivity to growth (for example 2× and 3× orders).
4. Define budgets, alerts, and cost controls.
5. Present low, expected, and high figures.
**Acceptance:** every figure traceable to an assumption; range given, not a single number.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-021-EX01 | 1 | Size the platform from these drivers: 600,000 orders per month, 10 times peak load at holidays, 2 TB of media. List the resource estimates and assumptions. |
| ARC-021-EX02 | 1 | A model lists compute and database only. Add the missing cost lines. |
| ARC-021-EX03 | 2 | Total monthly cost is 40,000 for 600,000 orders. Compute cost per order and the effect of 3× orders if 70 percent of cost is fixed. |
| ARC-021-EX04 | 2 | Identify two cost steps (cliffs) in a cloud design and how to model them. |
| ARC-021-EX05 | 3 | Define budgets and alerts for prod, non-prod, and sandbox accounts. |
| ARC-021-EX06 | 4 | Rewrite "the platform will cost 38,000 a month" as a proper estimate for a finance partner. |

## Solutions
- **EX01** Convert to orders per second at peak, application capacity, database size and I/O, storage with growth, CDN transfer; state each assumption with its confidence; peak sized with autoscaling.
- **EX02** Data transfer, NAT and load balancers, logging and metrics, backups and snapshots, DR copy, non-prod environments, security services, support plan, third-party SaaS.
- **EX03** Cost per order is 40,000 / 600,000 = about 0.067. At 3×: fixed 28,000 plus variable 12,000 × 3 = 36,000, total 64,000 over 1.8 million orders = about 0.036; cost per order falls, unless a step cost appears.
- **EX04** Database instance size tier and extra cache nodes or zones; model them as thresholds and add the step at the volume where they trigger.
- **EX05** Prod: budget with 50/80/100 percent and forecast alerts and anomaly detection; non-prod: lower budget plus auto-shutdown out of hours; sandbox: hard cap and expiry; each with an owner.
- **EX06** "Expected 38,000 per month, range 30,000 to 52,000 (peak months to 70,000), medium confidence; main drivers: order volume, data transfer, database tier; assumptions listed, price list dated".

**Workplace evidence:** a cost estimate you produced that was later compared with actuals.

---
Outcome coverage: all outcomes covered by exercises and the lab.
