# MID-P3 — Distributed Systems Foundations

**Phase goal:** the learner decides *whether* to split a system and *where*, then builds services that communicate reliably despite partial failures, and keeps data correct across them.

**Running project:** *Shop Platform* is first restructured as a hexagonal modular monolith, then split along domain boundaries into `catalog`, `orders`, `inventory`, and `payments` services that communicate over HTTP and Kafka. This is the core of the Mid capstone (`MID-CAP`).

**Phase total:** ~18.1 h video · ~45 h practice

> **Ordering change (v1.4):** Architectural styles, DDD, and the microservices introduction (MID-059 to MID-061) were in MID-P6 in the roadmap, after the services had already been split. They now open this phase. IDs are unchanged.
>
> **Teaching note:** Kubernetes arrives in MID-057. Until then, services run with Docker Compose, whose DNS provides the service discovery taught in MID-036.

---

### MID-059 · Architectural styles
`n: 167` · **Video:** 64 min · **Practice:** 3 h

**Prerequisites:** JNR-004, JNR-013

**Learning outcomes** — the learner can:
1. Compare layered, hexagonal (ports and adapters), and clean architecture, and state what each protects.
2. Restructure a layered service so the domain does not depend on frameworks or infrastructure.
3. Design a modular monolith with enforced module boundaries and explicit module APIs.
4. Choose a style for a given team size, domain complexity, and change rate.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-059-L01 | What architecture is for | 8 |
| MID-059-L02 | Layered architecture and its limits | 8 |
| MID-059-L03 | Hexagonal architecture | 14 |
| MID-059-L04 | Clean architecture | 8 |
| MID-059-L05 | The modular monolith | 12 |
| MID-059-L06 | Demo: turning Shop into ports and adapters | 14 |

**Lab** — `MID-059-LAB1` *Hexagonal Shop:* restructure Shop into modules with ports and adapters; ArchUnit tests enforce that the domain has no Spring or JPA imports. Acceptance: the payment adapter can be swapped without touching the domain.

**Common mistakes:** interfaces for everything with no boundary meaning; modules that share database tables freely.

**Assessment:** architecture-style comparison for a scenario.

**Career relevance:** architectural decomposition (SRC-008).

---

### MID-060 · DDD introduction
`n: 168` · **Video:** 70 min · **Practice:** 3 h

**Prerequisites:** JNR-030, MID-059

**Learning outcomes** — the learner can:
1. Distinguish entities and value objects and model each in Java.
2. Design aggregates around invariants and keep them small, referencing other aggregates by ID.
3. Use repositories per aggregate and domain services for logic that spans aggregates.
4. Build a ubiquitous language with domain experts and reflect it in code.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-060-L01 | Why domain-driven design | 8 |
| MID-060-L02 | Ubiquitous language | 8 |
| MID-060-L03 | Entities and value objects | 10 |
| MID-060-L04 | Aggregates and invariants | 14 |
| MID-060-L05 | Repositories and domain services | 8 |
| MID-060-L06 | Domain events | 8 |
| MID-060-L07 | Demo: redesigning the Order aggregate | 14 |

**Lab** — `MID-060-LAB1` *Order aggregate:* redesign `Order` so all invariants (status transitions, line totals, cancellation rules) are enforced inside it and it raises domain events. Acceptance: no invariant enforced in services; unit tests per invariant.

**Common mistakes:** one giant aggregate; anemic models with setter-based "domain"; aggregates holding object references to other aggregates.

**Assessment:** aggregate design for an unseen domain.

**Career relevance:** strategic DDD (SRA-003).

---

### MID-061 · Microservices introduction
`n: 169` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** MID-060

**Learning outcomes** — the learner can:
1. State the benefits of microservices (independent deployment, scaling, ownership) and their costs (network, consistency, operations).
2. Explain why a modular monolith is often the better first step.
3. Apply concrete criteria to decide whether a module should become a service.
4. Recognize a distributed monolith.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-061-L01 | What microservices promise | 8 |
| MID-061-L02 | What they cost | 12 |
| MID-061-L03 | The distributed monolith | 8 |
| MID-061-L04 | Criteria for extracting a service | 10 |
| MID-061-L05 | Demo: walking through the decision for each Shop module | 12 |

**Lab** — `MID-061-LAB1` *Split decision:* decide which Shop modules to extract (if any) and record the decision as an ADR with explicit criteria. Acceptance: ADR reviewed; "not extracting" is an acceptable outcome when justified.

**Common mistakes:** a service per entity; splitting to "scale" without load data.

**Assessment:** ADR review.

**Career relevance:** decomposition decisions (SRC-008) and migrations (SRB-008).

---

### MID-023 · Distributed computing
`n: 131` · **Video:** 62 min · **Practice:** 2 h

**Prerequisites:** BEG-003, JNR-022

**Learning outcomes** — the learner can:
1. List the fallacies of distributed computing and give a failure example for each.
2. Explain partial failure: why a timeout does not tell you whether the operation happened.
3. Explain clock skew and why wall-clock timestamps cannot order events across nodes.
4. Describe crash, omission, and byzantine failure models at a conceptual level.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-023-L01 | The eight fallacies | 12 |
| MID-023-L02 | Latency numbers every engineer should know | 8 |
| MID-023-L03 | Partial failure | 12 |
| MID-023-L04 | Clocks and ordering | 12 |
| MID-023-L05 | Failure models | 6 |
| MID-023-L06 | Demo: injecting latency and packet loss with Toxiproxy | 12 |

**Lab** — `MID-023-LAB1` *Unreliable network:* put Toxiproxy between Shop and its payment provider; observe what happens to orders under latency, timeouts, and dropped responses. Acceptance: list of every inconsistency observed.

**Common mistakes:** treating a timeout as a failure; ordering events by timestamps from different machines.

**Assessment:** failure-scenario quiz.

**Career relevance:** every later distributed-systems module.

---

### MID-024 · Communication models
`n: 132` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** JNR-018, MID-023

**Learning outcomes** — the learner can:
1. Compare synchronous request/response with asynchronous messaging for coupling, latency, and failure.
2. Compare REST and gRPC (contracts, performance, tooling, browser support).
3. Implement a gRPC service and client in Spring.
4. Choose a communication style for each interaction in a system.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-024-L01 | Sync vs async | 10 |
| MID-024-L02 | Temporal coupling | 8 |
| MID-024-L03 | REST vs gRPC | 10 |
| MID-024-L04 | gRPC and Protocol Buffers | 12 |
| MID-024-L05 | Request/reply over messaging | 8 |
| MID-024-L06 | Demo: the same call in REST and gRPC | 12 |

**Lab** — `MID-024-LAB1` *Interaction map:* for each Shop interaction, choose sync or async and justify; implement inventory's stock check as gRPC. Acceptance: interaction map plus working gRPC call.

**Common mistakes:** synchronous call chains five services deep; async used for queries that need an immediate answer.

**Assessment:** interaction-design review.

**Career relevance:** integration patterns (ARC-024).

---

### MID-025 · Service boundaries
`n: 133` · **Video:** 62 min · **Practice:** 3 h

**Prerequisites:** MID-060, MID-061

**Learning outcomes** — the learner can:
1. Identify bounded contexts from language and ownership, not from the database schema.
2. Assign data ownership so each service owns its data exclusively.
3. Replace cross-service joins with APIs, events, or local copies.
4. Evaluate a proposed boundary by coupling and change patterns.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-025-L01 | Bounded contexts | 12 |
| MID-025-L02 | One concept, several models | 8 |
| MID-025-L03 | Data ownership | 10 |
| MID-025-L04 | Life without cross-service joins | 10 |
| MID-025-L05 | Evaluating a boundary | 8 |
| MID-025-L06 | Demo: splitting Shop's shared database | 14 |

**Lab** — `MID-025-LAB1` *Split Shop:* extract `orders`, `inventory`, and `payments` into separate services with separate databases. Acceptance: no service reads another's tables; context map documented.

**Common mistakes:** shared databases between services; boundaries drawn by technical layer.

**Assessment:** boundary review of an unseen system.

**Career relevance:** context mapping (SRA-003) and data ownership strategy (SRA-004).

---

### MID-026 · Messaging fundamentals
`n: 134` · **Video:** 58 min · **Practice:** 2 h

**Prerequisites:** MID-024

**Learning outcomes** — the learner can:
1. Distinguish queues (point-to-point) from topics (publish/subscribe).
2. Distinguish commands from events and name events in the past tense.
3. Explain at-most-once, at-least-once, and effectively-once delivery, and why exactly-once delivery is not available end to end.
4. Design an event payload (identity, timestamp, version, minimal vs full state).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-026-L01 | Why messaging | 8 |
| MID-026-L02 | Queues vs topics | 10 |
| MID-026-L03 | Commands vs events | 8 |
| MID-026-L04 | Delivery semantics | 12 |
| MID-026-L05 | Designing event payloads | 10 |
| MID-026-L06 | Demo: one event, three consumers | 10 |

**Lab** — `MID-026-LAB1` *Event catalog:* define Shop's events (`OrderPlaced`, `StockReserved`, `PaymentAuthorized`, …) with schemas and owners. Acceptance: reviewed catalog used by later labs.

**Common mistakes:** events that are commands in disguise; events carrying entire database rows.

**Assessment:** quiz plus catalog review.

**Career relevance:** event-driven architecture (SRB-002).

---

### MID-027 · RabbitMQ
`n: 135` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** JNR-050, MID-026

**Learning outcomes** — the learner can:
1. Explain exchanges (direct, topic, fanout), bindings, and queues.
2. Publish and consume with Spring AMQP using manual acknowledgments.
3. Configure dead-letter exchanges and retry with delay.
4. Decide between RabbitMQ and Kafka for a workload.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-027-L01 | RabbitMQ's model | 10 |
| MID-027-L02 | Exchanges and routing | 10 |
| MID-027-L03 | Acknowledgments and prefetch | 10 |
| MID-027-L04 | Dead-letter queues and delayed retry | 10 |
| MID-027-L05 | RabbitMQ or Kafka? | 8 |
| MID-027-L06 | Demo: notification routing with a topic exchange | 12 |

**Lab** — `MID-027-LAB1` *Notifications:* email/SMS notification service fed by RabbitMQ with routing keys, retries, and a DLQ. Acceptance: a poison message ends in the DLQ without blocking others.

**Common mistakes:** auto-ack; infinite redelivery loops.

**Assessment:** lab plus tool-choice scenario.

**Career relevance:** enterprise integration (ARC-009).

---

### MID-028 · Apache Kafka
`n: 136` · **Video:** 100 min · **Practice:** 4 h

**Prerequisites:** JNR-050, MID-026

**Learning outcomes** — the learner can:
1. Explain brokers, topics, partitions, replicas, and the log model.
2. Choose partition keys to preserve the ordering that matters.
3. Explain consumer groups, offsets, commits, and rebalancing.
4. Produce and consume with Spring for Apache Kafka, with error handling and a DLT.
5. Configure producer durability (`acks`, idempotent producer).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-028-L01 | Kafka as a distributed log | 10 |
| MID-028-L02 | Topics, partitions, replicas | 12 |
| MID-028-L03 | Keys and ordering | 10 |
| MID-028-L04 | Consumer groups and offsets | 12 |
| MID-028-L05 | Spring for Apache Kafka | 12 |
| MID-028-L06 | Error handling and dead-letter topics | 10 |
| MID-028-L07 | Producer durability settings | 8 |
| MID-028-L08 | Demo: order events end to end | 14 |
| MID-028-L09 | Demo: what a rebalance does to in-flight messages | 12 |

**Lab** — `MID-028-LAB1` *Order events on Kafka:* `orders` publishes `OrderPlaced` keyed by order ID; `inventory` and `payments` consume in separate groups with DLTs. Acceptance: per-order ordering preserved; consumer restart loses nothing.

**Common mistakes:** random keys where order matters; auto-commit before processing; one partition for everything.

**Assessment:** partitioning and ordering scenarios.

**Career relevance:** large-scale messaging (SRB-006).

---

### MID-029 · Reliable messaging
`n: 137` · **Video:** 80 min · **Practice:** 4 h

**Prerequisites:** JNR-031, MID-028

**Learning outcomes** — the learner can:
1. Explain the dual-write problem (database + broker) and its failure modes.
2. Implement the transactional outbox with a relay (polling or CDC).
3. Make consumers idempotent with an inbox/processed-message table or natural idempotency.
4. Design retry policies with backoff and limits, and route permanent failures to a DLQ.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-029-L01 | The dual-write problem | 10 |
| MID-029-L02 | Transactional outbox | 14 |
| MID-029-L03 | Outbox relays: polling vs CDC | 10 |
| MID-029-L04 | Idempotent consumers and the inbox | 12 |
| MID-029-L05 | Retries, backoff, and DLQs | 10 |
| MID-029-L06 | Demo: losing an event without an outbox | 12 |
| MID-029-L07 | Demo: processing the same message twice, safely | 12 |

**Lab** — `MID-029-LAB1` *Reliable order events:* outbox in `orders`, idempotent consumers in `inventory` and `payments`. Acceptance: killing any service at any point never loses or double-applies an event (chaos test script).

**Common mistakes:** publishing inside the DB transaction; deduplication without a durable record.

**Assessment:** failure-injection review.

**Career relevance:** required in the MID capstone; CDC (SRB-007).

---

### MID-030 · Distributed consistency
`n: 138` · **Video:** 52 min · **Practice:** 2 h

**Prerequisites:** MID-023, MID-029

**Learning outcomes** — the learner can:
1. Distinguish strong, eventual, causal, and read-your-writes consistency with examples.
2. Explain CAP and PACELC accurately, including what they do not say.
3. Choose a consistency level per use case and design the user experience for eventual consistency.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-030-L01 | Consistency models | 12 |
| MID-030-L02 | CAP, correctly | 10 |
| MID-030-L03 | PACELC | 8 |
| MID-030-L04 | Designing for eventual consistency | 10 |
| MID-030-L05 | Demo: read-your-writes across services | 12 |

**Lab** — `MID-030-LAB1` *Consistency budget:* for each Shop operation, specify the required consistency and how the UI copes with lag (e.g., "order pending"). Acceptance: reviewed table applied to the API.

**Common mistakes:** "we chose AP" as a system-wide statement; hiding eventual consistency from users.

**Assessment:** scenario quiz.

**Career relevance:** distributed data (SRB-003).

---

### MID-031 · Distributed workflows
`n: 139` · **Video:** 88 min · **Practice:** 4 h

**Prerequisites:** MID-025, MID-029

**Learning outcomes** — the learner can:
1. Model a business process as a saga with local transactions and compensations.
2. Compare choreography and orchestration and choose for a given process.
3. Implement an orchestrated saga with persisted state and timeouts.
4. Design compensations that are idempotent and semantically correct.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-031-L01 | Why distributed transactions don't scale | 10 |
| MID-031-L02 | Sagas | 12 |
| MID-031-L03 | Choreography | 10 |
| MID-031-L04 | Orchestration | 10 |
| MID-031-L05 | Compensation design | 10 |
| MID-031-L06 | Saga state, timeouts, and stuck sagas | 10 |
| MID-031-L07 | Demo: the order saga, happy path | 14 |
| MID-031-L08 | Demo: payment declined, compensations run | 12 |

**Lab** — `MID-031-LAB1` *Order saga:* place order → reserve stock → authorize payment → confirm; payment failure releases stock and cancels the order; timeouts handled. Acceptance: every failure path tested end to end.

**Common mistakes:** compensations that assume the forward step happened; no timeout handling.

**Assessment:** saga design for a new process (returns).

**Career relevance:** required in the MID capstone; orchestration (SRB-001).

---

### MID-032 · Distributed coordination
`n: 140` · **Video:** 48 min · **Practice:** 2 h

**Prerequisites:** MID-030

**Learning outcomes** — the learner can:
1. Explain leases and leader election and when a system needs a single active worker.
2. Explain why a lock held via an expired lease is unsafe and how fencing tokens prevent damage.
3. Implement a single-runner scheduled job across instances (database-based lock, e.g., ShedLock).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-032-L01 | When only one instance may act | 8 |
| MID-032-L02 | Leases and leader election | 10 |
| MID-032-L03 | Distributed locks and their limits | 10 |
| MID-032-L04 | Fencing tokens | 8 |
| MID-032-L05 | Demo: a nightly job running once across three replicas | 12 |

**Lab** — `MID-032-LAB1` *Single runner:* the nightly reconciliation job runs exactly once across replicas, and its writes are fenced. Acceptance: test with a paused instance does not double-apply.

**Common mistakes:** trusting a Redis lock for correctness; no fencing.

**Assessment:** quiz.

**Career relevance:** consensus concepts (SRB-003).

---

### MID-033 · Resilience
`n: 141` · **Video:** 82 min · **Practice:** 3 h

**Prerequisites:** JNR-022, MID-024

**Learning outcomes** — the learner can:
1. Set timeouts on every remote call from a latency budget.
2. Retry with exponential backoff and jitter, only for idempotent, transient failures.
3. Apply circuit breakers and bulkheads with Resilience4j.
4. Design fallbacks and graceful degradation that are honest to the user.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-033-L01 | How failures cascade | 10 |
| MID-033-L02 | Timeouts and latency budgets | 10 |
| MID-033-L03 | Retries, backoff, and jitter | 10 |
| MID-033-L04 | Circuit breakers | 10 |
| MID-033-L05 | Bulkheads | 8 |
| MID-033-L06 | Fallbacks and degradation | 8 |
| MID-033-L07 | Demo: a cascading failure, then the fix | 14 |
| MID-033-L08 | Demo: retry storms and jitter | 12 |

**Lab** — `MID-033-LAB1` *Resilient checkout:* protect calls to `payments` and `inventory` with timeouts, retries, circuit breakers, and bulkheads; degrade product pages when reviews are down. Acceptance: Toxiproxy experiments show contained failures.

**Common mistakes:** retries without timeouts; retrying non-idempotent POSTs; circuit breakers never tested.

**Assessment:** resilience design review.

**Career relevance:** failure-mode analysis (SRC-009) and high-availability design (SRB-005).

---

### MID-034 · Rate limiting
`n: 142` · **Video:** 52 min · **Practice:** 2 h

**Prerequisites:** MID-033

**Learning outcomes** — the learner can:
1. Explain token bucket, leaky bucket, and window algorithms.
2. Implement per-client rate limiting with correct `429` responses and `Retry-After`.
3. Distinguish rate limits, quotas, and load shedding.
4. Behave well as a client of a rate-limited API.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-034-L01 | Why limit | 6 |
| MID-034-L02 | Token and leaky buckets | 10 |
| MID-034-L03 | Distributed rate limiting | 10 |
| MID-034-L04 | Quotas and load shedding | 8 |
| MID-034-L05 | Being a good client | 6 |
| MID-034-L06 | Demo: per-customer limits at the edge | 12 |

**Lab** — `MID-034-LAB1` *Fair use:* per-customer and per-IP limits on search and checkout. Acceptance: load test shows one abusive client cannot degrade others.

**Common mistakes:** in-memory limits behind a load balancer; no `Retry-After`.

**Assessment:** quiz plus lab.

**Career relevance:** abuse prevention (MID-052) and API management (ARC-025).

---

### MID-035 · API gateways
`n: 143` · **Video:** 56 min · **Practice:** 2.5 h

**Prerequisites:** JNR-039, MID-024

**Learning outcomes** — the learner can:
1. Describe gateway responsibilities: routing, TLS termination, authentication, rate limiting, request shaping.
2. Configure Spring Cloud Gateway (or an equivalent) in front of Shop's services.
3. Decide what belongs in the gateway vs in services, and avoid business logic at the edge.
4. Explain the backend-for-frontend pattern.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-035-L01 | Why a gateway | 8 |
| MID-035-L02 | Routing and filters | 10 |
| MID-035-L03 | Authentication at the edge | 10 |
| MID-035-L04 | What not to put in a gateway | 8 |
| MID-035-L05 | Backend for frontend | 8 |
| MID-035-L06 | Demo: one entry point for four services | 12 |

**Lab** — `MID-035-LAB1` *Shop gateway:* a single public entry point validating tokens, routing to services, and applying rate limits. Acceptance: services are not reachable directly from outside.

**Common mistakes:** gateway as a new monolith; services trusting any request with no token.

**Assessment:** responsibility-placement exercise.

**Career relevance:** API management (ARC-025).

---

### MID-036 · Service discovery
`n: 144` · **Video:** 42 min · **Practice:** 1.5 h

**Prerequisites:** JNR-049, MID-035

**Learning outcomes** — the learner can:
1. Explain client-side vs server-side discovery and load balancing.
2. Use DNS-based discovery (Docker Compose now, Kubernetes Services in MID-057).
3. Explain health-check-driven routing and what happens to in-flight requests during deployment.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-036-L01 | Finding services | 8 |
| MID-036-L02 | DNS-based discovery | 8 |
| MID-036-L03 | Platform-native discovery | 8 |
| MID-036-L04 | Load-balancing strategies | 8 |
| MID-036-L05 | Demo: scaling inventory to three replicas | 10 |

**Lab** — `MID-036-LAB1` *Scale out:* run three `inventory` replicas behind Compose DNS; kill one during a load test. Acceptance: errors limited to in-flight requests; explanation of why.

**Common mistakes:** hard-coded hosts; service registries added where the platform already provides discovery.

**Assessment:** quiz.

**Career relevance:** Kubernetes Services (MID-057) and service mesh (SRB-009).
