# JNR-051 · CI/CD introduction — Exercises and lab

## Lab
### JNR-051-LAB1 · Shop pipeline
**Outcomes:** 1–4 · **Time:** ~3 h
Every PR runs the full suite (including Testcontainers) with caching; merges to `main` publish a tagged image; `main` is protected with required checks.
**Acceptance:** a PR with a failing test cannot be merged.

## Exercises (assessment: fix a broken workflow)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-051-EX01 | 1 | Explain CI, continuous delivery, and continuous deployment in one sentence each, with a Shop example. |
| JNR-051-EX02 | 2 | Write a workflow that checks out, sets up Java 21 with Maven cache, and runs `./mvnw -B verify` on pull requests. |
| JNR-051-EX03 | 2 | Confirm Testcontainers tests run in the workflow and find the test count in the log. |
| JNR-051-EX04 | 3 | Add a job that builds the image and pushes it to `ghcr.io` tagged with the commit SHA on pushes to `main`. |
| JNR-051-EX05 | 4 | Configure branch protection requiring a PR, one review, and the `build` check. |
| JNR-051-EX06 | 2 | Given a broken workflow (wrong indentation, `-DskipTests`, missing `permissions`), find and fix each defect. |

## Solutions
- **EX01** CI: merge often and test automatically. Delivery: every green build is releasable, a human approves. Deployment: every green build goes live automatically.
- **EX02** `on: pull_request`; steps `actions/checkout`, `actions/setup-java` with `cache: maven`, `run: ./mvnw -B verify`.
- **EX03** Runners have Docker; the Surefire/Failsafe summary shows "Tests run: N"; N must be above zero.
- **EX04** `if` the event is a push to `main`; `permissions: packages: write`; `docker/login-action` with `GITHUB_TOKEN`; `docker/build-push-action` with `tags: ghcr.io/${{ github.repository }}:${{ github.sha }}`.
- **EX05** Settings, Branches (or Rulesets): require pull request, 1 approval, status check `build`, block force pushes.
- **EX06** Fix YAML indentation, remove `-DskipTests`, add `permissions: packages: write` for pushing images.
- Common mistakes (secrets printed in logs, zero tests run) are checked in the EX06 review.
