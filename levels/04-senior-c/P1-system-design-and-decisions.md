# SRC-P1 — System Design and Architecture Decisions

**Phase goal:** the engineer turns vague goals into explicit requirements and quality targets, sizes and models a system before building it, chooses between architectures with documented trade-offs, and anticipates how it will fail.

**Running case:** *Order Processing at 10×* — Shop Platform's order subsystem (from `MID-CAP`) must handle a 10× growth forecast, a new 99.95% availability commitment, and a 15-minute recovery objective. Every lab advances the Senior C capstone (`SRC-CAP`).

**Format:** Senior modules are case-study driven. Lectures are shorter on mechanics and longer on judgment; demos are worked design sessions on the running case, thinking aloud — including the dead ends.

**Phase total:** ~14.3 h video · ~40.5 h practice

---

### SRC-001 · Requirements engineering
`n: 175` · **Video:** 81 min · **Practice:** 4 h

**Prerequisites:** MID-064

**Learning outcomes** — the engineer can:
1. Elicit functional and nonfunctional requirements from stakeholders who state goals, not requirements.
2. Separate requirements, constraints, and assumptions, and record each explicitly.
3. Write quality-attribute scenarios (source, stimulus, environment, response, measure).
4. Identify missing, conflicting, and untestable requirements and resolve them with stakeholders.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-001-L01 | Why systems fail at the requirements stage | 10 |
| SRC-001-L02 | Functional vs nonfunctional requirements | 10 |
| SRC-001-L03 | Constraints and assumptions | 10 |
| SRC-001-L04 | Stakeholder interviews that surface real needs | 12 |
| SRC-001-L05 | Quality-attribute scenarios | 14 |
| SRC-001-L06 | Conflicts and trade-off conversations | 10 |
| SRC-001-L07 | Demo: turning "orders must never be lost" into testable requirements | 15 |

**Lab** — `SRC-001-LAB1` *Requirements for 10×:* from a role-played product, finance, and operations interview, produce a requirements document with constraints, assumptions, and at least eight quality-attribute scenarios. Acceptance: every scenario is measurable; conflicts listed with owners.

**Common mistakes:** accepting "fast" and "scalable" as requirements; hidden assumptions; designing before asking.

**Assessment:** requirements review against a rubric; interview role-play recorded.

**Workplace evidence:** a requirements or design document you wrote that changed scope or a target after stakeholder discussion.

**Career relevance:** requirements discovery for architects (ARC-003).

---

### SRC-002 · Quality attributes
`n: 176` · **Video:** 89 min · **Practice:** 4 h

**Prerequisites:** MID-049, SRC-001

**Learning outcomes** — the engineer can:
1. Define availability, scalability, maintainability, reliability, security, and operability in measurable terms.
2. Explain how quality attributes trade off against each other and against cost.
3. Prioritize quality attributes with stakeholders using a utility tree.
4. Map each prioritized attribute to the tactics that achieve it.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-002-L01 | Quality attributes drive architecture | 10 |
| SRC-002-L02 | Availability and reliability, measured | 12 |
| SRC-002-L03 | Scalability and elasticity | 10 |
| SRC-002-L04 | Maintainability and operability | 10 |
| SRC-002-L05 | Security as a quality attribute | 8 |
| SRC-002-L06 | Utility trees and prioritization | 12 |
| SRC-002-L07 | Tactics catalog | 12 |
| SRC-002-L08 | Demo: building the utility tree for the order subsystem | 15 |

**Lab** — `SRC-002-LAB1` *Utility tree:* prioritized utility tree for the order subsystem with tactics per leaf. Acceptance: top three attributes agreed with role-played stakeholders and justified.

**Common mistakes:** treating every attribute as top priority; availability numbers without a measurement definition.

**Assessment:** utility-tree review.

**Workplace evidence:** a design decision you influenced by making a quality attribute explicit.

**Career relevance:** architecture principles (ARC-007) and reviews (SRA-017).

---

### SRC-003 · Architecture trade-offs
`n: 177` · **Video:** 96 min · **Practice:** 4 h

**Prerequisites:** MID-063, SRC-002

**Learning outcomes** — the engineer can:
1. Identify the decisions that are expensive to reverse and spend design effort on them first.
2. Evaluate options against prioritized quality attributes using a lightweight ATAM-style review.
3. Account for complexity as a cost (cognitive load, operational burden, onboarding).
4. Record trade-offs, risks, and sensitivity points in ADRs.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-003-L01 | Every decision is a trade-off | 10 |
| SRC-003-L02 | One-way and two-way doors | 10 |
| SRC-003-L03 | Complexity budgets | 12 |
| SRC-003-L04 | The cost of abstraction | 10 |
| SRC-003-L05 | Lightweight architecture evaluation | 14 |
| SRC-003-L06 | Risks, sensitivity points, and trade-off points | 10 |
| SRC-003-L07 | Demo: evaluating three designs for order storage | 15 |
| SRC-003-L08 | Demo: an architecture review that changes its mind | 15 |

**Lab** — `SRC-003-LAB1` *Option analysis:* three candidate designs for scaling the order subsystem evaluated against the utility tree; ADR for the chosen one. Acceptance: rejected options documented with honest strengths.

**Common mistakes:** strawman alternatives; ignoring operational cost; deciding reversible things slowly and irreversible things quickly.

**Assessment:** ADR defense with assessor challenges.

**Workplace evidence:** an ADR or design review where you recommended against a more complex option.

**Career relevance:** solution options (ARC-033) and decision-making under uncertainty (SRA-013).

---

### SRC-004 · Capacity planning
`n: 178` · **Video:** 94 min · **Practice:** 5 h

**Prerequisites:** MID-046, SRC-002

**Learning outcomes** — the engineer can:
1. Derive peak RPS, concurrency, and data growth from business forecasts.
2. Estimate storage, network, and compute needs with back-of-the-envelope calculations.
3. Validate estimates with load-test data and identify headroom per component.
4. Present a capacity plan with assumptions, margins, and triggers for re-planning.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-004-L01 | From business forecast to load | 12 |
| SRC-004-L02 | Peaks, seasonality, and burst factors | 10 |
| SRC-004-L03 | Back-of-the-envelope estimation | 14 |
| SRC-004-L04 | Storage and data growth | 10 |
| SRC-004-L05 | Headroom and saturation points | 10 |
| SRC-004-L06 | Capacity plans people can act on | 8 |
| SRC-004-L07 | Demo: sizing the order subsystem for Black Friday at 10× | 15 |
| SRC-004-L08 | Demo: checking last year's capacity plan against reality | 15 |

**Lab** — `SRC-004-LAB1` *10× capacity plan:* capacity plan for orders, inventory, Kafka, and PostgreSQL, validated against MID load-test data. Acceptance: every number traceable to an assumption; first bottleneck named.

**Common mistakes:** averaging away peaks; forgetting replication and retention multipliers; no re-planning triggers.

**Assessment:** timed estimation exercise.

**Workplace evidence:** a capacity estimate you produced and later compared with actual usage.

**Career relevance:** large-scale performance (SRA-007) and cost architecture (ARC-021).

---

### SRC-005 · Performance modeling
`n: 179` · **Video:** 73 min · **Practice:** 4 h

**Prerequisites:** MID-017, SRC-004

**Learning outcomes** — the engineer can:
1. Allocate an end-to-end latency budget across components and calls.
2. Apply Little's Law to relate throughput, latency, and concurrency (threads, connections, consumers).
3. Explain queueing behavior near saturation and why latency explodes at high utilization.
4. Identify the bottleneck resource from a model and confirm it experimentally.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-005-L01 | Latency budgets | 12 |
| SRC-005-L02 | Little's Law | 12 |
| SRC-005-L03 | Queueing and utilization | 14 |
| SRC-005-L04 | Tail latency and fan-out | 10 |
| SRC-005-L05 | Finding the bottleneck on paper | 10 |
| SRC-005-L06 | Demo: predicting pool sizes with Little's Law, then measuring | 15 |

**Lab** — `SRC-005-LAB1` *Checkout latency budget:* allocate a p99 budget for checkout across services; model required pool and consumer sizes; verify with a load test. Acceptance: model within 20% of measurement or discrepancy explained.

**Common mistakes:** budgets based on averages; ignoring fan-out amplification of tail latency.

**Assessment:** modeling problem set.

**Workplace evidence:** a performance target you set or met using a model rather than trial and error.

**Career relevance:** performance engineering (SRC-016).

---

### SRC-006 · API and data contracts
`n: 180` · **Video:** 69 min · **Practice:** 3.5 h

**Prerequisites:** MID-062

**Learning outcomes** — the engineer can:
1. Define compatibility policies for APIs and events across teams.
2. Assess the consumer impact of a proposed change using contract tests, usage data, and ownership maps.
3. Establish schema governance (ownership, review, registry rules) without blocking teams.
4. Plan multi-team migrations for breaking changes.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-006-L01 | Contracts as promises between teams | 10 |
| SRC-006-L02 | Compatibility policies | 12 |
| SRC-006-L03 | Measuring consumer impact | 10 |
| SRC-006-L04 | Schema governance that scales | 12 |
| SRC-006-L05 | Coordinating breaking changes | 10 |
| SRC-006-L06 | Demo: splitting `OrderPlaced` into two events across five consumers | 15 |

**Lab** — `SRC-006-LAB1` *Contract policy:* write the order domain's API and event compatibility policy and a migration plan for one breaking change. Acceptance: plan names every consumer, the sequence, and the rollback.

**Common mistakes:** governance by meeting; breaking changes discovered in production.

**Assessment:** policy review.

**Workplace evidence:** a breaking change you coordinated across teams.

**Career relevance:** event architecture and API management (ARC-025, ARC-026).

---

### SRC-007 · Database scaling
`n: 181` · **Video:** 104 min · **Practice:** 4.5 h

**Prerequisites:** MID-018, MID-019, SRC-004

**Learning outcomes** — the engineer can:
1. Scale reads with replicas while handling replication lag in application design.
2. Choose between vertical scaling, partitioning, and sharding with evidence.
3. Choose a shard key, predict hot partitions, and plan resharding.
4. Evaluate managed distributed SQL options against operating sharded PostgreSQL.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-007-L01 | The scaling ladder | 10 |
| SRC-007-L02 | Read replicas and lag-aware design | 12 |
| SRC-007-L03 | Partitioning revisited | 8 |
| SRC-007-L04 | Sharding and shard keys | 14 |
| SRC-007-L05 | Hot partitions | 10 |
| SRC-007-L06 | Resharding | 10 |
| SRC-007-L07 | Distributed SQL and managed options | 10 |
| SRC-007-L08 | Demo: choosing a shard key for orders | 15 |
| SRC-007-L09 | Demo: read replicas and the stale-read bug they introduce | 15 |

**Lab** — `SRC-007-LAB1` *Order data at 10×:* decide how the order database reaches the 10× forecast (replicas, partitioning, sharding, or managed distributed SQL) with an ADR and a migration outline. Acceptance: hot-partition risk quantified.

**Common mistakes:** sharding before exhausting simpler options; shard keys that break the most common query.

**Assessment:** shard-key scenarios plus ADR.

**Workplace evidence:** a database scaling change you designed or reviewed.

**Career relevance:** distributed data (SRB-003) and database architecture (ARC-016).

---

### SRC-008 · Architectural decomposition
`n: 182` · **Video:** 92 min · **Practice:** 4 h

**Prerequisites:** MID-061, SRC-003

**Learning outcomes** — the engineer can:
1. Decide between keeping a modular monolith and extracting services using explicit criteria (team topology, change coupling, scaling, fault isolation).
2. Detect coupling from code, data, deployment, and change history.
3. Recommend merging services back when the split costs more than it gives.
4. Outline a migration path and its exit criteria.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-008-L01 | Decomposition is a means, not a goal | 10 |
| SRC-008-L02 | Kinds of coupling | 12 |
| SRC-008-L03 | Evidence from change history | 10 |
| SRC-008-L04 | Team topology and boundaries | 10 |
| SRC-008-L05 | When to merge services back | 10 |
| SRC-008-L06 | Migration criteria and exit conditions | 10 |
| SRC-008-L07 | Demo: mining Git history for change coupling | 15 |
| SRC-008-L08 | Demo: making the case to merge two chatty services | 15 |

**Lab** — `SRC-008-LAB1` *Boundary review:* analyze Shop Platform's service boundaries with change-coupling data and recommend one split and one merge (or justify none). Acceptance: recommendation backed by data and team considerations.

**Common mistakes:** boundaries by noun; ignoring team structure; decomposition without migration plan.

**Assessment:** boundary defense.

**Workplace evidence:** a decomposition or consolidation decision you contributed to, with its outcome.

**Career relevance:** architecture migration (SRB-008) and organizational bottlenecks (SRA-018).

---

### SRC-009 · Failure-mode analysis
`n: 183` · **Video:** 96 min · **Practice:** 4 h

**Prerequisites:** MID-033, SRC-002

**Learning outcomes** — the engineer can:
1. Map dependencies (including hidden ones: DNS, identity, config, shared clusters) and their failure domains.
2. Run a failure-mode and effects analysis (FMEA) with likelihood, impact, and detection.
3. Design graceful degradation so partial failures cost features, not the whole product.
4. Turn findings into failure-injection experiments.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-009-L01 | How real systems fail | 12 |
| SRC-009-L02 | Dependency mapping | 10 |
| SRC-009-L03 | Failure domains and blast radius | 10 |
| SRC-009-L04 | FMEA for software | 14 |
| SRC-009-L05 | Graceful degradation | 10 |
| SRC-009-L06 | From analysis to experiments | 10 |
| SRC-009-L07 | Demo: FMEA of the checkout path | 15 |
| SRC-009-L08 | Demo: a hidden dependency found by failure injection | 15 |

**Lab** — `SRC-009-LAB1` *Order subsystem FMEA:* dependency map, FMEA table, degradation design, and three failure-injection experiments run against the platform. Acceptance: at least one previously unknown weakness found and fixed.

**Common mistakes:** only considering your own services; degradation that silently corrupts data.

**Assessment:** FMEA review.

**Workplace evidence:** a failure-mode review or game day you led.

**Career relevance:** enterprise resilience (SRA-006) and resilience architecture (ARC-031).

---

### SRC-010 · Architecture documentation
`n: 184` · **Video:** 67 min · **Practice:** 3.5 h

**Prerequisites:** MID-063, SRC-008

**Learning outcomes** — the engineer can:
1. Produce an architecture description tailored to its audiences (engineers, operators, leadership).
2. Keep docs close to the code and current (docs-as-code, review on change).
3. Write operational runbooks that a tired on-call engineer can follow.
4. Write a design document that gets a decision in one review.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-010-L01 | Documentation for different readers | 10 |
| SRC-010-L02 | C4 at subsystem scale | 10 |
| SRC-010-L03 | Docs as code | 8 |
| SRC-010-L04 | Runbooks under pressure | 12 |
| SRC-010-L05 | Design docs that get decisions | 12 |
| SRC-010-L06 | Demo: reviewing and rewriting a confusing runbook | 15 |

**Lab** — `SRC-010-LAB1` *Subsystem architecture pack:* architecture description, design doc for the 10× redesign, and runbooks for the top five failure modes from SRC-009. Acceptance: a peer executes a runbook successfully without help.

**Common mistakes:** one document for every audience; runbooks with "investigate" as a step.

**Assessment:** documentation review (COM dimension, higher weight at this level).

**Workplace evidence:** a design doc or runbook used by others without your help.

**Career relevance:** architecture deliverables (ARC-034).
