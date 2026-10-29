# STF-002 · Technical strategy — Exercises and lab

## Lab
### STF-002-LAB1 · Platform 2.0 strategy
**Outcomes:** 1–4 · **Time:** ~3 h
1. Gather evidence: delivery data, incident history, cloud cost by team, and survey comments (use the case materials).
2. Write the diagnosis, naming two or three root causes with evidence.
3. Write guiding policies and actions; trace each to evidence and a business priority.
4. List what will explicitly stop, with the capacity it frees.
5. Present to a role-played CTO and CPO, record their decisions, and set a refresh date.
**Acceptance:** every action traces to evidence and a business priority; at least one thing is explicitly stopped.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-002-EX01 | 1 | Given the business goals "enter three countries", "cut cloud cost 15%", "fewer outages", map each to an engineering investment and a measure. |
| STF-002-EX02 | 2 | Review a strategy document written from opinion ("we should use Kubernetes everywhere"); list the missing evidence and rewrite the first paragraph as a diagnosis. |
| STF-002-EX03 | 2 | Given a table of lead time by team with different definitions of "deploy", explain how you would make the data comparable. |
| STF-002-EX04 | 3 | A strategy proposes four new initiatives and no stops. Identify three things to stop and quantify the capacity freed. |
| STF-002-EX05 | 4 | Plan the endorsement: who to pre-wire, what each leader must decide, and how objections are handled. |
| STF-002-EX06 | 4 | Six months on, delivery data contradicts one guiding policy. Describe how the refresh process responds. |

## Solutions
- **EX01** Countries: self-service new-service path (days from idea to production); cost: standard compute templates and rightsizing (cost per order); outages: shared reliability program (repeat incidents per quarter).
- **EX02** Missing: baseline data, alternatives, cost, link to a priority. Rewrite as a problem statement with evidence.
- **EX03** Agree one definition (for example, production deploy of a customer-visible change), re-extract from deploy logs, and flag teams whose data cannot be reconciled.
- **EX04** Examples: duplicate CI tools, a bespoke logging stack, an optional review board; state engineer-months freed per item.
- **EX05** Pre-wire the CTO, CPO, VP Engineering, and two senior managers; ask for a sponsor, funding, and a named stop; record objections and responses.
- **EX06** Treat as new evidence: publish the data, revise or retire the policy, and tell teams what changed and why.

Outcomes are also checked by the quiz; the lab acceptance covers evidence tracing and the stop.

**Workplace evidence:** an organization-wide strategy you authored or shaped that leadership adopted.
