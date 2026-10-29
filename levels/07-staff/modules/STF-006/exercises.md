# STF-006 · Cross-domain systems — Exercises and lab

## Lab
### STF-006-LAB1 · Cross-domain map
**Outcomes:** 1–4 · **Time:** ~3 h
1. Map Platform 2.0's cross-domain systems (identity, billing, commerce core, data, integration) with consumers and coupling.
2. Decide for each: shared platform or domain-owned, with reasons.
3. Recommend an owner and a funding model for each shared system.
4. Choose one duplicated capability and plan consolidation in steps with side-by-side running.
5. Walk through the plan with role-played consumer teams.
**Acceptance:** consolidation plan keeps every consumer working at each step.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-006-EX01 | 1 | From a call-and-data flow table, identify the five most depended-on systems and the teams each constrains. |
| STF-006-EX02 | 1 | Three teams keep their own customer address store. Describe the risks and who is affected. |
| STF-006-EX03 | 2 | Apply the shared-or-domain test to notifications, pricing rules, and customer identity; justify each. |
| STF-006-EX04 | 3 | Propose ownership and funding for a shared search service used by eight teams, with service levels. |
| STF-006-EX05 | 4 | Plan the migration of a shared API from v1 to v2 for 12 consumers without a big-bang cutover. |
| STF-006-EX06 | 4 | A consumer team says the migration clashes with its launch. Describe how you adjust the plan. |

## Solutions
- **EX01** Rank by number of consumers and failure impact; typical: identity, commerce core, billing, data platform, integration.
- **EX02** Divergent data, inconsistent privacy handling, duplicated fixes; affects checkout, support, marketing.
- **EX03** Customer identity: shared platform. Notifications: shared platform if stable and common. Pricing rules: usually domain-owned, as they change with the business.
- **EX04** One search team with on-call, an API, SLOs, a request process; fund centrally for core, chargeback only for heavy custom indexing.
- **EX05** Version the API, run both, migrate willing consumers first, publish a timeline, offer help, retire v1 after the last consumer.
- **EX06** Shift that team's window, keep v1 available longer, avoid blocking others.

Outcome coverage: all four outcomes are covered by the exercises and lab.

**Workplace evidence:** a cross-domain system whose ownership or design you changed.
