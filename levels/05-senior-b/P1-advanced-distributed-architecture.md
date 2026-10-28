# SRB-P1 — Advanced Distributed Architecture

**Phase goal:** the engineer chooses among advanced distributed patterns with a clear view of their costs, designs systems that survive regional failure and scale-out messaging, and plans safe architectural migrations across teams.

**Running case:** *The FulfillCo integration.* The company behind Shop Platform has acquired FulfillCo, whose warehouse and fulfillment system is a 10-year-old Java modular monolith on one PostgreSQL database, exchanging nightly CSV files with partners. Four teams (Shop orders, FulfillCo warehouse, FulfillCo shipping, Platform) must integrate the two systems in real time and extract selected FulfillCo capabilities into services — without stopping either business. Every lab advances the Senior B capstone (`SRB-CAP`).

**Format:** case studies, worked design sessions, and multi-team role-play. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~16.4 h video · ~42 h practice

---

### SRB-001 · Distributed architecture patterns
`n: 195` · **Video:** 100 min · **Practice:** 4.5 h

**Prerequisites:** MID-022, MID-031

**Learning outcomes** — the engineer can:
1. Apply full CQRS with separate write and read models, and say when CQRS-lite is enough.
2. Explain event sourcing (event store, projections, snapshots, upcasting) and its operational costs.
3. Build materialized views across service boundaries and manage their staleness.
4. Choose between orchestration engines (e.g., Temporal, Camunda) and hand-built sagas.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-001-L01 | Patterns as trade-offs, not upgrades | 10 |
| SRB-001-L02 | CQRS in full | 12 |
| SRB-001-L03 | Event sourcing | 14 |
| SRB-001-L04 | Projections, snapshots, and upcasting | 12 |
| SRB-001-L05 | Materialized views across services | 10 |
| SRB-001-L06 | Workflow engines vs hand-built sagas | 12 |
| SRB-001-L07 | Demo: modeling shipment tracking with and without event sourcing | 15 |
| SRB-001-L08 | Demo: rebuilding a broken projection from the event store | 15 |

**Lab** — `SRB-001-LAB1` *Shipment tracking design:* design FulfillCo's shipment tracking with two candidate patterns (event-sourced vs state + outbox) and decide in an ADR. Acceptance: operational costs (replay time, schema evolution, storage) estimated for both.

**Common mistakes:** event sourcing everything; projections nobody can rebuild; workflow engines adopted for one saga.

**Assessment:** pattern-selection defense.

**Workplace evidence:** a design where you chose a simpler pattern over a fashionable one and could show why.

**Career relevance:** architecture at scale (SRA-001).

---

### SRB-002 · Event-driven architecture
`n: 196` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** MID-062, SRB-001

**Learning outcomes** — the engineer can:
1. Design event contracts (notification vs state transfer vs domain events) for consumers in other teams.
2. Assign event ownership and publish an event catalog.
3. Evolve schemas across teams with compatibility rules and versioned topics.
4. Plan replay and backfill of events safely, including for consumers with side effects.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-002-L01 | Event-driven architecture at organization scale | 10 |
| SRB-002-L02 | Kinds of events and when to use each | 12 |
| SRB-002-L03 | Ownership and event catalogs | 10 |
| SRB-002-L04 | Schema evolution across teams | 12 |
| SRB-002-L05 | Replay and backfill | 12 |
| SRB-002-L06 | Demo: designing the Shop ↔ FulfillCo event contract | 15 |
| SRB-002-L07 | Demo: a replay that would have resent 40,000 emails, and the fix | 15 |

**Lab** — `SRB-002-LAB1` *Integration events:* event catalog between Shop and FulfillCo (`OrderReadyForFulfillment`, `ShipmentDispatched`, …) with owners, schemas, and replay rules. Acceptance: reviewed by two role-played consuming teams.

**Common mistakes:** leaking internal models as events; replays that resend customer emails.

**Assessment:** contract review.

**Workplace evidence:** an event contract you designed that another team consumes.

**Career relevance:** event architecture (ARC-026).

---

### SRB-003 · Distributed data
`n: 197` · **Video:** 86 min · **Practice:** 3.5 h

**Prerequisites:** MID-030, MID-032, SRC-007

**Learning outcomes** — the engineer can:
1. Explain leader-based, multi-leader, and leaderless replication and their failure behavior.
2. Explain consensus (Raft) at the level needed to evaluate systems that use it (etcd, Kafka KRaft, distributed SQL).
3. Reason about quorums and tunable consistency.
4. Evaluate a datastore's consistency claims against published analyses (e.g., Jepsen).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-003-L01 | Replication strategies | 12 |
| SRB-003-L02 | Consensus and Raft | 14 |
| SRB-003-L03 | Quorums | 10 |
| SRB-003-L04 | Consistency models, revisited | 10 |
| SRB-003-L05 | Reading a Jepsen report | 10 |
| SRB-003-L06 | Demo: partitioning a three-node cluster and watching it choose | 15 |
| SRB-003-L07 | Demo: a quorum read returning stale data, explained | 15 |

**Lab** — `SRB-003-LAB1` *Datastore evaluation:* evaluate two candidate datastores for FulfillCo's stock ledger by their replication and consistency behavior under partition. Acceptance: claims backed by documentation, Jepsen findings, or experiment.

**Common mistakes:** trusting marketing consistency claims; quorum math without failure scenarios.

**Assessment:** scenario quiz.

**Workplace evidence:** a datastore decision you informed with consistency analysis.

**Career relevance:** multi-region trade-offs (SRA-005).

---

### SRB-004 · Multi-region systems
`n: 198` · **Video:** 94 min · **Practice:** 4 h

**Prerequisites:** SRC-013, SRB-003

**Learning outcomes** — the engineer can:
1. Compare active-passive and active-active designs by cost, complexity, RPO/RTO, and consistency.
2. Design traffic routing and failover (DNS, global load balancers, health-based routing).
3. Handle data residency requirements per region.
4. Decide which parts of a system need to be multi-region and which do not.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-004-L01 | Why go multi-region | 10 |
| SRB-004-L02 | Active-passive | 12 |
| SRB-004-L03 | Active-active and conflict handling | 14 |
| SRB-004-L04 | Global traffic routing | 10 |
| SRB-004-L05 | Data residency | 10 |
| SRB-004-L06 | Selective multi-region | 8 |
| SRB-004-L07 | Demo: regional failover of the order path, step by step | 15 |
| SRB-004-L08 | Demo: the hidden single-region dependency that breaks failover | 15 |

**Lab** — `SRB-004-LAB1` *EU expansion:* FulfillCo opens EU warehouses with EU data residency; design the regional topology for Shop + FulfillCo. Acceptance: residency enforced by design; cost delta estimated.

**Common mistakes:** active-active by default; forgetting regional dependencies (identity, secrets, CI).

**Assessment:** topology review.

**Workplace evidence:** a multi-region or residency design you contributed to.

**Career relevance:** HA and DR architecture (ARC-019) and compliance (ARC-029).

---

### SRB-005 · High-availability design
`n: 199` · **Video:** 86 min · **Practice:** 3.5 h

**Prerequisites:** SRC-009, SRB-004

**Learning outcomes** — the engineer can:
1. Design redundancy at every layer and remove hidden single points of failure.
2. Apply load shedding, admission control, and prioritization under overload.
3. Contain faults with cells, shuffle sharding, and bulkheads at the infrastructure level.
4. Compute composite availability and explain why dependencies cap it.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-005-L01 | Availability math | 12 |
| SRB-005-L02 | Redundancy and hidden SPOFs | 10 |
| SRB-005-L03 | Load shedding and admission control | 12 |
| SRB-005-L04 | Cell-based architecture | 12 |
| SRB-005-L05 | Shuffle sharding | 10 |
| SRB-005-L06 | Demo: shedding low-priority traffic during a flash sale | 15 |
| SRB-005-L07 | Demo: computing checkout's real availability from its dependencies | 15 |

**Lab** — `SRB-005-LAB1` *Availability budget:* compute the composite availability of checkout including FulfillCo dependencies; redesign to meet 99.95% with shedding and fault containment. Acceptance: math shown; load-shedding experiment run.

**Common mistakes:** multiplying nines without dependency analysis; shedding that drops paying customers first.

**Assessment:** availability calculation problems.

**Workplace evidence:** an availability improvement you designed with before/after numbers.

**Career relevance:** enterprise resilience (SRA-006).

---

### SRB-006 · Large-scale messaging
`n: 200` · **Video:** 92 min · **Practice:** 3.5 h

**Prerequisites:** MID-028, SRC-005

**Learning outcomes** — the engineer can:
1. Choose partition counts and keys for throughput, ordering, and future growth.
2. Monitor and act on consumer lag with clear thresholds.
3. Minimize rebalancing impact (cooperative rebalancing, static membership).
4. Apply backpressure end to end so producers cannot overwhelm consumers.
5. Plan Kafka cluster capacity, retention, and multi-tenant topic governance.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-006-L01 | Messaging at scale | 8 |
| SRB-006-L02 | Partition strategy | 12 |
| SRB-006-L03 | Consumer lag | 10 |
| SRB-006-L04 | Rebalancing | 10 |
| SRB-006-L05 | Backpressure end to end | 12 |
| SRB-006-L06 | Cluster capacity and governance | 10 |
| SRB-006-L07 | Demo: recovering from a six-hour consumer backlog | 15 |
| SRB-006-L08 | Demo: choosing partition counts for three years of growth | 15 |

**Lab** — `SRB-006-LAB1` *Partner feed at scale:* design topics and consumers for FulfillCo's partner tracking feed (50× Shop's order volume) with lag alerts and a backlog-recovery plan. Acceptance: load test proves catch-up time within target.

**Common mistakes:** partition counts chosen for today; lag alerts without action plans.

**Assessment:** design review.

**Workplace evidence:** a messaging scale problem you diagnosed or prevented.

**Career relevance:** platform strategy (STF-004).

---

### SRB-007 · Data platform integration
`n: 201` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** MID-029, SRB-002

**Learning outcomes** — the engineer can:
1. Capture changes from a legacy database with CDC (Debezium) without changing its code.
2. Distinguish CDC events from domain events and translate between them.
3. Build stream processing for enrichment and aggregation (Kafka Streams or Flink concepts).
4. Feed analytics pipelines while respecting data ownership and privacy.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-007-L01 | Integrating systems you can't change | 10 |
| SRB-007-L02 | Change data capture with Debezium | 14 |
| SRB-007-L03 | From CDC events to domain events | 10 |
| SRB-007-L04 | Stream processing concepts | 12 |
| SRB-007-L05 | Analytics pipelines and data ownership | 10 |
| SRB-007-L06 | Demo: streaming FulfillCo's stock table without touching its code | 15 |
| SRB-007-L07 | Demo: filtering personal data out of a CDC stream | 15 |

**Lab** — `SRB-007-LAB1` *Stock sync:* Debezium on FulfillCo's database, translated into a `StockLevelChanged` domain event consumed by Shop's inventory. Acceptance: Shop sees stock changes within seconds; FulfillCo code unchanged.

**Common mistakes:** exposing raw table changes as a public contract; CDC on tables with personal data without filtering.

**Assessment:** integration design review.

**Workplace evidence:** a legacy integration you delivered with CDC or a similar technique.

**Career relevance:** integration patterns (ARC-024) and data architecture (ARC-023).

---

### SRB-008 · Architecture migration
`n: 202` · **Video:** 94 min · **Practice:** 4.5 h

**Prerequisites:** SRC-008, SRB-007

**Learning outcomes** — the engineer can:
1. Apply the strangler fig pattern with routing at the edge and incremental capability extraction.
2. Use branch by abstraction inside the legacy codebase.
3. Explain dual-write risks and replace them with CDC, outbox, or a single writer.
4. Plan data migration for an extracted service, including the cut-over of ownership.
5. Define per-step rollback and measurable exit criteria.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-008-L01 | Why big-bang rewrites fail | 10 |
| SRB-008-L02 | The strangler fig | 12 |
| SRB-008-L03 | Branch by abstraction | 10 |
| SRB-008-L04 | Dual writes and their alternatives | 12 |
| SRB-008-L05 | Moving data ownership | 12 |
| SRB-008-L06 | Rollback and exit criteria | 8 |
| SRB-008-L07 | Demo: extracting shipment tracking from the FulfillCo monolith | 15 |
| SRB-008-L08 | Demo: catching a dual-write inconsistency in production data | 15 |

**Lab** — `SRB-008-LAB1` *Migration plan:* a phased plan to extract shipment tracking and carrier integration from the FulfillCo monolith, with routing, data migration, rollback per phase, and success metrics. Acceptance: no phase requires both systems to write the same data.

**Common mistakes:** extracting the hardest piece first; no plan for retiring legacy code paths; dual writes "just for a while".

**Assessment:** migration plan defense.

**Workplace evidence:** a strangler or extraction step you led into production.

**Career relevance:** legacy modernization (ARC-010) and migration strategy (ARC-037).

---

### SRB-009 · Service mesh
`n: 203` · **Video:** 90 min · **Practice:** 3 h

**Prerequisites:** MID-051, MID-057

**Learning outcomes** — the engineer can:
1. Explain what a service mesh provides (mTLS, traffic management, telemetry, policy) and how sidecar and sidecar-less meshes differ.
2. Configure mTLS and traffic splitting for a canary.
3. Decide whether a mesh is worth its operational cost compared with library-based alternatives.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-009-L01 | What a mesh does | 10 |
| SRB-009-L02 | Mesh architectures | 10 |
| SRB-009-L03 | mTLS and workload identity | 12 |
| SRB-009-L04 | Traffic management | 10 |
| SRB-009-L05 | Policy enforcement | 8 |
| SRB-009-L06 | The cost of a mesh | 10 |
| SRB-009-L07 | Demo: canary traffic split and mTLS with a mesh | 15 |
| SRB-009-L08 | Demo: measuring a mesh's latency and operational overhead | 15 |

**Lab** — `SRB-009-LAB1` *Mesh decision:* trial a mesh on a subset of services; record operational effort, latency overhead, and benefits; write the adopt/reject ADR. Acceptance: decision supported by measurements.

**Common mistakes:** adopting a mesh to fix problems of process; duplicate retries in mesh and code.

**Assessment:** ADR defense.

**Workplace evidence:** a platform technology adoption or rejection you led with evidence.

**Career relevance:** security architecture (SRB-016) and platform strategy (STF-004).

---

### SRB-010 · Platform engineering
`n: 204` · **Video:** 84 min · **Practice:** 3.5 h

**Prerequisites:** MID-055, MID-057

**Learning outcomes** — the engineer can:
1. Explain internal developer platforms, golden paths, and the platform-as-a-product mindset.
2. Identify repeated toil across teams that a platform capability should remove.
3. Design a self-service capability with sensible defaults and escape hatches.
4. Measure platform adoption and developer satisfaction.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-010-L01 | Why platform teams exist | 10 |
| SRB-010-L02 | Platform as a product | 12 |
| SRB-010-L03 | Golden paths | 10 |
| SRB-010-L04 | Self-service with guardrails | 12 |
| SRB-010-L05 | Measuring a platform | 10 |
| SRB-010-L06 | Demo: a service template that ships with CI, telemetry, and SLOs | 15 |
| SRB-010-L07 | Demo: interviewing teams to find the platform's first capability | 15 |

**Lab** — `SRB-010-LAB1` *Golden path for FulfillCo:* a service template and pipeline that new FulfillCo services use, with telemetry, security scans, and deployment pre-wired. Acceptance: a new service reaches staging in under one hour using the template.

**Common mistakes:** mandates instead of paved roads; platforms built without talking to users.

**Assessment:** platform capability proposal.

**Workplace evidence:** a reusable capability other teams adopted.

**Career relevance:** the Staff capstone (STF-CAP) builds on this.

---

### SRB-021 · AI platform capabilities
`n: new (added in v2.0)` · **Video:** 88 min · **Practice:** 4 h

**Prerequisites:** SRB-010, SRC-021

**Learning outcomes** — the engineer can:
1. Design a shared LLM gateway: authentication, per-team quotas, redaction of sensitive data, logging, cost attribution, and model routing.
2. Offer shared retrieval services (embedding, indexing, search) with clear data ownership per team.
3. Build an AI golden path: template, evaluation harness, observability, and security checks pre-wired.
4. Decide which AI capabilities to centralize and which to leave to product teams.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRB-021-L01 | Why AI needs platform support | 10 |
| SRB-021-L02 | The LLM gateway | 14 |
| SRB-021-L03 | Quotas, redaction, and cost attribution | 12 |
| SRB-021-L04 | Shared retrieval services and data ownership | 12 |
| SRB-021-L05 | An AI golden path | 10 |
| SRB-021-L06 | Demo: four teams, one gateway, one cost report | 15 |
| SRB-021-L07 | Demo: redacting customer data before it reaches a model | 15 |

**Lab** — `SRB-021-LAB1` *FulfillCo LLM gateway:* design and prototype a gateway used by all four teams, with per-team quotas, redaction, request logging, and cost attribution; write the AI golden path. Acceptance: one team's runaway usage cannot exhaust another's quota; cost per team reported; no unredacted personal data in logs.

**Common mistakes:** every team holding its own provider keys; logging full prompts with customer data; centralizing prompt design that belongs to product teams.

**Assessment:** platform capability review.

**Workplace evidence:** a shared AI capability other teams adopted.

**Career relevance:** AI strategy (SRA-021) and AI governance (STF-021).
