# SRB-019 · Risk management — Exercises and lab

## Lab
### SRB-019-LAB1 · Program risks
**Outcomes:** 1–4 · **Time:** ~3 h
1. Run a pre-mortem and build the risk register for the FulfillCo program across technical, dependency, people, and schedule categories, with owners and triggers.
2. Plan spikes or staged commitments for the riskiest items.
3. Write contingency plans for the top three risks with invocation thresholds.
4. The assessor triggers one risk mid-lab; respond.
**Acceptance:** response follows the plan or justifies deviation.

## Exercises (assessment: risk-response simulation)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-019-EX01 | 1 | Run a pre-mortem on the FulfillCo program and list at least eight risks across the four categories. |
| SRB-019-EX02 | 2 | Convert five risks into register rows with likelihood, impact, owner, and trigger. |
| SRB-019-EX03 | 2 | Case: a register has 60 risks, no owners, and was last updated four months ago. Write the repair plan. |
| SRB-019-EX04 | 3 | Choose a spike for the risk "stock sync cannot keep up with peak load": question, time box, decision enabled. |
| SRB-019-EX05 | 3 | Propose a staged commitment for the program so that stage two is approved after three risks fall. |
| SRB-019-EX06 | 4 | Write a contingency card for "legacy warehouse expert leaves", including trigger and cost. |
| SRB-019-EX07 | 4 | Case: the trigger of a top risk fires on a Friday. Write the decision memo with options and your recommendation. |

## Solutions
- **EX01** Examples: warehouse data quality (technical), API not ready (dependency), single expert (people), fixed launch date (schedule), security review queue (dependency), unclear event ownership, migration backfill load, vendor contract delay.
- **EX02** Each row has one owner and an observable trigger, such as "contract unsigned by week 3".
- **EX03** Cut to the top ten, assign owners, add triggers, set a monthly review, and archive closed items.
- **EX04** Question: can the sync path handle peak volume; run a load spike for three days; decision: events or batch.
- **EX05** Stage one covers discovery and key spikes; the exit check is that top risks fall below an agreed score; stage two commits the build.
- **EX06** Trigger: resignation or long absence; actions: documentation sprint now, pairing with a second engineer, vendor support; cost: time and training.
- **EX07** Options: invoke contingency, wait with a short deadline, or re-plan; recommend per the threshold in the card; state impact and ask.
- Outcome 1 is also covered by the lab pre-mortem.

**Workplace evidence:** a risk you identified early and the action it led to.
