# SRA-008 · Architecture economics — Exercises and lab

## Lab
### SRA-008-LAB1 · Payouts decision
**Outcomes:** 1–4 · **Time:** ~2 h
1. Define requirements for marketplace seller payouts and three options (build, buy, hybrid).
2. Build a five-year TCO model with volume growth, staffing, infrastructure, compliance, and integration costs.
3. Add opportunity cost and an exit plan for each option; value the flexibility of at least one option.
4. Write a one-page business case with sensitivity analysis and recommendation.
5. Defend it to a role-played finance partner who tries to reproduce the numbers.
**Acceptance:** role-played finance partner can reproduce the numbers.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-008-EX01 | 1 | Compare build, buy, and open source for a search engine over five years using a given set of costs. |
| SRA-008-EX02 | 1 | Identify the hidden costs missing from a TCO that compares a vendor licence with "zero". |
| SRA-008-EX03 | 2 | Compute the opportunity cost of assigning twelve engineers to build an internal tool for eighteen months. |
| SRA-008-EX04 | 2 | Write an exit plan for a vendor payment platform: triggers, data portability, parallel run, and cost. |
| SRA-008-EX05 | 3 | Value an abstraction layer that costs 150k now and could avoid a 1.2M migration with 30% probability. Decide and state assumptions. |
| SRA-008-EX06 | 4 | Rewrite an engineering-language case into a one-page finance-checkable business case with assumptions, sensitivity, and decision request. |

## Solutions
- **EX01** Sum licence or usage, infrastructure, staffing, operation, and upgrades per year; compare with growth; note exit effort and fit. Pick the lowest risk-adjusted TCO that meets requirements.
- **EX02** Missing: engineering, operations, on-call, compliance, upgrades, delay to market, and the cost of capacity growth. Also missing: exit and training.
- **EX03** Estimate loaded cost of twelve engineers over eighteen months plus the value of the next best project they would not deliver; state the benefit forgone.
- **EX04** Triggers: price rise, service failure, acquisition. Needs data export format, a second provider path, a reconciliation parallel run, and a cost and timeline estimate.
- **EX05** Expected avoided cost 0.3 × 1.2M = 360k against 150k, so the option has positive expected value; state that probability is an assumption and a sensitivity check shows break-even at about 12.5%.
- **EX06** State decision requested, options, cost and benefit by year, assumptions sheet with source and owner, sensitivity on top two inputs, risks, and the cost of delay.

Outcome 4 is also covered by the lab finance defense and the quiz.

**Workplace evidence:** a build/buy decision you analyzed and its outcome.
