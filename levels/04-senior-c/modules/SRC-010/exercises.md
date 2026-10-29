# SRC-010 · Architecture documentation — Exercises and lab

## Lab
### SRC-010-LAB1 · Subsystem architecture pack
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Write the architecture description (context, containers, key components, quality attributes, constraints) for the order subsystem as docs-as-code.
2. Write the design doc for the 10× redesign (decision needed, options, recommendation, risks, rollout).
3. Write runbooks for the top five failure modes from SRC-009.
4. Have a peer execute one runbook without help; revise from their feedback.
**Acceptance:** a peer executes a runbook successfully without help.

## Exercises (documentation review; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-010-EX01 | 1 | Make an audience matrix (engineers, operators, leadership) for the order subsystem docs with the question each answers. |
| SRC-010-EX02 | 1 | Sketch the C4 context and container views of the order subsystem in text form. |
| SRC-010-EX03 | 2 | Propose a repository layout and CI checks that keep docs current. |
| SRC-010-EX04 | 3 | Rewrite the runbook step "check if the database is OK" into executable steps. |
| SRC-010-EX05 | 4 | Review a design doc that starts with background and ends without a recommendation; restructure it. |
| SRC-010-EX06 | 3 | Review a runbook for missing symptom, impact, rollback, and escalation sections and fix it. |

## Solutions
- **EX01** Engineers: structure, decisions, interfaces; operators: failure handling, dashboards, procedures; leadership: risks, cost, outcomes, status. Different documents, linked.
- **EX02** Context: customers, web app, payment provider, warehouse; containers: gateway, order service, PostgreSQL, Kafka, inventory; label protocols.
- **EX03** `docs/architecture`, `docs/adr`, `docs/runbooks` in the repo; link check and diagram build in CI; owner and review date in front matter; docs reviewed in the code PR.
- **EX04** Step: run the connection-count query (exact SQL), expected below N; check replica lag via the dashboard link, expected below 5 s; if not, go to step with failover decision; escalate after 15 minutes.
- **EX05** Move the decision needed and recommendation to the top, then context, goals, options with trade-offs, risks, rollout, open questions.
- **EX06** Add symptom and impact, ordered quick checks with expected results, rollback, escalation contacts, and verification of recovery.

**Workplace evidence:** a design doc or runbook used by others without your help.
