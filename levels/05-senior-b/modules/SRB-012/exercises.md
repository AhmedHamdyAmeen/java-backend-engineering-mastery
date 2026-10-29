# SRB-012 · Architecture governance — Exercises and lab

## Lab
### SRB-012-LAB1 · Program governance
**Outcomes:** 1–4 · **Time:** ~3 h
1. Write the RFC template, review cadence, and exception process for the FulfillCo program, including tiers by reversibility and blast radius.
2. Run two reviews with role-played team leads: one on a hard-to-reverse cross-team change, one on a local change.
3. Record decisions, concerns, and any exception raised.
**Acceptance:** both RFCs reach a decision within the deadline.

## Exercises (assessment: review facilitation)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-012-EX01 | 1 | Case: an RFC has no owner, no deadline, and 40 comments. Write the process fixes and the decision note. |
| SRB-012-EX02 | 1 | Write an RFC outline (headings plus one line each) for choosing the shipment-status event contract. |
| SRB-012-EX03 | 2 | Review a log of a design review where the reviewer added new requirements at the end. Rewrite the closing minutes. |
| SRB-012-EX04 | 3 | Write an exception record for a team that needs a non-standard database for one service, with expiry and follow-up. |
| SRB-012-EX05 | 4 | Classify five changes (new logging library, public event schema, rename internal class, new datastore, change of retry timeout) into governance tiers. |
| SRB-012-EX06 | 2 | Case: a review ends with "let's think about it". Write what the facilitator says to get a decision. |

## Solutions
- **EX01** Name a decision owner, state a decision date, require comments by a deadline, group comments into blockers and suggestions, record the outcome with reasons.
- **EX02** Headings: context, goals/non-goals, options (stream, polling, webhook), recommendation, risks, rollout, reviewers, decision deadline.
- **EX03** Minutes list required changes with owners, move new ideas to a follow-up list, state the decision (accepted with changes) and the confirmation date.
- **EX04** Record: standard, deviation, reason, risk, mitigation (own backup and monitoring), owner, expiry (for example six months), review action.
- **EX05** Logging library: none or note. Rename: none. Retry timeout: peer note. Public event schema: full RFC. New datastore: design review or RFC depending on blast radius.
- **EX06** Restate options and criteria, ask for the remaining blocking concern, then state a decision or a dated next step with an owner.
- Outcome 4 is also covered by the lab (two tiers of review).

**Workplace evidence:** an RFC or review process you introduced and its effect on decision time.
