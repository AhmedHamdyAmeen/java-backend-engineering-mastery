# MID-P5 — Production Engineering and Security

**Phase goal:** the learner runs Shop Platform like a production system: it is tested across service contracts and under load, observable end to end, held to SLOs, secured against API threats, delivered through gated pipelines, and deployed on Kubernetes in the cloud with infrastructure as code.

**Running project:** *Shop Platform* on Kubernetes with OpenTelemetry tracing, Prometheus/Grafana dashboards, SLO alerts, and Terraform-managed infrastructure.

**Phase total:** ~18.9 h video · ~47 h practice

> **Cloud note:** labs are written for one provider (AWS or Azure, per the pending baseline decision in `CONVENTIONS.md`). A local Kubernetes cluster (kind or k3d) covers everything except MID-056 and MID-058 for learners without a cloud account.

---

### MID-069 · Tool calling and agents
`n: new (added in v2.0)` · **Video:** 80 min · **Practice:** 3.5 h · `version:` tool-calling APIs and the Model Context Protocol evolve quickly — verify before recording

**Prerequisites:** MID-033, MID-068

**Learning outcomes** — the learner can:
1. Explain how tool (function) calling works: the model proposes a call, the application decides whether and how to execute it.
2. Design tools with narrow scope, typed parameters, idempotency, and clear error results.
3. Enforce authorization on every tool call using the end user's identity, never the model's judgment.
4. Require human approval for tools with side effects (refunds, cancellations) and bound agent loops with step, time, and cost limits.
5. Describe the Model Context Protocol (MCP) as a standard way to expose tools and data to models, and when it is worth adopting.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-069-L01 | From answering to acting | 8 |
| MID-069-L02 | How tool calling works | 12 |
| MID-069-L03 | Designing safe tools | 10 |
| MID-069-L04 | Authorization and identity for tool calls | 10 |
| MID-069-L05 | Side effects, idempotency, and human approval | 8 |
| MID-069-L06 | Agent loops and their limits; MCP as a concept | 7 |
| MID-069-L07 | Demo: an order-status tool that respects ownership | 12 |
| MID-069-L08 | Demo: a refund request routed to human approval | 13 |

**Lab** — `MID-069-LAB1` *Assistant with tools:* give the order-support assistant read-only tools (order status, shipment tracking) that call Shop Platform services with the customer's token, and a "request refund" tool that only creates a pending request for a human agent. Acceptance: a customer can never see another customer's order through the assistant (test); no tool with side effects executes without approval; loops stop at the configured step and cost limits.

**Common mistakes:** tools that run with a service account and bypass ownership checks; letting the model decide whether an action is allowed; non-idempotent tools retried by the agent loop; unbounded loops.

**Assessment:** tool-design review — find authorization, idempotency, and approval gaps in a provided tool set.

**Career relevance:** agentic features at Senior levels (SRC-021) and the AI platform's tool governance (SRB-021).

---

### MID-045 · Advanced testing
`n: 153` · **Video:** 64 min · **Practice:** 3 h

**Prerequisites:** JNR-046, MID-029

**Learning outcomes** — the learner can:
1. Explain why end-to-end tests across many services are slow and brittle.
2. Write consumer-driven contract tests for HTTP and messaging (Pact or Spring Cloud Contract).
3. Verify provider contracts in CI and block breaking changes.
4. Write property-based tests (jqwik) for domain invariants.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-045-L01 | Testing distributed systems | 10 |
| MID-045-L02 | Consumer-driven contracts | 12 |
| MID-045-L03 | Contracts for messages | 10 |
| MID-045-L04 | Contracts in CI | 8 |
| MID-045-L05 | Property-based testing | 12 |
| MID-045-L06 | Demo: a breaking API change caught by a contract | 12 |

**Lab** — `MID-045-LAB1` *Contracts for Shop:* contracts between `orders` and `inventory` (HTTP) and for `OrderPlaced` (Kafka), verified in both pipelines; property tests for the Order aggregate. Acceptance: renaming a field fails the provider build.

**Common mistakes:** contracts written by the provider alone; asserting entire payloads.

**Assessment:** lab plus test-strategy question.

**Career relevance:** API evolution (MID-062) and quality strategy at Staff level.

---

### MID-046 · Performance testing
`n: 154` · **Video:** 64 min · **Practice:** 3 h

**Prerequisites:** MID-008, MID-017

**Learning outcomes** — the learner can:
1. Distinguish load, stress, spike, and soak tests and what each reveals.
2. Write k6 (or Gatling) scenarios with realistic traffic mixes and think time.
3. Report latency percentiles and throughput, and avoid coordinated omission.
4. Correlate test results with profiles and metrics to find the bottleneck.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-046-L01 | Kinds of performance tests | 10 |
| MID-046-L02 | Writing k6 scenarios | 12 |
| MID-046-L03 | Workload models | 10 |
| MID-046-L04 | Percentiles and coordinated omission | 10 |
| MID-046-L05 | From test result to bottleneck | 10 |
| MID-046-L06 | Demo: a soak test that finds a slow leak | 12 |

**Lab** — `MID-046-LAB1` *Shop under load:* load, spike, and 2-hour soak tests of checkout with a report naming the first bottleneck. Acceptance: report with percentiles, graphs, and evidence.

**Common mistakes:** averages instead of percentiles; testing from the same machine; unrealistic data sets.

**Assessment:** report review.

**Career relevance:** capacity planning (SRC-004) and the MID gate.

---

### MID-047 · Observability
`n: 155` · **Video:** 94 min · **Practice:** 3.5 h

**Prerequisites:** JNR-006, MID-031

**Learning outcomes** — the learner can:
1. Explain the roles of logs, metrics, and traces and the questions each answers.
2. Instrument services with OpenTelemetry (auto and manual spans) and propagate context over HTTP and Kafka.
3. Correlate logs with traces through trace and span IDs.
4. Add business-meaningful custom metrics with Micrometer.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-047-L01 | Monitoring vs observability | 8 |
| MID-047-L02 | Logs, metrics, traces | 10 |
| MID-047-L03 | OpenTelemetry concepts | 12 |
| MID-047-L04 | Instrumenting Spring services | 12 |
| MID-047-L05 | Context propagation through Kafka | 10 |
| MID-047-L06 | Correlating logs and traces | 8 |
| MID-047-L07 | Custom metrics with Micrometer | 8 |
| MID-047-L08 | Demo: following one order through four services | 14 |
| MID-047-L09 | Demo: finding a slow span in a saga | 12 |

**Lab** — `MID-047-LAB1` *Traceable Shop:* traces across gateway, services, and Kafka visualized in Jaeger/Tempo; logs carry trace IDs; business metrics for orders placed and failed. Acceptance: any order ID can be traced end to end.

**Common mistakes:** high-cardinality metric labels; traces broken at the message broker; logging instead of metrics for counts.

**Assessment:** diagnose an issue from telemetry alone.

**Career relevance:** incident handling (MID-050) and the MID gate.

---

### MID-048 · Monitoring
`n: 156` · **Video:** 54 min · **Practice:** 2.5 h

**Prerequisites:** MID-047

**Learning outcomes** — the learner can:
1. Scrape metrics with Prometheus and write PromQL for rates, ratios, and percentiles.
2. Build Grafana dashboards using the RED and USE methods.
3. Write alerts on symptoms rather than causes, with clear runbook links.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-048-L01 | Prometheus model | 10 |
| MID-048-L02 | PromQL essentials | 12 |
| MID-048-L03 | Dashboards: RED and USE | 10 |
| MID-048-L04 | Alerting that people trust | 10 |
| MID-048-L05 | Demo: a service dashboard from scratch | 12 |

**Lab** — `MID-048-LAB1` *Shop dashboards:* one dashboard per service plus a business overview; alerts for error rate and latency with runbooks. Acceptance: a fault injected by the instructor triggers exactly one actionable alert.

**Common mistakes:** alerting on CPU; dashboards nobody reads; alerts without runbooks.

**Assessment:** dashboard and alert review.

**Career relevance:** SLO engineering (SRC-012).

---

### MID-070 · LLM evaluation and observability
`n: new (added in v2.0)` · **Video:** 67 min · **Practice:** 3 h

**Prerequisites:** MID-047, MID-068

**Learning outcomes** — the learner can:
1. Build an evaluation set of realistic questions with expected sources and acceptance criteria.
2. Measure retrieval recall, answer groundedness (faithfulness to sources), and refusal correctness.
3. Use an LLM as a judge with calibration against human-labeled samples, and state its limits.
4. Run evaluations in CI so prompt, model, or retrieval changes cannot silently degrade quality.
5. Trace each request with token counts, latency per step, model version, and cost, and build dashboards and alerts on them.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-070-L01 | Why LLM features need evaluations | 8 |
| MID-070-L02 | Building an evaluation set | 10 |
| MID-070-L03 | Metrics: recall, groundedness, refusals | 10 |
| MID-070-L04 | LLM-as-judge and its caveats | 8 |
| MID-070-L05 | Evaluations in CI | 8 |
| MID-070-L06 | Tracing tokens, latency, and cost | 10 |
| MID-070-L07 | Demo: an evaluation run catching a prompt regression | 13 |

**Lab** — `MID-070-LAB1` *Measured assistant:* a 50-question evaluation set for the order-support assistant run in CI with pass thresholds; OpenTelemetry spans for retrieval, model call, and tools with token and cost attributes; a Grafana dashboard for cost per conversation and p95 latency. Acceptance: a deliberately worse prompt fails the pipeline; cost per conversation is visible per day.

**Common mistakes:** evaluating with five hand-picked questions; trusting an uncalibrated judge model; no record of which prompt and model version produced an answer; cost discovered on the monthly invoice.

**Assessment:** design an evaluation plan for a new AI feature, including thresholds and what blocks a release.

**Career relevance:** evaluation-gated releases (SRC-022) and AI vendor and model evaluation (ARC-047).

---

### MID-049 · Reliability
`n: 157` · **Video:** 60 min · **Practice:** 2 h

**Prerequisites:** MID-048

**Learning outcomes** — the learner can:
1. Define SLIs that reflect user experience (availability, latency percentiles, correctness).
2. Set SLOs and compute error budgets.
3. Alert on error-budget burn rate.
4. Explain how error budgets guide release and reliability decisions.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-049-L01 | What reliability means to users | 8 |
| MID-049-L02 | SLIs | 10 |
| MID-049-L03 | SLOs and error budgets | 12 |
| MID-049-L04 | Burn-rate alerts | 10 |
| MID-049-L05 | Using the budget | 8 |
| MID-049-L06 | Demo: SLO dashboard and burn-rate alert for checkout | 12 |

**Lab** — `MID-049-LAB1` *Checkout SLOs:* define SLIs/SLOs for checkout and search with burn-rate alerts. Acceptance: SLO document reviewed; alerts tested with injected errors.

**Common mistakes:** 100% targets; SLIs measured at the server rather than as users experience them.

**Assessment:** SLO document review.

**Career relevance:** SLO engineering (SRC-012).

---

### MID-050 · Incident handling
`n: 158` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** JNR-054, MID-049

**Learning outcomes** — the learner can:
1. Triage an incident: assess impact, set severity, and escalate.
2. Prioritize mitigation (rollback, feature flag, scale) over root-cause analysis during the incident.
3. Keep an incident timeline and communicate status updates.
4. Write a blameless postmortem with contributing factors and tracked action items.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-050-L01 | Anatomy of an incident | 8 |
| MID-050-L02 | Triage and severity | 10 |
| MID-050-L03 | Mitigate first | 10 |
| MID-050-L04 | Roles and communication | 8 |
| MID-050-L05 | Blameless postmortems | 10 |
| MID-050-L06 | Demo: a simulated incident, start to finish | 14 |

**Lab** — `MID-050-LAB1` *Game day:* the instructor breaks Shop Platform during a load test; the learner acts as incident responder, then writes the postmortem. Acceptance: mitigation within the time box; postmortem reviewed.

**Common mistakes:** debugging root cause while users are down; postmortems that name a person.

**Assessment:** the MID graduation gate's incident simulation uses this format.

**Career relevance:** incident leadership (SRC-019).

---

### MID-051 · Advanced API security
`n: 159` · **Video:** 54 min · **Practice:** 2.5 h

**Prerequisites:** JNR-039, MID-035

**Learning outcomes** — the learner can:
1. Choose OAuth 2.0 flows for user-facing, machine-to-machine, and delegated scenarios.
2. Validate tokens fully at every service, not only at the gateway.
3. Design scopes and claims for fine-grained authorization, and propagate user identity between services.
4. Apply token exchange or client credentials for service-to-service calls.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-051-L01 | OAuth flows revisited | 10 |
| MID-051-L02 | Token validation everywhere | 10 |
| MID-051-L03 | Scopes, claims, and authorization design | 12 |
| MID-051-L04 | Service-to-service identity | 10 |
| MID-051-L05 | Demo: propagating identity from gateway to inventory | 12 |

**Lab** — `MID-051-LAB1` *Zero implicit trust:* every Shop service validates tokens; `orders` calls `inventory` with its own client credentials; scopes restrict admin operations. Acceptance: a direct call without a valid token fails at every service.

**Common mistakes:** trusting a header set by the gateway; one all-powerful service account.

**Assessment:** authorization design review.

**Career relevance:** zero-trust security architecture (SRB-016).

---

### MID-052 · Application threats
`n: 160` · **Video:** 56 min · **Practice:** 2.5 h

**Prerequisites:** JNR-041, MID-051

**Learning outcomes** — the learner can:
1. Threat-model a service with STRIDE and a data-flow diagram.
2. Explain the OWASP API Security Top 10 (e.g., BOLA, broken function-level authorization, unrestricted resource consumption).
3. Design abuse prevention (bots, scraping, credential stuffing, promo abuse).
4. Turn threats into tests and backlog items.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-052-L01 | Threat modeling with STRIDE | 12 |
| MID-052-L02 | OWASP API Security Top 10 | 14 |
| MID-052-L03 | Business-logic abuse | 10 |
| MID-052-L04 | From threats to tests | 8 |
| MID-052-L05 | Demo: threat-modeling the checkout flow | 12 |

**Lab** — `MID-052-LAB1` *Threat model:* STRIDE model of Shop Platform with mitigations and security tests for the top five threats. Acceptance: reviewed threat model; tests in CI.

**Common mistakes:** threat models written once and forgotten; ignoring business-logic abuse.

**Assessment:** threat model review.

**Career relevance:** security reviews (SRC-018).

---

### MID-071 · AI application threats
`n: new (added in v2.0)` · **Video:** 61 min · **Practice:** 2.5 h · `version:` follows the current OWASP Top 10 for LLM Applications — verify before recording

**Prerequisites:** MID-052, MID-069

**Learning outcomes** — the learner can:
1. Explain the OWASP Top 10 for LLM Applications categories, including prompt injection, sensitive information disclosure, improper output handling, excessive agency, system prompt leakage, vector and embedding weaknesses, and unbounded consumption.
2. Demonstrate indirect prompt injection through retrieved content and mitigate it (content provenance, separation of instructions and data, tool restrictions, output checks).
3. Prevent data exfiltration through tools, links, and rendered output.
4. Protect against cost and resource abuse with per-user quotas, input limits, and loop limits.
5. Add these threats to the service's threat model and to automated security tests.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-071-L01 | The LLM threat landscape | 12 |
| MID-071-L02 | Indirect prompt injection through retrieved content | 10 |
| MID-071-L03 | Excessive agency and improper output handling | 10 |
| MID-071-L04 | Sensitive data disclosure and system prompt leakage | 8 |
| MID-071-L05 | Unbounded consumption and cost abuse | 8 |
| MID-071-L06 | Demo: a poisoned help article hijacks the assistant, then the fix | 13 |

**Lab** — `MID-071-LAB1` *Attack the assistant:* write automated tests for direct and indirect injection (a planted help article), attempts to read another customer's data via tools, data exfiltration via generated links, and quota exhaustion; then fix what they find. Acceptance: all attack tests run in CI and pass after the fixes; threat model updated.

**Common mistakes:** relying on "ignore malicious instructions" in the system prompt as the only defense; trusting content because it came from your own index; rendering model output as HTML or executing it.

**Assessment:** threat-model the order-support assistant and rank the top five risks with mitigations.

**Career relevance:** AI security architecture (ARC-046) and responsible AI (SRA-022).

---

### MID-053 · Dependency security
`n: 161` · **Video:** 56 min · **Practice:** 2 h

**Prerequisites:** JNR-042, JNR-051

**Learning outcomes** — the learner can:
1. Run software composition analysis and triage findings by exploitability and reachability.
2. Generate an SBOM (CycloneDX) for services and images.
3. Scan container images and pin base images.
4. Explain supply-chain risks (typosquatting, compromised builds) and controls (signing, provenance).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-053-L01 | Your code is mostly other people's code | 8 |
| MID-053-L02 | SCA and triage | 10 |
| MID-053-L03 | SBOMs | 8 |
| MID-053-L04 | Image scanning | 8 |
| MID-053-L05 | Supply-chain security | 10 |
| MID-053-L06 | Demo: triaging a critical CVE | 12 |

**Lab** — `MID-053-LAB1` *Secure builds:* SBOMs and image scans in every pipeline with a severity gate and documented exceptions. Acceptance: a planted vulnerable dependency fails the build.

**Common mistakes:** ignoring all findings due to noise; never updating base images.

**Assessment:** triage exercise.

**Career relevance:** secure delivery at platform level (STF-008).

---

### MID-054 · Secrets and cryptography
`n: 162` · **Video:** 62 min · **Practice:** 2 h

**Prerequisites:** JNR-042

**Learning outcomes** — the learner can:
1. Explain symmetric vs asymmetric encryption, hashing, and signatures, and when each is used.
2. Configure TLS correctly, including for service-to-service and database connections.
3. Store and rotate secrets with a secrets manager (Vault or cloud equivalent).
4. Explain envelope encryption and key management services, and encrypt sensitive columns.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-054-L01 | Cryptography for engineers | 12 |
| MID-054-L02 | TLS in practice | 10 |
| MID-054-L03 | Encryption at rest | 8 |
| MID-054-L04 | Key management and envelope encryption | 10 |
| MID-054-L05 | Secrets managers and rotation | 10 |
| MID-054-L06 | Demo: rotating a database password without downtime | 12 |

**Lab** — `MID-054-LAB1` *Secrets in Shop:* move all secrets to a secrets manager; rotate the database credentials live; encrypt stored customer phone numbers. Acceptance: no secret in images, manifests, or Git.

**Common mistakes:** inventing crypto; disabling certificate validation; secrets in environment dumps.

**Assessment:** quiz plus lab.

**Career relevance:** security architecture (ARC-028).

---

### MID-055 · CI/CD advanced
`n: 163` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** JNR-051, JNR-052

**Learning outcomes** — the learner can:
1. Promote one immutable artifact through environments (dev, staging, production).
2. Add automated quality gates (tests, contracts, coverage thresholds, security scans).
3. Implement blue-green or rolling deployments with automated rollback on failed checks.
4. Use feature flags to separate deployment from release.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-055-L01 | Build once, promote everywhere | 10 |
| MID-055-L02 | Environments and approvals | 8 |
| MID-055-L03 | Quality gates | 10 |
| MID-055-L04 | Deployment strategies | 12 |
| MID-055-L05 | Feature flags | 8 |
| MID-055-L06 | Demo: an automated rollback on a failed health check | 12 |

**Lab** — `MID-055-LAB1` *Promotion pipeline:* Shop services promoted through two environments with gates and automatic rollback. Acceptance: a deliberately broken release is rolled back without human action.

**Common mistakes:** rebuilding per environment; manual production steps; flags never removed.

**Assessment:** pipeline review.

**Career relevance:** large migrations (SRB-017) and engineering productivity (STF-009).

---

### MID-056 · Cloud fundamentals
`n: 164` · **Video:** 72 min · **Practice:** 3 h

**Prerequisites:** JNR-048, JNR-052

**Learning outcomes** — the learner can:
1. Explain regions, availability zones, and the shared-responsibility model.
2. Design a basic VPC/VNet with public and private subnets.
3. Configure IAM with least privilege for a service.
4. Use a managed database, load balancer, and object storage, and estimate their cost.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-056-L01 | Cloud building blocks | 10 |
| MID-056-L02 | Regions and availability zones | 8 |
| MID-056-L03 | Identity and access management | 12 |
| MID-056-L04 | Networking: VPCs and subnets | 12 |
| MID-056-L05 | Managed databases, load balancers, object storage | 12 |
| MID-056-L06 | Reading a cloud bill | 6 |
| MID-056-L07 | Demo: a private database reachable only from the app | 12 |

**Lab** — `MID-056-LAB1` *Shop in the cloud:* network, managed PostgreSQL, object storage for images, and least-privilege roles (clicked once, then rebuilt with Terraform in MID-058). Acceptance: database has no public endpoint; monthly cost estimate written.

**Common mistakes:** admin credentials for applications; public databases; forgetting to tear down.

**Assessment:** architecture diagram review.

**Career relevance:** cloud architecture (ARC-P2).

---

### MID-057 · Kubernetes foundations
`n: 165` · **Video:** 106 min · **Practice:** 4 h

**Prerequisites:** JNR-049, MID-056

**Learning outcomes** — the learner can:
1. Explain the control plane, nodes, and the desired-state model.
2. Deploy services with Deployments, Services, ConfigMaps, and Secrets.
3. Configure liveness, readiness, and startup probes plus resource requests and limits for JVM services.
4. Scale with the Horizontal Pod Autoscaler and perform rolling updates.
5. Debug pods (`describe`, `logs`, `exec`, events).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-057-L01 | Why Kubernetes | 8 |
| MID-057-L02 | Architecture and desired state | 10 |
| MID-057-L03 | Pods and Deployments | 12 |
| MID-057-L04 | Services and Ingress | 10 |
| MID-057-L05 | ConfigMaps and Secrets | 8 |
| MID-057-L06 | Probes for JVM services | 10 |
| MID-057-L07 | Requests, limits, and autoscaling | 12 |
| MID-057-L08 | Debugging pods | 10 |
| MID-057-L09 | Demo: deploying Shop Platform to a cluster | 14 |
| MID-057-L10 | Demo: a crash-looping pod, diagnosed | 12 |

**Lab** — `MID-057-LAB1` *Shop on Kubernetes:* all services, Kafka (operator or managed), and the gateway on a cluster with probes, limits, and autoscaling on `orders`. Acceptance: rolling update under load with zero failed requests.

**Common mistakes:** liveness probes that check the database; no memory limits for JVMs; `latest` tags.

**Assessment:** debugging exercise on a broken manifest set.

**Career relevance:** platform engineering (SRB-010) and the MID capstone.

---

### MID-058 · Infrastructure as Code
`n: 166` · **Video:** 62 min · **Practice:** 3 h

**Prerequisites:** MID-056

**Learning outcomes** — the learner can:
1. Describe infrastructure declaratively with Terraform and apply changes through plan and review.
2. Manage remote state with locking and explain state drift.
3. Structure configuration into reusable modules and environments.
4. Run Terraform from CI with reviewable plans.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-058-L01 | Why infrastructure as code | 8 |
| MID-058-L02 | Terraform basics | 12 |
| MID-058-L03 | State and drift | 10 |
| MID-058-L04 | Modules and environments | 10 |
| MID-058-L05 | Terraform in CI | 8 |
| MID-058-L06 | Demo: rebuilding the clicked infrastructure as code | 14 |

**Lab** — `MID-058-LAB1` *Shop infrastructure:* the MID-056 environment rebuilt in Terraform with modules, remote state, and plans posted on PRs. Acceptance: destroy and recreate the environment from code alone.

**Common mistakes:** local state files; manual changes in the console; one giant root module.

**Assessment:** plan review exercise.

**Career relevance:** infrastructure governance (ARC-020).
