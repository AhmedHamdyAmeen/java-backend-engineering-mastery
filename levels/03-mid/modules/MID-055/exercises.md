# MID-055 · CI/CD advanced — Exercises and lab

## Lab
### MID-055-LAB1 · Promotion pipeline
**Outcomes:** 1–4 · **Time:** ~3 h
Build a pipeline for Shop services: build one image, deploy to dev, then staging with gates (tests, contracts, scans, coverage threshold), then production with approval. Use a rolling or blue-green strategy with a post-deploy smoke check and automatic rollback. Put one new feature behind a flag.
**Acceptance:** a deliberately broken release is rolled back without human action.

## Exercises (assessment: pipeline review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-055-EX01 | 1 | Review a pipeline that builds a separate image per environment. List the problems and the fix. |
| MID-055-EX02 | 2 | Choose gates for `orders` and order them by speed; state what blocks a merge versus a deployment. |
| MID-055-EX03 | 3 | Compare rolling, blue-green, and canary for the `payments` service; pick one with reasons. |
| MID-055-EX04 | 3 | Plan a database column rename so that a rollback stays safe. |
| MID-055-EX05 | 4 | Put a new discount rule behind a flag; define rollout stages and the removal date. |
| MID-055-EX06 | 1 | List the manual production steps in a given runbook and automate two of them. |

## Solutions
- **EX01** Rebuilds can differ from the tested artifact and are slower; build once, tag by SHA, promote by digest, configure per environment.
- **EX02** Fast first: lint and unit tests, then integration and contract tests, then scans. Merge gates: tests, contracts, scans. Deployment gates: smoke tests and SLO check.
- **EX03** For payments, blue-green or canary with automatic rollback to limit exposure; rolling is acceptable if the change is backward compatible and probes are good.
- **EX04** Expand and contract: add the new column, write to both, migrate, switch reads, drop the old column in a later release.
- **EX05** Flag default off; staff, then 5%, 25%, 100% watching error rate; remove the flag and the old path within a set period.
- **EX06** Example: manual database migrations and smoke tests become pipeline jobs; approval remains only for the production gate.

**Outcome 4** is also covered by quiz Q09–Q10; outcomes 1–3 by the lab and the pipeline review.
