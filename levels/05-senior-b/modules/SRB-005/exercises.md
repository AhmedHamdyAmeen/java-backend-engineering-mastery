# SRB-005 · High-availability design — Exercises and lab

## Lab
### SRB-005-LAB1 · Availability budget
**Outcomes:** 1, 2, 3, 4 · **Time:** ~3.5 h
1. Map checkout dependencies including FulfillCo ones and mark hard or soft.
2. Compute composite availability with measured figures.
3. Redesign (fallbacks, cells, bulkheads) to reach 99.95%.
4. Run a load-shedding experiment and record results.
**Acceptance:** math shown; load-shedding experiment run with before/after numbers.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-005-EX01 | 4 | Compute checkout availability: 99.95%, 99.99%, 99.9%, 99.9% in series. |
| SRB-005-EX02 | 4 | Recompute when the 99.9% stock check gets a cache fallback that serves 90% of failures. |
| SRB-005-EX03 | 1 | Audit a design for hidden SPOFs and list five. |
| SRB-005-EX04 | 2 | Write the shedding priority policy for the flash sale. |
| SRB-005-EX05 | 3 | Propose a cell design for FulfillCo shipping and the routing key. |
| SRB-005-EX06 | 3 | Explain shuffle sharding to a teammate with numbers. |

## Solutions
- **EX01** Product about 99.74%; below 99.95% so redesign needed.
- **EX02** Effective stock failure drops to 0.01%, so about 99.99%; total about 99.83%; show the arithmetic.
- **EX03** Certificate expiry, shared config, single DNS provider, single CI pipeline, one on-call expert.
- **EX04** Protect payment confirmation and checkout of logged-in users; throttle browse; drop crawlers and recommendations first.
- **EX05** Cells by warehouse region with routing by warehouse id; rollouts cell by cell.
- **EX06** 8 workers, 2 per customer: 28 pairs; chance two share both is 1/28.

**Workplace evidence:** an availability improvement you designed with before/after numbers.
