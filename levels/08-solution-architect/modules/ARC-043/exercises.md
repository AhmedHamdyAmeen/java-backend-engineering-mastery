# ARC-043 · Solution documentation — Exercises and lab

## Lab
### ARC-043-LAB1 · Larkspur architecture pack
**Outcomes:** 1–4 · **Time:** ~3 h
1. Create the pack index with reader, owner, status, and version for each document.
2. Write the one-page executive summary.
3. Compile the decision log (at least five decisions), assumption log (at least five), and risk register (at least six) with owners and dates.
4. Define ownership and update triggers for each document and a handover reading order for operations and a future architect.
5. Have a role-played new architect answer ten questions using the pack alone; fix any gaps.
**Acceptance:** a role-played new architect answers ten questions using the pack alone.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-043-EX01 | 1 | Larkspur has a 120-page "solution document" that every group has stopped reading. Propose a pack structure by audience. |
| ARC-043-EX02 | 2 | Write a decision log entry for choosing a managed payment page and an assumption entry about a payment provider capability. |
| ARC-043-EX03 | 2 | Rewrite the risk "ERP integration problems" as an actionable register entry. |
| ARC-043-EX04 | 3 | Define update triggers and owners for HLD, LLD, risk register, and deployment diagram, and a check that catches stale documents. |
| ARC-043-EX05 | 4 | Plan the handover of the pack to operations and a successor architect: reading order, open items, and a verification step. |

## Solutions
- **EX01** Index and one-page summary; executive section (decision, value, risks, ask); reviewer section (HLD, ADRs, compliance); delivery section (LLD, contracts); operations section (deployment, runbooks, monitoring); each linked and owned.
- **EX02** Decision: context (card data scope), options, choice, consequences, owner, date. Assumption: capability statement, owner, confirm-by date, link to the decision it supports.
- **EX03** "Because the ERP vendor releases monthly, a changed stock API may break order promises; likelihood, impact, owner, mitigation (contract tests, change notice), trigger, review date."
- **EX04** HLD: owned by the architect, updated on any significant change or ADR; LLD: owned by the tech lead, updated per release; risk register: owner per risk, reviewed monthly; deployment diagram: owned by operations lead, updated on infrastructure change; health check compares documents with deployed reality at phase boundaries.
- **EX05** Reading order: summary, decision log, HLD, deployment, operations handover, risks; open decisions and risks listed with owners; verification: the successor answers a set of questions from the pack alone.

All four outcomes are also covered by the lab acceptance and the quiz.

**Workplace evidence:** an architecture pack you maintained through delivery.
