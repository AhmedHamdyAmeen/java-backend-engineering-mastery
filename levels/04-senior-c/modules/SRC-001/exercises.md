# SRC-001 · Requirements engineering — Exercises and lab

## Lab
### SRC-001-LAB1 · Requirements for 10×
**Outcomes:** 1–4 · **Time:** ~2 h
1. Role-play product, finance, and operations interviews (record them); a peer or assessor plays each stakeholder.
2. Extract functional and nonfunctional requirements; separate constraints and assumptions into their own register.
3. Write at least eight quality-attribute scenarios (source, stimulus, environment, artifact, response, measure) covering availability, latency, durability, scalability, security, and operability.
4. List missing, conflicting, and untestable items; assign an owner to each conflict and propose options.
5. Assemble the requirements document.
**Acceptance:** every scenario is measurable; conflicts listed with owners.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-001-EX01 | 1 | Product says "checkout must be fast and scalable". Write six interview questions that convert it into requirements. |
| SRC-001-EX02 | 2 | Classify ten statements about the order subsystem as requirement, constraint, or assumption and name an owner for each assumption. |
| SRC-001-EX03 | 3 | Write a six-part scenario for "order tracking stays available during a database failover". |
| SRC-001-EX04 | 3 | Rewrite three vague scenarios ("quick", "highly available", "secure") so each has a measure. |
| SRC-001-EX05 | 4 | Find the missing, conflicting, and untestable requirements in a given draft list of eight items. |
| SRC-001-EX06 | 4 | Prepare a trade-off conversation: 99.95% availability vs a flat infrastructure budget. Present two options with cost, risk, and recommendation. |

## Solutions
- **EX01** Examples: Which actions? What response time at which percentile? Peak load and when? What does a minute of downtime cost? What may degrade first? Who decides trade-offs?
- **EX02** Constraints are fixed (PostgreSQL as system of record, EU data residency); assumptions are beliefs to verify (peak 6× average); requirements need an owner and a measure.
- **EX03** Source: operations-triggered failover; stimulus: primary database loss; environment: peak hour; artifact: tracking API; response: reads served from replica, stale data flagged; measure: 99.9% of tracking requests succeed during a 60 s failover, staleness under 30 s.
- **EX04** "Quick" becomes p99 under 800 ms at 600 req/s; "highly available" becomes 99.95% monthly measured at the load balancer excluding planned maintenance; "secure" becomes a named threat and a response, e.g. credential stuffing blocked after 5 attempts per minute.
- **EX05** Missing: retention and recovery targets; conflicting: zero downtime deploys vs no extra environment; untestable: "user friendly". Resolve each with stakeholders and record the answer.
- **EX06** Option A second region (higher cost, meets target), option B multi-AZ with automated failover and a 15-minute recovery (cheaper, risk of regional outage); recommend by quantifying outage cost with Finance; record the decision and owner.

Outcome 1 is also covered by the interview recording in the lab; outcome 2 by the lab register.

**Workplace evidence:** a requirements or design document you wrote that changed scope or a target after stakeholder discussion.
