# ARC-003 · Requirements discovery — Exercises and lab

## Lab
### ARC-003-LAB1 · Larkspur requirements baseline
**Outcomes:** 1–5 · **Time:** ~4 h
1. Plan the workshop: objective, agenda, participants, pre-reads, expected outputs.
2. Run a role-played workshop with store operations, e-commerce, finance, IT, and security (peers or assessor play them).
3. Capture functional requirements as journeys or use cases and nonfunctional requirements as quality scenarios.
4. Record constraints and assumptions, with owners and check dates for assumptions.
5. List conflicts with options and a decision owner.
6. Assemble the baseline with a traceability ID per requirement and a change-control note.
**Acceptance:** every nonfunctional requirement is measurable; conflicts listed with a decision owner.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-003-EX01 | 1 | Write a one-page workshop plan and six interview questions for Larkspur store operations. |
| ARC-003-EX02 | 1 | Two participants dominate a session; describe three facilitation moves and when to use each. |
| ARC-003-EX03 | 2 | Write one journey with a failure flow for "customer picks up an online order" and give it IDs. |
| ARC-003-EX04 | 2 | Rewrite "the shop must be fast, secure, and always available" as three measurable quality scenarios. |
| ARC-003-EX05 | 3 | Sort twelve statements into constraints and assumptions, and assign an owner and a verification step to each assumption. |
| ARC-003-EX06 | 4, 5 | Store operations wants stock accuracy checked hourly; finance forbids new nightly ERP load. Present the trade-off, two options, a recommendation, and a decision owner; show how the baseline records it with change control. |

## Solutions
- **EX01** Plan has objective, 3-hour agenda, invitees with decision rights, pre-read, outputs. Questions probe failures, peak days, current workarounds, and decision owners.
- **EX02** Silent ranking round, time-boxes, direct invitation of quiet participants; the parking lot for tangents.
- **EX03** Steps from notification to handover; failure flow: wrong ID, order not ready; IDs like FR-021 with links to capabilities.
- **EX04** Example: 95% of product pages under 1.5 s at 2,000 shoppers per minute; account takeover attempts blocked after five failures per minute; 99.9% monthly availability of checkout excluding planned windows.
- **EX05** Constraints are fixed (ERP remains finance ledger); assumptions need verification such as measuring store network bandwidth by a date.
- **EX06** Options: hourly cycle count events to an inventory service with ERP nightly reconcile, or ERP API polling limited by capacity. Recommend the first; CIO and finance decide. Baseline stores requirement IDs, decision, date, and change log with version.

Outcome 5 is also covered by the lab traceability step.

**Workplace evidence:** a requirements baseline you facilitated that was signed off by the business.
