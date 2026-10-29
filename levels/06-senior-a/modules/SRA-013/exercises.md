# SRA-013 · Decision-making under uncertainty — Exercises and lab

## Lab
### SRA-013-LAB1 · Marketplace bets
**Outcomes:** 1–4 · **Time:** ~2 h
1. Build an assumption map for the Commerce 2030 marketplace architecture with at least fifteen assumptions, ranked by impact and uncertainty.
2. Design two experiments for the top assumptions with thresholds, cost caps, and decisions each outcome triggers.
3. Identify which decisions to commit now and which to keep open, and why.
4. Write decision records that include assumptions, signals, and review triggers.
5. The assessor invalidates one assumption mid-lab; respond by finding the affected decisions and proposing options.
**Acceptance:** response follows from the recorded assumptions.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-013-EX01 | 1 | List ten assumptions behind the plan "launch the marketplace in three countries in nine months" and rank them. |
| SRA-013-EX02 | 2 | Design an experiment for "sellers will integrate through our API" with a threshold and cost cap. |
| SRA-013-EX03 | 2 | Critique an experiment that cannot change the decision and rewrite it. |
| SRA-013-EX04 | 3 | Decide whether to commit to one payment provider now or keep two open; justify with option value and a commit date. |
| SRA-013-EX05 | 4 | Write a decision record for the seller data store including assumptions and review triggers. |
| SRA-013-EX06 | 4 | A recorded assumption fails (bulk file uploads dominate). Identify dependent decisions and propose options. |

## Solutions
- **EX01** Include business assumptions (seller count, order mix, commission), technical ones (peak, latency), and regulatory ones (residency); rank by impact and uncertainty; start with the high-high cell.
- **EX02** Hypothesis: at least 60% of three pilot sellers integrate within two weeks without support. Method: pilot with documentation only. Cost cap: two engineers for three weeks. If it fails, plan a batch-file path.
- **EX03** A load test run after the contract is signed cannot change the decision; move it before the commitment and set the threshold that decides.
- **EX04** Keep two open behind an interface if the interface is cheap and uncertainty is high; set the commit date at contract renewal; commit sooner if delay costs exceed the option value.
- **EX05** Record context, decision, options, assumptions with signals (seller write rate, data volume), consequences, review trigger (quarterly or when a signal trips), owner.
- **EX06** List decisions that used the assumption (ingestion interface, capacity plan, support model); options: adapt, add batch path, reverse; compare remaining cost, not sunk cost; update records.

Outcome 3 is also covered by the lab and the quiz.

**Workplace evidence:** a decision you made with explicit assumptions and later revisited.
