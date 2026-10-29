# SRC-011 · Production readiness — Exercises and lab

## Lab
### SRC-011-LAB1 · Launch the redesign
**Outcomes:** 1–4 · **Time:** ~4 h
Run a readiness review for the redesigned order subsystem (observability, capacity, failure handling, security, support) using agreed go/no-go criteria. Define a canary rollout with automated analysis on guard metrics, including a data-change rollback path. Seed a regression (for example a slow query) and roll out.
**Acceptance:** a seeded regression is halted at the canary stage; review record with decision and rollback rehearsal evidence.

## Exercises (assessment: run a readiness review for a peer's service)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-011-EX01 | 1 | Case: a service has dashboards but no alerts and no runbook. Write the five-area review findings with severities. |
| SRC-011-EX02 | 2 | Design a four-stage rollout for the order service: traffic, bake time, guard metrics, abort rules. |
| SRC-011-EX03 | 3 | Write go/no-go criteria for the launch, including who decides and what counts as an accepted risk. |
| SRC-011-EX04 | 4 | A release splits `orders.status` into two columns. Write the expand/contract plan with rollback at each step. |
| SRC-011-EX05 | 2 | Review a canary config that compares only mean latency on 1% traffic for 2 minutes. List its weaknesses and fixes. |
| SRC-011-EX06 | 3 | Case: launch day is fixed and the review finds a missing payment-timeout alert. Write your recommendation and how you present it. |

## Solutions
- **EX01** Blockers: no alerts, no runbook or on-call owner. Must-fix: paging alerts on SLO signals. Evidence is requested per area; "we will add later" becomes a tracked item.
- **EX02** Example: 1% / 10 min, 10% / 30 min, 50% / 30 min, 100%. Guard: error rate, p99, saturation, orders completed. Abort on tolerance breach against baseline.
- **EX03** Criteria such as: no open blockers, load test at forecast passed, rollback rehearsed, alerts verified. Decider named; accepted risks need an owner and an expiry date.
- **EX04** Expand: add new columns, dual-write. Migrate and backfill. Switch reads to the new columns. Contract: drop the old column in a later release. Before the contract step, rollback is a deploy.
- **EX05** Mean hides tails; volume is too small and the window too short. Use percentiles, error rate and a business metric, more traffic and longer bake time.
- **EX06** Recommend no-go, or a documented accepted risk with owner, expiry, and a manual check until the alert exists. Present facts and options, not blame.
- Outcome 1 is also covered by the lab review record; outcome 3 by Q06-Q07.

**Workplace evidence:** a launch you led with a readiness review and rollout plan.
