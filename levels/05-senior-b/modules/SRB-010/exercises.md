# SRB-010 · Platform engineering — Exercises and lab

## Lab
### SRB-010-LAB1 · Golden path for FulfillCo
**Outcomes:** 1, 2, 3, 4 · **Time:** ~3.5 h
1. Interview the four teams and list toil.
2. Build a service template with pipeline, telemetry, security scans, and deploy.
3. Add defaults and an escape hatch.
4. Time a new service from template to staging and define adoption metrics.
**Acceptance:** a new service reaches staging in under one hour using the template.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-010-EX01 | 1 | Write a three-sentence pitch for why FulfillCo needs a platform team. |
| SRB-010-EX02 | 2 | List five toil items across the four teams from the case. |
| SRB-010-EX03 | 2 | Rank two toil items by teams affected and hours saved. |
| SRB-010-EX04 | 3 | Design the golden path template contents and one escape hatch. |
| SRB-010-EX05 | 3 | Add guardrails for self-service database requests. |
| SRB-010-EX06 | 4 | Define three adoption metrics and a satisfaction survey question. |

## Solutions
- **EX01** Four teams repeat setup; inconsistent services; platform reduces toil and lowers cognitive load.
- **EX02** Pipeline setup, telemetry wiring, secrets, scans, deployment config.
- **EX03** Rank with numbers; the item affecting four teams with most hours first.
- **EX04** Template, CI, deploy, dashboards, SLO file; escape hatch: custom deploy with team-owned pipeline.
- **EX05** Default sizing, encryption, backups; policy denies public endpoints; quotas.
- **EX06** Adoption %, time to staging, tickets avoided; question: how easy was it to ship your last service?

**Workplace evidence:** a reusable capability other teams adopted.
