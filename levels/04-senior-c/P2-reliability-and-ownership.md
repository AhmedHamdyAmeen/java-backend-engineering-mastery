# SRC-P2 — Reliability and Technical Ownership

**Phase goal:** the engineer owns a subsystem end to end: it launches safely, meets its SLOs, survives disasters, stays correct across services, gets faster on evidence, carries manageable debt, passes security review, and is supported by an engineer who leads incidents and grows the people around them.

**Running case:** *Order Processing at 10×* continues. The redesign from SRC-P1 is built, hardened, and handed over — this phase produces most of the capstone's evidence.

**Format:** as in SRC-P1 — case studies, worked sessions, and scenario-based assessment.

**Phase total:** ~15.1 h video · ~43 h practice

---

### SRC-011 · Production readiness
`n: 185` · **Video:** 94 min · **Practice:** 4 h

**Prerequisites:** MID-055, MID-065

**Learning outcomes** — the engineer can:
1. Run a production readiness review covering observability, capacity, failure handling, security, and support.
2. Design deployment safety: progressive rollout, automated verification, and fast rollback.
3. Decide go/no-go with explicit, pre-agreed criteria.
4. Make rollback possible for data changes, not only code.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-011-L01 | Why launches fail | 10 |
| SRC-011-L02 | The readiness review | 14 |
| SRC-011-L03 | Progressive delivery and canaries | 12 |
| SRC-011-L04 | Automated verification and rollback | 10 |
| SRC-011-L05 | Rolling back data | 10 |
| SRC-011-L06 | Go/no-go decisions | 8 |
| SRC-011-L07 | Demo: a canary that catches a regression | 15 |
| SRC-011-L08 | Demo: a readiness review that says no-go | 15 |

**Lab** — `SRC-011-LAB1` *Launch the redesign:* readiness review for the redesigned order subsystem and a canary rollout with automated analysis. Acceptance: a seeded regression is halted at the canary stage.

**Common mistakes:** readiness as paperwork after launch; rollback plans never rehearsed.

**Assessment:** run a readiness review for a peer's service.

**Workplace evidence:** a launch you led with a readiness review and rollout plan.

**Career relevance:** operational acceptance (ARC-042) and large migrations (SRB-017).

---

### SRC-012 · SLO engineering
`n: 186` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** MID-049, SRC-002

**Learning outcomes** — the engineer can:
1. Derive SLOs from user journeys and business commitments, including dependency SLOs.
2. Write an error-budget policy that changes team behavior when the budget runs out.
3. Design multi-window, multi-burn-rate alerts and tune them for precision and recall.
4. Review SLOs periodically and retire useless ones.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-012-L01 | SLOs from user journeys | 12 |
| SRC-012-L02 | Composing SLOs across dependencies | 12 |
| SRC-012-L03 | Error-budget policies | 12 |
| SRC-012-L04 | Multi-window burn-rate alerting | 12 |
| SRC-012-L05 | Reviewing and evolving SLOs | 8 |
| SRC-012-L06 | Demo: tuning noisy alerts with burn-rate windows | 15 |
| SRC-012-L07 | Demo: negotiating an error-budget policy with product | 15 |

**Lab** — `SRC-012-LAB1` *99.95% for orders:* SLOs for the order journey consistent with the 99.95% commitment and dependency SLOs, an error-budget policy agreed with role-played product leadership, and tuned alerts. Acceptance: alert simulation shows no pages for brief blips and fast pages for real outages.

**Common mistakes:** promising more nines than dependencies allow; budgets with no consequences.

**Assessment:** SLO and policy review.

**Workplace evidence:** an SLO or error-budget policy adopted by your team.

**Career relevance:** organization-wide reliability (STF-005).

---

### SRC-022 · Operating AI in production
`n: new (added in v2.0)` · **Video:** 86 min · **Practice:** 4 h

**Prerequisites:** SRC-011, SRC-021

**Learning outcomes** — the engineer can:
1. Version prompts, model choices, and retrieval settings as deployable configuration with rollback.
2. Gate releases on evaluation results and roll out prompt or model changes progressively.
3. Detect quality drift (model updates, data changes, new user behavior) from evaluation and production signals.
4. Run incidents for bad AI output (wrong, unsafe, or leaking answers), including kill switches and human review queues.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-022-L01 | AI changes are deployments too | 10 |
| SRC-022-L02 | Versioning prompts, models, and retrieval | 12 |
| SRC-022-L03 | Evaluation-gated and progressive releases | 12 |
| SRC-022-L04 | Detecting drift | 10 |
| SRC-022-L05 | Bad-output incidents, kill switches, and human review | 12 |
| SRC-022-L06 | Demo: rolling back a prompt change that broke refund answers | 15 |
| SRC-022-L07 | Demo: an incident where the assistant revealed another customer's order | 15 |

**Lab** — `SRC-022-LAB1` *Run the assistant:* put the order-support assistant's prompts and model choice under versioned configuration; add an evaluation gate and canary; rehearse a bad-output incident with a kill switch and a human review queue. Acceptance: a seeded regression is blocked by the gate; the kill switch disables the feature in under one minute; postmortem written.

**Common mistakes:** editing prompts directly in production; no record of which prompt and model produced an answer; treating unsafe output as "just a bug" without an incident process.

**Assessment:** incident simulation on a misbehaving AI feature.

**Workplace evidence:** a release process or incident you ran for an AI feature.

**Career relevance:** shared AI platforms (SRB-021) and responsible AI controls (SRA-022).

---

### SRC-013 · Disaster recovery
`n: 187` · **Video:** 96 min · **Practice:** 4.5 h

**Prerequisites:** MID-018, SRC-009

**Learning outcomes** — the engineer can:
1. Set RPO and RTO per data set and service from business impact.
2. Choose backup, replication, and failover strategies that meet them, including for Kafka and caches.
3. Design and run recovery exercises with measured results.
4. Plan for region or account loss at the subsystem level.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-013-L01 | Disasters that actually happen | 10 |
| SRC-013-L02 | RPO and RTO from business impact | 12 |
| SRC-013-L03 | Backup and replication strategies | 12 |
| SRC-013-L04 | Failover design | 12 |
| SRC-013-L05 | Recovering event streams and derived data | 10 |
| SRC-013-L06 | Recovery exercises | 10 |
| SRC-013-L07 | Demo: recovering the order database within a 15-minute RTO | 15 |
| SRC-013-L08 | Demo: rebuilding derived data after a Kafka cluster loss | 15 |

**Lab** — `SRC-013-LAB1` *DR drill:* DR plan for the order subsystem and a timed recovery drill from simulated database and cluster loss. Acceptance: RTO and RPO met, or gaps documented with a remediation plan.

**Common mistakes:** RTO set without measurement; forgetting secrets, DNS, and config in recovery; derived stores never rebuilt.

**Assessment:** drill report review.

**Workplace evidence:** a recovery exercise you planned or ran.

**Career relevance:** multi-region systems (SRB-004) and HA/DR architecture (ARC-019).

---

### SRC-014 · Data integrity
`n: 188` · **Video:** 84 min · **Practice:** 4 h

**Prerequisites:** MID-029, MID-031

**Learning outcomes** — the engineer can:
1. Identify invariants that span services and decide how each is protected or detected.
2. Explain the difference between exactly-once delivery (unavailable) and exactly-once *effects* (designable).
3. Build reconciliation jobs that detect and repair drift between services and external systems (e.g., payment provider).
4. Design audit trails for financially significant data.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-014-L01 | Invariants across boundaries | 12 |
| SRC-014-L02 | Exactly-once effects | 12 |
| SRC-014-L03 | Prevent, detect, repair | 10 |
| SRC-014-L04 | Reconciliation design | 12 |
| SRC-014-L05 | Audit trails | 8 |
| SRC-014-L06 | Demo: reconciling orders against the payment provider | 15 |
| SRC-014-L07 | Demo: tracing a double charge to its root cause | 15 |

**Lab** — `SRC-014-LAB1` *Money matches:* a daily reconciliation between orders, payments, and the provider's settlement file that detects and repairs three planted discrepancy types. Acceptance: report with counts, repairs logged and auditable.

**Common mistakes:** assuming messaging guarantees remove the need for reconciliation; repairs without audit.

**Assessment:** invariant analysis of an unseen workflow.

**Workplace evidence:** a reconciliation or integrity check you introduced and what it found.

**Career relevance:** data governance (ARC-030) and compliance (SRA-009).

---

### SRC-015 · Advanced troubleshooting
`n: 189` · **Video:** 91 min · **Practice:** 4.5 h

**Prerequisites:** MID-008, MID-017, MID-047

**Learning outcomes** — the engineer can:
1. Diagnose thread starvation, connection exhaustion, and deadlocks across services from telemetry and dumps.
2. Recognize cascading-failure and metastable-failure patterns (retry storms, queue buildup) and break them.
3. Form and test hypotheses systematically under time pressure.
4. Find causes that span layers (JVM, database, network, Kubernetes).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-015-L01 | Troubleshooting as hypothesis testing | 10 |
| SRC-015-L02 | Thread starvation | 10 |
| SRC-015-L03 | Connection exhaustion | 10 |
| SRC-015-L04 | Distributed deadlocks and lock convoys | 10 |
| SRC-015-L05 | Cascading and metastable failures | 14 |
| SRC-015-L06 | Cross-layer investigations | 10 |
| SRC-015-L07 | Demo: a retry storm that won't stop by itself | 15 |
| SRC-015-L08 | Demo: latency caused by Kubernetes CPU throttling | 12 |

**Lab** — `SRC-015-LAB1` *Mystery outages:* three timed scenarios on Shop Platform with layered causes. Acceptance: root cause, evidence chain, and fix for each within the time box.

**Common mistakes:** stopping at the first plausible cause; restarting away the evidence.

**Assessment:** live troubleshooting simulation (graduation gate component).

**Workplace evidence:** a hard production investigation you led, written up.

**Career relevance:** incident leadership (SRC-019) and systemic risk (STF-005).

---

### SRC-016 · Performance engineering
`n: 190` · **Video:** 92 min · **Practice:** 4.5 h

**Prerequisites:** MID-046, SRC-005

**Learning outcomes** — the engineer can:
1. Design benchmarks (JMH for code, load tests for systems) that measure what matters and avoid common traps.
2. Remove bottlenecks in order of impact and stop when the target is met.
3. Detect performance regressions in CI.
4. Communicate performance results with uncertainty and context.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-016-L01 | A performance engineering process | 10 |
| SRC-016-L02 | Microbenchmarks with JMH | 12 |
| SRC-016-L03 | System benchmarks that predict production | 12 |
| SRC-016-L04 | Removing bottlenecks in order | 10 |
| SRC-016-L05 | Regression detection in CI | 10 |
| SRC-016-L06 | Reporting results honestly | 8 |
| SRC-016-L07 | Demo: halving checkout p99 with evidence | 15 |
| SRC-016-L08 | Demo: a JMH benchmark that lied, and the fixed version | 15 |

**Lab** — `SRC-016-LAB1` *Meet the latency target:* bring checkout p99 within the SLO at 10× forecast load; add a performance regression check to CI. Acceptance: before/after evidence; CI catches a seeded regression.

**Common mistakes:** JMH-free microbenchmarks; optimizing non-bottlenecks; single-run results.

**Assessment:** performance report review.

**Workplace evidence:** a measured performance improvement you delivered.

**Career relevance:** cost-performance optimization (SRA-007).

---

### SRC-017 · Technical debt
`n: 191` · **Video:** 75 min · **Practice:** 3.5 h

**Prerequisites:** MID-065

**Learning outcomes** — the engineer can:
1. Classify debt (deliberate/inadvertent, prudent/reckless) and describe its interest in concrete costs.
2. Build a debt register and prioritize by cost of delay and risk.
3. Pay debt down incrementally alongside feature work (boy-scout rule, strangler techniques).
4. Make the business case for a debt investment.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-017-L01 | What technical debt is and isn't | 10 |
| SRC-017-L02 | Measuring the interest | 12 |
| SRC-017-L03 | A debt register | 8 |
| SRC-017-L04 | Prioritizing by cost of delay | 10 |
| SRC-017-L05 | Incremental remediation | 10 |
| SRC-017-L06 | Making the case | 10 |
| SRC-017-L07 | Demo: turning a vague complaint into a funded debt item | 15 |

**Lab** — `SRC-017-LAB1` *Shop debt register:* register for Shop Platform with cost estimates and a one-quarter paydown plan; pitch it to role-played product leadership. Acceptance: at least one item approved on its business case.

**Common mistakes:** "rewrite" as the remediation; debt lists with no costs.

**Assessment:** pitch and register review.

**Workplace evidence:** a debt item you got prioritized and delivered.

**Career relevance:** technical strategy (SRA-010) and modernization (ARC-010).

---

### SRC-018 · Security reviews
`n: 192` · **Video:** 67 min · **Practice:** 3.5 h

**Prerequisites:** MID-052, SRC-010

**Learning outcomes** — the engineer can:
1. Lead a secure design review using a threat model and a checklist adapted to the system.
2. Verify authorization boundaries end to end, including service-to-service and data access paths.
3. Assess risk (likelihood × impact) and agree mitigations or accepted risks with owners.
4. Work with a security team as a peer, not a gate.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-018-L01 | Security reviews engineers run themselves | 10 |
| SRC-018-L02 | Threat modeling at subsystem scale | 12 |
| SRC-018-L03 | Authorization boundaries end to end | 12 |
| SRC-018-L04 | Risk rating and acceptance | 10 |
| SRC-018-L05 | Working with security teams | 8 |
| SRC-018-L06 | Demo: reviewing the redesigned order subsystem | 15 |

**Lab** — `SRC-018-LAB1` *Secure design review:* review a peer's redesign; produce findings, risk ratings, and agreed actions. Acceptance: review accepted by the peer and a role-played security lead.

**Common mistakes:** reviews limited to the public API; findings without owners.

**Assessment:** review-quality rubric.

**Workplace evidence:** a security review you led and its tracked outcomes.

**Career relevance:** security architecture (SRB-016, ARC-028).

---

### SRC-019 · Incident leadership
`n: 193` · **Video:** 71 min · **Practice:** 3.5 h

**Prerequisites:** MID-050

**Learning outcomes** — the engineer can:
1. Act as incident commander: assign roles, set priorities, and keep responders focused.
2. Communicate to stakeholders at a steady cadence with impact, actions, and next update.
3. Decide on risky mitigations with incomplete information.
4. Facilitate a blameless postmortem that finds systemic contributing factors and gets actions done.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-019-L01 | The incident commander role | 12 |
| SRC-019-L02 | Running the response | 12 |
| SRC-019-L03 | Stakeholder communication | 10 |
| SRC-019-L04 | Decisions under uncertainty | 10 |
| SRC-019-L05 | Facilitating postmortems | 12 |
| SRC-019-L06 | Demo: commanding a multi-team incident simulation | 15 |

**Lab** — `SRC-019-LAB1` *Command a game day:* lead a multi-team simulated incident with role-players, then facilitate its postmortem. Acceptance: assessed on coordination, communication, and action quality.

**Common mistakes:** commander debugging instead of coordinating; silent periods for stakeholders.

**Assessment:** incident-command simulation (graduation gate component).

**Workplace evidence:** an incident you led as commander and its postmortem.

**Career relevance:** incident and crisis leadership (STF-018).

---

### SRC-020 · Mentorship
`n: 194` · **Video:** 63 min · **Practice:** 3 h

**Prerequisites:** MID-066

**Learning outcomes** — the engineer can:
1. Delegate work at the right size for growth, with clear outcomes and support.
2. Coach through code and design review rather than rewrite.
3. Give feedback on design thinking, not only on code.
4. Track a mentee's growth against level expectations.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| SRC-020-L01 | Mentoring as a senior responsibility | 8 |
| SRC-020-L02 | Delegation that grows people | 12 |
| SRC-020-L03 | Coaching through reviews | 10 |
| SRC-020-L04 | Design feedback | 10 |
| SRC-020-L05 | Growth plans | 8 |
| SRC-020-L06 | Demo: a coaching review of a junior's design doc | 15 |

**Lab** — `SRC-020-LAB1` *Mentor a Mid learner:* mentor a Level 3 learner through one capstone component over four weeks. Acceptance: mentee feedback and their delivered result.

**Common mistakes:** taking over the hard parts; feedback that is only praise or only criticism.

**Assessment:** mentee feedback plus reflection.

**Workplace evidence:** an engineer you mentored and how their scope grew.

**Career relevance:** mentoring senior peers (SRB-018) and mentoring at scale (STF-015).

---

## Senior C capstone — Reliability & Performance Redesign (`SRC-CAP`)

Full brief, acceptance criteria, and graduation gate: [`projects/ladder.md`](../../projects/ladder.md#04--reliability--performance-redesign-src-cap).
