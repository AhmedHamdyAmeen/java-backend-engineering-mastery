# SRC-017 · Technical debt — Exercises and lab

## Lab
### SRC-017-LAB1 · Shop debt register
**Outcomes:** 1–4 · **Time:** ~3.5 h
Build a debt register for Shop Platform with classified items, cost estimates, and a one-quarter paydown plan using incremental techniques. Pitch it to role-played product leadership.
**Acceptance:** at least one item approved on its business case.

## Exercises (assessment: pitch and register review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-017-EX01 | 1 | Classify five examples into the deliberate/inadvertent and prudent/reckless quadrants and say which are not debt at all. |
| SRC-017-EX02 | 1 | Estimate the interest on a module touched 12 times a quarter with 1.5 extra days per change and one incident. State ranges. |
| SRC-017-EX03 | 2 | Build a five-item register with costs and rank them by payback and risk. |
| SRC-017-EX04 | 3 | Write an incremental plan to remove a God class `OrderService` over a quarter without a rewrite. |
| SRC-017-EX05 | 4 | Write the one-page business case for adding tests and extracting pricing, with options and measures. |
| SRC-017-EX06 | 2 | Case: debt in a module nobody will change for a year. Decide priority and justify. |

## Solutions
- **EX01** Examples should show that a known shortcut with a repayment plan is prudent; a missing feature or a bug is not debt; skipped tests with no plan is reckless.
- **EX02** 12 × 1.5 = 18 engineer-days per quarter, with a range such as 14 to 22, plus the incident cost.
- **EX03** Rank by payback (fix cost divided by monthly interest) and adjust for risk items such as security that rank first regardless.
- **EX04** Add characterization tests, extract responsibilities one at a time behind interfaces, route new features to the new classes, delete old code as it empties, release each slice.
- **EX05** Problem, evidence, cost of delay, options (do nothing, partial, full), cost, expected outcome and metrics, checkpoint.
- **EX06** Low priority: little interest is paid; revisit if work in that area is planned.
- Outcome 3 is also covered by the lab plan and Q06-Q07.

**Workplace evidence:** a debt item you got prioritized and delivered.
