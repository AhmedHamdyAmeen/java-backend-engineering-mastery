# ARC-P3 — Enterprise Data, Integration, and Security

**Phase goal:** the architect designs how data lives, moves, and is protected across an enterprise solution: separating operational and analytical data, choosing integration styles, managing APIs and events as products, controlling identity and access, building security and compliance into the design, governing data, planning for failure, and connecting to the ERP, CRM, payment, and identity systems the business already runs.

**Running case:** *Larkspur Retail* (fictional). A mid-size retailer with 120 stores and a dated on-premises web shop needs a platform for web and mobile customers, inventory, payments, order fulfillment, customer service, and reporting, integrated with its existing ERP and CRM. The learner is the solution architect. Every lab produces a piece of the Solution Architect capstone (`ARC-CAP`): this phase delivers the data, integration, identity, security, compliance, and resilience architecture.

**Format:** case studies, worked architecture sessions, and stakeholder role-play. Each module lists the workplace evidence that demonstrates the role.

**Phase total:** ~10.9 h video · ~33 h practice

---

### ARC-023 · Data architecture
`n: 277` · **Video:** 68 min · **Practice:** 3 h

**Prerequisites:** MID-044, SRA-004

**Learning outcomes** — the architect can:
1. Separate operational (transactional) and analytical workloads and explain why they need different stores.
2. Describe the data lifecycle (creation, use, sharing, archiving, deletion) for each major data set.
3. Choose between a data warehouse, a data lake, and a lakehouse for a reporting need.
4. Produce a conceptual data model and a data-flow view for a solution.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-023-L01 | Data architecture for solution architects | 10 |
| ARC-023-L02 | Operational vs analytical workloads | 12 |
| ARC-023-L03 | Warehouses, lakes, and lakehouses | 12 |
| ARC-023-L04 | The data lifecycle | 10 |
| ARC-023-L05 | Conceptual models and data-flow views | 10 |
| ARC-023-L06 | Demo: Larkspur's data landscape from sales floor to board report | 14 |

**Lab** — `ARC-023-LAB1` *Larkspur data architecture:* conceptual data model, systems of record per data set, data-flow view from stores and web to reporting, and a lifecycle table. Acceptance: every data set has one system of record and a defined retention.

**Common mistakes:** reporting directly off production databases; data sets with no system of record; ignoring deletion.

**Assessment:** data architecture review.

**Workplace evidence:** a data architecture view you produced that guided a reporting or platform decision.

**Career relevance:** the data section of every solution architecture pack.

---

### ARC-024 · Integration patterns
`n: 278` · **Video:** 70 min · **Practice:** 4 h

**Prerequisites:** SRB-007, ARC-009

**Learning outcomes** — the architect can:
1. Choose between synchronous APIs, asynchronous events, batch ETL/ELT, file exchange, and CDC for each integration, with justification.
2. Explain the coupling, latency, and failure characteristics of each style.
3. Design an integration catalog that lists every interface with owner, style, frequency, and SLA.
4. Apply enterprise integration patterns (message translator, content-based router, aggregator) where they help.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-024-L01 | Integration styles compared | 12 |
| ARC-024-L02 | Coupling, latency, and failure | 10 |
| ARC-024-L03 | Batch, ETL, and ELT | 10 |
| ARC-024-L04 | Enterprise integration patterns | 10 |
| ARC-024-L05 | Demo: choosing a style for each Larkspur interface | 14 |
| ARC-024-L06 | Demo: replacing a nightly stock file with near-real-time CDC | 14 |

**Lab** — `ARC-024-LAB1` *Integration catalog:* every Larkspur interface (ERP, CRM, payments, carriers, stores, marketing) with chosen style, owner, frequency, volume, and SLA, plus a context diagram. Acceptance: each style choice justified against latency and coupling needs.

**Common mistakes:** one style for everything; real-time integration where daily batch is enough; no owner per interface.

**Assessment:** integration catalog defense.

**Workplace evidence:** an integration design you produced and how it held up in operation.

**Career relevance:** integration is where most enterprise solutions succeed or fail.

---

### ARC-025 · API management
`n: 279` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** MID-035, SRC-006

**Learning outcomes** — the architect can:
1. Decide what an API management layer provides (gateway, developer portal, keys, quotas, analytics) and whether a solution needs one.
2. Design API governance: style guide, review, versioning, and lifecycle.
3. Set quotas and access tiers for internal, partner, and public consumers.
4. Treat APIs as products with owners and consumers.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-025-L01 | APIs as products | 10 |
| ARC-025-L02 | What API management platforms provide | 12 |
| ARC-025-L03 | API governance and lifecycle | 12 |
| ARC-025-L04 | Quotas, keys, and consumer tiers | 10 |
| ARC-025-L05 | Demo: designing Larkspur's partner API program | 14 |

**Lab** — `ARC-025-LAB1` *Partner API program:* API management design for Larkspur's marketplace partners and mobile app: consumer tiers, quotas, onboarding through a developer portal, and versioning policy. Acceptance: reviewed by a role-played partner manager and security lead.

**Common mistakes:** a gateway without governance; one quota for all consumers; no deprecation path.

**Assessment:** API program review.

**Workplace evidence:** an API program or governance process you designed or improved.

**Career relevance:** API management choices recur in almost every integration-heavy solution.

---

### ARC-026 · Event architecture
`n: 280` · **Video:** 66 min · **Practice:** 3 h

**Prerequisites:** SRB-002, ARC-024

**Learning outcomes** — the architect can:
1. Define event ownership across systems and organizations.
2. Set up an event catalog with schemas, owners, and consumers.
3. Define compatibility rules and an evolution process for event schemas.
4. Decide when an event backbone (broker or streaming platform) is justified for an enterprise.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-026-L01 | Events at enterprise scale | 10 |
| ARC-026-L02 | Event ownership | 10 |
| ARC-026-L03 | Event catalogs and schemas | 12 |
| ARC-026-L04 | Compatibility and evolution | 10 |
| ARC-026-L05 | When an event backbone pays off | 10 |
| ARC-026-L06 | Demo: Larkspur's order and stock events, from catalog to consumers | 14 |

**Lab** — `ARC-026-LAB1` *Event catalog:* Larkspur's business events (order placed, stock changed, shipment dispatched, return received) with owners, schemas, consumers, and compatibility rules. Acceptance: no event has two owners; evolution process documented.

**Common mistakes:** events that mirror database tables; no owner for shared events.

**Assessment:** catalog review.

**Workplace evidence:** an event catalog or event standard you established.

**Career relevance:** event architecture decisions shape integration for years.

---

### ARC-027 · Identity and access
`n: 281` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** ARC-017

**Learning outcomes** — the architect can:
1. Choose between RBAC and ABAC (or a combination) for a solution's authorization needs.
2. Design identity federation between the enterprise directory, partners, and customer identity.
3. Design privileged access management for administrators and operators.
4. Define joiner-mover-leaver processes and access reviews.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-027-L01 | Authorization models: RBAC and ABAC | 12 |
| ARC-027-L02 | Identity federation | 12 |
| ARC-027-L03 | Privileged access | 10 |
| ARC-027-L04 | Joiners, movers, leavers, and access reviews | 10 |
| ARC-027-L05 | Demo: store managers, call-center agents, and partners in one access model | 14 |

**Lab** — `ARC-027-LAB1` *Larkspur access model:* roles and attributes for staff, store managers, customer-service agents, partners, and customers; federation design; privileged-access controls. Acceptance: least privilege demonstrated for five representative users.

**Common mistakes:** role explosion; shared admin accounts; no access reviews.

**Assessment:** access model review.

**Workplace evidence:** an access model or federation design you delivered.

**Career relevance:** identity is a cross-cutting concern in every enterprise solution.

---

### ARC-028 · Security architecture
`n: 282` · **Video:** 71 min · **Practice:** 4 h

**Prerequisites:** SRA-009, ARC-018

**Learning outcomes** — the architect can:
1. Apply zero-trust and defense-in-depth principles across application, data, network, and identity layers.
2. Threat-model a whole solution and prioritize controls by risk.
3. Map controls to the security requirements of the business and its standards.
4. Produce a security architecture view that security teams can review and approve.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-028-L01 | Security architecture for whole solutions | 10 |
| ARC-028-L02 | Zero trust and defense in depth | 12 |
| ARC-028-L03 | Solution-level threat modeling | 12 |
| ARC-028-L04 | Controls and security requirements | 10 |
| ARC-028-L05 | Demo: threat-modeling Larkspur's checkout and payment flow | 14 |
| ARC-028-L06 | Demo: walking a security team through the security architecture view | 13 |

**Lab** — `ARC-028-LAB1` *Larkspur security architecture:* threat model, control map by layer, and a security architecture view for the platform. Acceptance: top ten threats each have a control and an owner; reviewed by a role-played CISO.

**Common mistakes:** security as a list of products; controls with no threat behind them; perimeter-only thinking.

**Assessment:** security architecture defense.

**Workplace evidence:** a security architecture you designed that passed a formal review.

**Career relevance:** security sign-off is a gate for every enterprise solution.

---

### ARC-029 · Privacy and compliance
`n: 283` · **Video:** 74 min · **Practice:** 3.5 h

**Prerequisites:** SRA-009, ARC-023

**Learning outcomes** — the architect can:
1. Classify data (public, internal, confidential, personal, payment) and attach handling rules to each class.
2. Design retention, deletion, and data-subject-rights handling (access, correction, erasure) across systems.
3. Address data residency and cross-border transfer requirements in the architecture.
4. Reduce payment-card compliance scope (PCI DSS) with tokenization and hosted payment pages.
5. Design audit trails that satisfy auditors without logging sensitive data.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-029-L01 | Data classification | 10 |
| ARC-029-L02 | Retention and deletion | 10 |
| ARC-029-L03 | Data-subject rights across many systems | 10 |
| ARC-029-L04 | Residency and cross-border transfers | 8 |
| ARC-029-L05 | Payment compliance scope | 10 |
| ARC-029-L06 | Demo: shrinking Larkspur's PCI DSS scope with a hosted payment page | 13 |
| ARC-029-L07 | Demo: tracing one customer's data for an erasure request | 13 |

**Lab** — `ARC-029-LAB1` *Larkspur compliance architecture:* data classification, retention schedule, data-subject-request flow across platform, ERP, and CRM, and payment-scope reduction. Acceptance: reviewed by a role-played data protection officer; no card data stored in Larkspur systems.

**Common mistakes:** deletion that misses backups and analytics copies; compliance documentation without architectural controls.

**Assessment:** compliance architecture review.

**Workplace evidence:** a compliance requirement you turned into architecture that passed an audit.

**Career relevance:** privacy and compliance constraints shape retail and payments solutions.

---

### ARC-030 · Data governance
`n: 284` · **Video:** 58 min · **Practice:** 2.5 h

**Prerequisites:** SRA-004, ARC-029

**Learning outcomes** — the architect can:
1. Define data ownership and stewardship roles for a solution.
2. Specify data quality rules and how they are measured and reported.
3. Capture lineage from source to report.
4. Design access policies for data consumers, including analytics.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-030-L01 | Governance that enables use | 10 |
| ARC-030-L02 | Owners and stewards | 10 |
| ARC-030-L03 | Data quality rules | 12 |
| ARC-030-L04 | Lineage and access policies | 12 |
| ARC-030-L05 | Demo: tracing a wrong revenue number back to its source | 14 |

**Lab** — `ARC-030-LAB1` *Larkspur data governance:* owners and stewards for key data sets, ten quality rules with measures, lineage for the daily sales report, and analytics access policies. Acceptance: lineage complete from till and web order to board report.

**Common mistakes:** governance committees without data owners; quality rules nobody measures.

**Assessment:** governance plan review.

**Workplace evidence:** a data quality or lineage improvement you led.

**Career relevance:** governance makes the data architecture trustworthy.

---

### ARC-031 · Resilience architecture
`n: 285` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** SRA-006, ARC-019

**Learning outcomes** — the architect can:
1. Enumerate failure scenarios for a whole solution, including third-party and on-premises dependencies.
2. Isolate faults so a failing component degrades a feature rather than the business.
3. Write business continuity plans for processes when systems are unavailable (e.g., stores selling offline).
4. Define resilience tests that prove the design.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-031-L01 | Resilience beyond infrastructure | 10 |
| ARC-031-L02 | Failure scenarios for enterprise solutions | 12 |
| ARC-031-L03 | Fault isolation and degradation | 12 |
| ARC-031-L04 | Business continuity planning | 10 |
| ARC-031-L05 | Demo: keeping 120 stores selling when the central platform is down | 14 |

**Lab** — `ARC-031-LAB1` *Larkspur resilience:* failure-scenario catalog, degradation design (offline store sales, payment-provider failover, ERP outage queueing), and continuity plans with resilience tests. Acceptance: every critical business process has a documented degraded mode.

**Common mistakes:** resilience that covers servers but not processes; assuming the ERP is always available.

**Assessment:** scenario walkthrough with the assessor.

**Workplace evidence:** a continuity plan or degraded mode you designed that was used or tested.

**Career relevance:** resilience is a top concern of business stakeholders.

---

### ARC-032 · Integration with enterprise systems
`n: 286` · **Video:** 72 min · **Practice:** 4 h

**Prerequisites:** ARC-024, ARC-027

**Learning outcomes** — the architect can:
1. Integrate with an ERP (products, prices, stock, financial postings) respecting it as the system of record.
2. Integrate with a CRM for customer profiles, service cases, and marketing consent.
3. Integrate payment gateways and identity providers with correct failure handling and reconciliation.
4. Use anti-corruption layers to keep enterprise-system models out of the new platform's domain.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-032-L01 | Working with systems of record | 10 |
| ARC-032-L02 | ERP integration | 12 |
| ARC-032-L03 | CRM integration | 10 |
| ARC-032-L04 | Payment gateways and identity providers | 12 |
| ARC-032-L05 | Demo: an anti-corruption layer between the platform and the ERP | 14 |
| ARC-032-L06 | Demo: reconciling payments between the gateway, platform, and ERP | 14 |

**Lab** — `ARC-032-LAB1` *Larkspur enterprise integration:* integration design for ERP, CRM, payment gateway, and identity provider, with data ownership, failure handling, and reconciliation. Acceptance: every flow defines the system of record and what happens when the other side is down.

**Common mistakes:** letting ERP data models leak into the platform; no reconciliation for money flows.

**Assessment:** integration design defense.

**Workplace evidence:** an ERP, CRM, or payment integration you designed and its operational results.

**Career relevance:** enterprise-system integration is the core of most solution architect roles.
