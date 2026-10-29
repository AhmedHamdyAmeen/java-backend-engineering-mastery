# SRB-013 · Technology evaluation — Exercises and lab

## Lab
### SRB-013-LAB1 · Workflow engine choice
**Outcomes:** 1–4 · **Time:** ~3.5 h
1. Write the evaluation charter and weighted criteria for FulfillCo's returns process before naming products.
2. Run a time-boxed PoC of one workflow engine against the hand-built saga baseline, testing failure paths.
3. Build the evaluation matrix with a three-year cost and exit cost, a sensitivity check, and a bias checklist.
4. Write the recommendation with an exit plan.
**Acceptance:** recommendation includes exit plan and cost over three years.

## Exercises (assessment: evaluation report review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-013-EX01 | 1 | Rewrite the request "we should adopt a graph database" as a problem statement with constraints, options, and decision date. |
| SRB-013-EX02 | 1 | Define five criteria, mark must-haves, and assign weights for a message broker choice. |
| SRB-013-EX03 | 2 | Case: a PoC plan only shows a demo flow. List five riskier questions and the tests for them. |
| SRB-013-EX04 | 3 | Given a filled matrix, run a sensitivity check and decide whether the result is robust. |
| SRB-013-EX05 | 3 | Estimate three-year total cost for a managed workflow service versus self-hosted, listing every cost line. |
| SRB-013-EX06 | 3 | Write an exit plan for a vendor-hosted workflow service: triggers, data export, rewrite effort, test of the exit. |
| SRB-013-EX07 | 4 | Case: a lead picked a favorite and then wrote the criteria. Identify the biases and propose corrections. |

## Solutions
- **EX01** Problem: relationship queries are slow and complex in current model; constraints: skills, operations, budget; options include optimized relational, graph database, do nothing; decision owner and date named.
- **EX02** Example criteria: delivery guarantees (must), operability, throughput headroom, team skill, cost; weights sum to 100 and are written before scoring.
- **EX03** Worker death mid-run, retries and duplicates, timeout handling, upgrade with running instances, observability of stuck instances. Each has a pass criterion.
- **EX04** Vary the top weights; if the winner flips with a small change, the choice is not robust and the contested criterion needs stakeholder decision.
- **EX05** Licence or hosting, infrastructure, engineering build time, operations and on-call, training, upgrades, support; compare over 36 months with stated assumptions.
- **EX06** Trigger examples: price rise, outage record, roadmap change. Export workflow definitions and state in an open format, estimate rewrite weeks, rehearse export and re-import of a sample.
- **EX07** Pre-chosen favorite and criteria fitted to it. Correct by rewriting criteria from the problem, having a second reviewer, scoring the do-nothing option, and re-running the matrix.
- Outcome 2 is also covered by the lab PoC and Q03; outcome 4 by Q07-Q08.

**Workplace evidence:** a technology evaluation you ran and the decision it produced.
