# ARC-006 · Solution architecture lifecycle — Exercises and lab

## Lab
### ARC-006-LAB1 · Architecture plan
**Outcomes:** 1–4 · **Time:** ~3 h
1. Start from a given Larkspur program plan (phases, teams, milestones).
2. Lay out the lifecycle stages with deliverables and exit criteria per stage.
3. Place reviews and name a decision-maker for each.
4. Define the delivery-support model: design authority scope, decision log format, office hours.
5. Add transition and handover tasks with acceptance criteria.
**Acceptance:** aligned with the program plan; every review has a decision-maker.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-006-EX01 | 1 | Draw the seven-stage lifecycle for Larkspur and mark the decision at the end of each stage. |
| ARC-006-EX02 | 2 | Write exit criteria and deliverables for discovery, options, and design. |
| ARC-006-EX03 | 2 | A review is scheduled with no named decision-maker. Explain the risk and fix the schedule. |
| ARC-006-EX04 | 3 | Three teams complain that waiting for architect approval slows them. Redesign the support model. |
| ARC-006-EX05 | 3 | Write a decision-log entry for choosing near-real-time inventory events. |
| ARC-006-EX06 | 4 | Write a handover checklist and acceptance criteria for the operations team. |

## Solutions
- **EX01** Discovery → baseline signed; options → option chosen; design → target architecture drafted; review → approval; delivery support → continuous guidance; transition → cutover complete; handover → operations accepts.
- **EX02** Discovery: signed baseline. Options: compared options paper and recommendation. Design: approved target architecture and risks with conditions.
- **EX03** An undecided review produces opinions and not approval; name the decision-maker (design authority chair or sponsor) and the decision options.
- **EX04** Define guardrails, which changes need approval (interfaces, data ownership, quality targets), a two-day response target, scheduled office hours, and delegation within guardrails.
- **EX05** Record: context (stock accuracy, ERP limits), decision (event-based inventory service with nightly reconciliation), alternatives, consequences, owner, date.
- **EX06** Documentation, dashboards, alerts, runbooks, on-call ownership, access, open risks, rollback plan; acceptance signed by operations and owning teams.

**Workplace evidence:** a solution you took from discovery through handover.
