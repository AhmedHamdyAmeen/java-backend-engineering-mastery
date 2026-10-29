# SRA-002 · Long-term system evolution — Exercises and lab

## Lab
### SRA-002-LAB1 · Fitness and lifecycle
**Outcomes:** 1–4 · **Time:** ~2 h
1. Choose five qualities for the commerce area (for example coupling, checkout latency, security patch age, cost per order, test coverage of critical flows) and define measure, threshold, and owner for each.
2. Implement them as automated checks that run in CI or on a schedule, with a baseline for current violations.
3. Inventory every runtime, framework, and datastore in the case and record versions and end-of-support dates (verify before recording).
4. Build a three-year obsolescence calendar with upgrade plans, owners, and effort.
5. Introduce one changed assumption (a vendor notice) and revise the roadmap.
**Acceptance:** fitness functions run in CI; calendar covers every runtime, framework, and datastore.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-002-EX01 | 1 | Write a fitness function for "checkout p99 stays under 800 ms" including measure, threshold, owner, and what happens on failure. |
| SRA-002-EX02 | 1 | A coupling rule has 140 existing violations. Design the rollout so it can be enforced without halting delivery. |
| SRA-002-EX03 | 2 | Convert a feature-list roadmap into target state, two transition states, and checkpoints with the evidence each checkpoint needs. |
| SRA-002-EX04 | 3 | Given an inventory of eight components, build an obsolescence calendar and rank the three highest risks. |
| SRA-002-EX05 | 3 | Evaluate vendor viability for a datastore after a licence change: list signals, options, and a decision date. |
| SRA-002-EX06 | 4 | A launch is delayed by six months. Revise the roadmap and write a half-page note explaining what moved and why. |

## Solutions
- **EX01** Measure: p99 latency of checkout API from production telemetry, rolling 7 days; threshold 800 ms; owner the checkout team; on breach, open a tracked item and block risky releases touching checkout until a plan exists. Also run a pre-release load check in CI.
- **EX02** Baseline the 140, fail only on new violations, publish a trend, assign each baseline item to its team with a retirement date, and add a short exception process with expiry.
- **EX03** Target in capabilities and qualities; transition 1 and 2 each deliver value alone; checkpoints name evidence (adoption, latency, incidents) and decisions (continue, adjust, stop).
- **EX04** Rank by end-of-support date, blast radius, and effort; the highest risks are typically a datastore with a near deadline, a runtime shared by many services, and a framework with no upgrade path (verify dates).
- **EX05** Signals: licence terms, release cadence, community and commercial support, migration cost. Options: stay with a support contract, fork or migrate; set a decision date well before the cost of delay rises.
- **EX06** Move dependent items, keep transition states valid, shift obsolescence work that no longer fits, update assumptions, and state the business impact so leadership can confirm.

Outcome 2 is also covered by the lab roadmap revision; outcome 4 by the quiz and the lab changed-assumption step.

**Workplace evidence:** a fitness function or lifecycle plan adopted by multiple teams.
