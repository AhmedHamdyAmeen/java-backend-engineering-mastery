# SRB-011 · Cross-team design — Exercises and lab

## Lab
### SRB-011-LAB1 · Program design
**Outcomes:** 1–4 · **Time:** ~4 h
1. Build the dependency map for the four FulfillCo teams: capabilities, owners, interfaces, consumer-to-provider arrows.
2. Draft interface agreements (schema, owner, versioning, date) and an integration timeline using stubs and feature flags.
3. Run a recorded design session with role-played team leads; include a seeded disagreement between two teams.
4. Resolve one conflict on record using agreed criteria.
**Acceptance:** every interface has an owner and a date; one conflict resolved on record.

## Exercises (assessment: session facilitation scored by role-players)
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-011-EX01 | 1 | Case: stock sync, shipment status, and returns involve four teams. Produce an ownership table and mark the busiest provider. |
| SRB-011-EX02 | 1 | A map shows a chain A to B to C to D. Identify the schedule risk and propose two ways to shorten it. |
| SRB-011-EX03 | 2 | Write the pre-read and agenda for a design session on returns, including roles, decision date, and what silence means. |
| SRB-011-EX04 | 3 | Write a contract-first plan for the stock-changed event: schema agreement, stub, contract test, flag, and swap date. |
| SRB-011-EX05 | 4 | Case: warehouse team wants a nightly batch; shop team wants near-real-time events. Write criteria, score both, and state what would change the decision. |
| SRB-011-EX06 | 2 | Review a transcript of a design session where one lead presented a finished design. Identify three process faults and fixes. |
| SRB-011-EX07 | 3 | Case: a consumer team has waited three weeks for a provider API. Write the unblocking message and a two-week plan. |

## Solutions
- **EX01** One accountable owner per capability and interface; the provider with the most inbound arrows (often the stock source) is the bottleneck and gets contracts first.
- **EX02** Chains serialize the schedule. Options: agree contracts early and use stubs so C and D start in parallel; split the middle service's work so a thin interface lands first.
- **EX03** Pre-read: problem, two or three options, constraints known. Agenda with time boxes; roles proposer/reviewer/informed; decision date; silence after the date recorded as agreement.
- **EX04** Week 1 agree schema and versioning rule; provider builds; consumer uses a stub behind a flag; both run contract tests in CI; swap stub for real event on an agreed date.
- **EX05** Criteria such as freshness need, delivery date, operational cost, reversibility. A plausible outcome: events for stock, batch reconciliation as a safety net; state what evidence (stock accuracy tolerance) would flip it.
- **EX06** Faults: no pre-read, decision made before the session, no recorded dissent or owners. Fixes: share options first, ask for constraints, record owners and dates.
- **EX07** Ask for the minimum viable contract, publish a stub, flag the integration, add a contract test and a date; inform managers after talking to the provider lead.
- Outcome 4 is also covered by the lab (conflict on record); outcome 2 by the lab recording and by Q03.

**Workplace evidence:** a cross-team design you led to agreement.
