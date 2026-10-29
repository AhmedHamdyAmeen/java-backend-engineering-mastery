# MID-065 · Engineering ownership — Exercises and lab

## Lab
### MID-065-LAB1 · Owner's pack
**Outcomes:** 1–4 · **Time:** ~2 h
1. Choose one Shop service and create its ownership page: purpose, owners, SLOs, dashboards, runbooks, dependencies, known risks.
2. List the top three technical debts with evidence, cost, effort, and a decision.
3. Run the production readiness checklist and record evidence.
4. Write a short health and trade-off note for product.
**Acceptance:** passes the readiness checklist.

## Exercises (assessment: readiness review; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-065-EX01 | 1 | List ten items an ownership page for `inventory` must contain and say why each matters. |
| MID-065-EX02 | 2 | Given a spent error budget, a feature request, and three debt items, make a prioritization with evidence. |
| MID-065-EX03 | 1 | Review a noisy alert list (twelve alerts) and decide which should page, which should ticket, and which should be deleted. |
| MID-065-EX04 | 3 | Run the readiness checklist for one service and list failed items with risk. |
| MID-065-EX05 | 4 | Write a one-paragraph note to product explaining a reliability-first quarter and its trade-offs. |

## Solutions
- **EX01** Purpose, owners and contacts, SLOs, dashboards, alerts, runbooks, dependencies, data stores, cost, known risks and debt: each lets another person operate or change the service.
- **EX02** Reliability first while the budget is spent; show evidence (incidents, lost hours); schedule the debt item with the highest cost per effort; give product a date for resuming features.
- **EX03** Page only on user-visible symptoms or SLO burn with a runbook; ticket for slow-burn issues; delete alerts nobody acts on.
- **EX04** Evidence per item (link or test result); failed items ranked by impact and likelihood, with owners and dates.
- **EX05** Start with the decision; state SLO performance, the cost of staying the course, what is delayed, and the date to review.
