# ARC-035 · Architecture review boards — Exercises and lab

## Lab
### ARC-035-LAB1 · ARB submission
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Draft the submission: the decision asked, context, options considered, recommended solution, and risks.
2. Pre-wire at least two role-played board members and record their concerns.
3. Build the compliance table against the provided principles and standards with evidence links.
4. Write one exception request with mitigation, owner, and expiry.
5. Present to the role-played ARB and respond to the conditions raised.
6. Create the condition tracker with owners, dates, and closure evidence.
**Acceptance:** approval or conditional approval with a closure plan.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-035-EX01 | 1 | Larkspur's board meets monthly and the pre-read deadline is five days before. Create a timeline from today to a decision and list who you pre-wire and why. |
| ARC-035-EX02 | 2 | Review a compliance table that is all green with no evidence. Rewrite three lines honestly with status and evidence. |
| ARC-035-EX03 | 3 | Write an exception for using a file-transfer interface with ERP when the standard requires APIs; include risk, mitigation, owner, and expiry. |
| ARC-035-EX04 | 3 | The board rejects an exception request with no expiry date. Explain why and repair the request. |
| ARC-035-EX05 | 4 | The board approves with three conditions. Build a tracker, assign owners, and write the status report you will send in six weeks. |

## Solutions
- **EX01** Work backwards: decision date, pre-read five days earlier, pre-wiring in the two weeks before, draft earlier still; pre-wire security (data classification), infrastructure (hosting), and data (retention), each with their likely concern.
- **EX02** Example: "API-first integration: compliant with condition, order posting uses APIs, ERP stock feed uses file transfer, see ADR-004"; each line has a design element and an evidence link.
- **EX03** Standard: API-first; reason: ERP cannot expose APIs before its upgrade; risk: delayed and unauthenticated data; mitigation: encrypted transfer, reconciliation job, alert on missing files; owner: integration lead; expiry: ERP upgrade milestone, with re-review date.
- **EX04** Without expiry the exception becomes permanent and the risk is never revisited; add an expiry date or trigger and a review owner.
- **EX05** Tracker columns: condition, owner, due date, evidence, status; report lists closed, in progress, and at-risk items with the plan for each.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** a solution you took through formal architecture governance.
