# SRC-002 · Quality attributes — Exercises and lab

## Lab
### SRC-002-LAB1 · Utility tree
**Outcomes:** 1–4 · **Time:** ~2 h
1. Start from the SRC-001 scenarios and define each attribute (availability, scalability, maintainability, reliability, security, operability) with a measure.
2. Build the utility tree for the order subsystem: attributes, leaf scenarios, importance and difficulty ratings.
3. Review it with role-played stakeholders; force-rank to find the top three attributes.
4. Attach tactics, with cost and side effects, to every leaf.
**Acceptance:** top three attributes agreed with role-played stakeholders and justified.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-002-EX01 | 1 | Write a measurement definition for "checkout availability 99.95%" (probe, what counts as failure, window, exclusions) and compute allowed monthly downtime. |
| SRC-002-EX02 | 1 | Checkout depends serially on three services at 99.95%, 99.9%, and 99.9%. Estimate combined availability and say what you would do. |
| SRC-002-EX03 | 2 | Pick two attributes that conflict in the order subsystem and describe the trade-off including cost. |
| SRC-002-EX04 | 3 | Given a stakeholder who rates all ten leaves High, plan the conversation to reach a ranking. |
| SRC-002-EX05 | 4 | For the three top leaves, list two tactics each with cost and side effect. |
| SRC-002-EX06 | 1 | Turn "the system must be secure and maintainable" into two measurable scenarios. |

## Solutions
- **EX01** Probe the order-submit endpoint through the load balancer every 10 s plus real-request error rate; count 5xx and timeouts over 2 s as failures; monthly window; exclude announced maintenance if agreed. 0.05% of 30 days is about 21.6 minutes.
- **EX02** About 99.75% (0.9995 x 0.999 x 0.999 is roughly 0.9975), below target. Options: remove a dependency from the critical path, make one asynchronous, add a fallback, or add redundancy.
- **EX03** For example availability vs cost (second region doubles infrastructure) or latency vs consistency (replica reads are faster but stale). State the price and who accepts it.
- **EX04** Give a fixed budget of votes, ask what you would sacrifice first, show costs per leaf, and escalate unresolved choices to the accountable owner.
- **EX05** Availability: multi-AZ database with automated failover (cost, longer commit latency), graceful degradation (feature loss); latency: read cache (staleness), async confirmation emails (eventual delivery); operability: dashboards and runbooks (maintenance effort), SLO alerts (tuning effort).
- **EX06** Security: stolen token rejected after expiry and alert within 1 minute; maintainability: a small change in the order module goes to production in under one day with passing tests.

Outcome 3 is also covered by the lab review with role-played stakeholders; outcome 4 by the lab tactics column.

**Workplace evidence:** a design decision you influenced by making a quality attribute explicit.
