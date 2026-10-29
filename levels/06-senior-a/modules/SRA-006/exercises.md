# SRA-006 · Enterprise resilience — Exercises and lab

## Lab
### SRA-006-LAB1 · Resilience posture
**Outcomes:** 1–4 · **Time:** ~2 h
1. Tier Commerce 2030 capabilities by survival need and agree recovery targets with role-played business owners.
2. Assess regional and provider failure scenarios and decide what must survive each.
3. Plan a chaos program: backlog of experiments with hypotheses, blast radius, abort criteria, cadence, and review process.
4. Map shared dependencies, correlated risks, single teams, and knowledge silos.
5. Rank investments and quantify the top risk in business impact.
**Acceptance:** top risk quantified in business impact.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-006-EX01 | 1 | Tier ten capabilities (must survive, degrade, may stop) and set recovery targets; justify the two hardest placements. |
| SRA-006-EX02 | 1 | A cloud account lock-out scenario: list what breaks, what must survive, and the cheapest design that meets the target. |
| SRA-006-EX03 | 2 | Write a chaos experiment for a message broker degradation: hypothesis, steady state, blast radius, abort criteria, follow-up. |
| SRA-006-EX04 | 2 | Critique a proposed chaos experiment that has no hypothesis and runs in production at full scale; rewrite it. |
| SRA-006-EX05 | 3 | From four incident summaries, find the common dependency and propose two mitigations with owners. |
| SRA-006-EX06 | 4 | Write a one-page resilience investment case with three ranked investments and the top risk in business impact. |

## Solutions
- **EX01** Checkout, payments, and order capture must survive; search and recommendations degrade; internal reporting may stop. Hard calls are justified by revenue and legal impact.
- **EX02** Breaks: provisioning, deployment, possibly all services in the account. Must survive: checkout and payments. Cheapest: backups and infrastructure code in a second account, tested restore, break-glass access, with a stated recovery time.
- **EX03** Hypothesis: checkout success stays above 99% with broker latency of 2 s because producers time out and retry. Blast radius: one consumer group in staging, then 1%. Abort: success below 98% or a customer-visible error spike. Follow-up: fix missing timeouts.
- **EX04** Missing: hypothesis, steady-state metric, blast radius, abort criteria, watcher, review. Rewrite starting in staging with small cohorts.
- **EX05** Typical common causes: shared certificate expiry, a shared config service, a single on-call engineer. Mitigations: expiry monitoring and automation; redundancy or caching; cross-train owners.
- **EX06** Rank by risk reduced per cost; show cost, residual risk, and the revenue-at-risk calculation with assumptions (for example hourly revenue times expected outage hours).

Outcome 4 is also covered by the lab ranking and the quiz.

**Workplace evidence:** a resilience program or systemic risk you led action on.
