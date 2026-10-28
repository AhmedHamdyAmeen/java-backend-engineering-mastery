# ARC-P2 — Cloud and Infrastructure Architecture

**Phase goal:** the architect designs the infrastructure a solution runs on: choosing service models and compute, laying out regions, networks, storage, and databases, designing identity and network security, meeting availability and recovery targets, governing infrastructure at scale, and controlling cost — evaluated against a well-architected framework.

**Running case:** *Larkspur Retail* continues. This phase produces the cloud and infrastructure architecture for the new platform: landing zone, network, compute, data stores, identity, security controls, HA/DR, governance, and cost model — all part of the Architect capstone package (`ARC-CAP`).

**Format:** case studies and worked design sessions. Labs are written for one cloud provider (AWS or Azure, per the pending baseline decision in `CONVENTIONS.md`); lectures teach the provider-neutral principle first and the provider mapping second. Provider service names and limits change — verify them against current documentation before recording.

**Phase total:** ~14.3 h video · ~40 h practice

---

### ARC-011 · Cloud service models
`n: 265` · **Video:** 58 min · **Practice:** 2.5 h

**Prerequisites:** MID-056

**Learning outcomes** — the architect can:
1. Distinguish IaaS, PaaS, SaaS, and managed services by what the customer still operates.
2. Apply the shared-responsibility model to security and operations for each model.
3. Choose a service model per component based on control, operational burden, cost, and lock-in.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-011-L01 | IaaS, PaaS, SaaS, managed services | 12 |
| ARC-011-L02 | Shared responsibility by model | 12 |
| ARC-011-L03 | Control vs operational burden | 10 |
| ARC-011-L04 | Lock-in, honestly assessed | 10 |
| ARC-011-L05 | Demo: choosing service models for each Larkspur component | 14 |

**Lab** — `ARC-011-LAB1` *Service-model matrix:* for each Larkspur component, the chosen service model, who operates what, and the lock-in and exit consideration. Acceptance: responsibility gaps identified and assigned.

**Common mistakes:** IaaS by default; assuming managed means "no operations".

**Assessment:** matrix review.

**Workplace evidence:** a service-model decision that reduced operational burden.

**Career relevance:** compute choices (ARC-014) and cost (ARC-021).

---

### ARC-012 · Cloud architecture
`n: 266` · **Video:** 75 min · **Practice:** 4 h · `version:` provider-specific

**Prerequisites:** MID-056, ARC-011

**Learning outcomes** — the architect can:
1. Use regions and availability zones to design for latency, resilience, and data residency.
2. Apply the provider's reference architectures for a web and mobile commerce workload, adapting rather than copying them.
3. Structure accounts/subscriptions and environments for isolation and blast-radius control.
4. Produce a target cloud architecture diagram with trust boundaries.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-012-L01 | Regions, zones, and edge locations | 10 |
| ARC-012-L02 | Reading reference architectures critically | 12 |
| ARC-012-L03 | Accounts, subscriptions, and environments | 12 |
| ARC-012-L04 | A reference web/mobile commerce architecture | 12 |
| ARC-012-L05 | Demo: Larkspur's target cloud architecture | 15 |
| ARC-012-L06 | Demo: adapting a reference architecture to Larkspur's constraints | 14 |

**Lab** — `ARC-012-LAB1` *Larkspur target architecture:* region and zone choice, account/environment structure, and a target architecture diagram for the platform. Acceptance: each element traceable to a requirement from `ARC-003-LAB1`.

**Common mistakes:** copying a reference architecture wholesale; one account for every environment.

**Assessment:** architecture review.

**Workplace evidence:** a cloud architecture you designed that went to production.

**Career relevance:** every later infrastructure module.

---

### ARC-013 · Networking
`n: 267` · **Video:** 95 min · **Practice:** 4 h · `version:` provider-specific

**Prerequisites:** MID-056, ARC-012

**Learning outcomes** — the architect can:
1. Plan IP address space with CIDR so environments, regions, and on-premises networks don't overlap.
2. Design VPC/VNet layouts with public and private subnets, routing, and NAT.
3. Connect cloud to on-premises (site-to-site VPN, dedicated connections) and choose by bandwidth, latency, and resilience.
4. Expose services privately with private endpoints and keep data paths off the public internet.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-013-L01 | CIDR and address planning | 12 |
| ARC-013-L02 | VPC/VNet layout and subnets | 12 |
| ARC-013-L03 | Routing and NAT | 10 |
| ARC-013-L04 | Hybrid connectivity | 12 |
| ARC-013-L05 | Private endpoints and private data paths | 10 |
| ARC-013-L06 | Hub-and-spoke topologies | 10 |
| ARC-013-L07 | Demo: planning address space for Larkspur, stores, and the data center | 15 |
| ARC-013-L08 | Demo: connecting the cloud platform to the on-premises ERP | 14 |

**Lab** — `ARC-013-LAB1` *Larkspur network design:* address plan, VPC/VNet topology, hybrid connectivity to the data center hosting the ERP, and private endpoints for data stores. Acceptance: no overlapping ranges; no data store reachable from the internet; connectivity failure mode documented.

**Common mistakes:** overlapping CIDRs that block future peering; single VPN tunnel as the only ERP link.

**Assessment:** network design review.

**Workplace evidence:** a network design you produced or reviewed for a hybrid environment.

**Career relevance:** network security (ARC-018) and HA/DR (ARC-019).

---

### ARC-014 · Compute choices
`n: 268` · **Video:** 66 min · **Practice:** 3 h

**Prerequisites:** MID-057, ARC-012

**Learning outcomes** — the architect can:
1. Compare VMs, containers on managed platforms, Kubernetes, and serverless functions by control, scaling, cost, and operating effort.
2. Match compute to workload shape (steady, spiky, event-driven, batch).
3. Decide whether an organization should run Kubernetes at all.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-014-L01 | The compute spectrum | 10 |
| ARC-014-L02 | VMs and managed container platforms | 10 |
| ARC-014-L03 | Kubernetes: when it is worth it | 12 |
| ARC-014-L04 | Serverless functions | 12 |
| ARC-014-L05 | Matching compute to workload shape | 8 |
| ARC-014-L06 | Demo: compute choices for Larkspur's storefront, order processing, and nightly batch | 14 |

**Lab** — `ARC-014-LAB1` *Compute decisions:* compute choice per Larkspur workload with scaling behavior and operating model, recorded as ADRs. Acceptance: the team's skills and operating capacity are part of each decision.

**Common mistakes:** Kubernetes for a small team with simple workloads; serverless for long-running steady load.

**Assessment:** ADR review.

**Workplace evidence:** a compute platform decision you made with operating cost considered.

**Career relevance:** cost architecture (ARC-021).

---

### ARC-015 · Storage architecture
`n: 269` · **Video:** 58 min · **Practice:** 2.5 h

**Prerequisites:** ARC-012

**Learning outcomes** — the architect can:
1. Choose object, block, or file storage per use case.
2. Design backup strategy, retention, and immutability for ransomware resilience.
3. Apply lifecycle policies and storage tiers to control cost.
4. Protect stored data with encryption and access controls.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-015-L01 | Object, block, and file storage | 12 |
| ARC-015-L02 | Backups, retention, and immutability | 12 |
| ARC-015-L03 | Lifecycle policies and tiers | 10 |
| ARC-015-L04 | Securing stored data | 10 |
| ARC-015-L05 | Demo: storage design for product media, documents, and backups | 14 |

**Lab** — `ARC-015-LAB1` *Larkspur storage design:* storage types, lifecycle policies, backup and retention schedule, and encryption for product images, invoices, logs, and backups. Acceptance: retention meets requirements; backup copies are isolated from production credentials.

**Common mistakes:** backups in the same account with the same credentials; no lifecycle rules.

**Assessment:** design review.

**Workplace evidence:** a storage or backup design you implemented.

**Career relevance:** HA/DR (ARC-019) and data governance (ARC-030).

---

### ARC-016 · Database architecture
`n: 270` · **Video:** 68 min · **Practice:** 3.5 h

**Prerequisites:** SRC-007, ARC-012

**Learning outcomes** — the architect can:
1. Select managed relational, NoSQL, cache, and search services per workload.
2. Design replication, read scaling, and failover for each data store.
3. Define backup, point-in-time recovery, and disaster recovery for data stores.
4. Plan data migration from on-premises databases.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-016-L01 | Managed databases: what you still own | 10 |
| ARC-016-L02 | Selecting stores by workload | 12 |
| ARC-016-L03 | Replication, read scaling, failover | 12 |
| ARC-016-L04 | Backup, PITR, and DR for data | 10 |
| ARC-016-L05 | Migrating databases to the cloud | 10 |
| ARC-016-L06 | Demo: Larkspur's data stores and their failover design | 14 |

**Lab** — `ARC-016-LAB1` *Larkspur data platform:* data store per workload with replication, backup, recovery objectives, and the migration approach for the current web shop database. Acceptance: each store's RPO/RTO meets requirements or the gap is flagged.

**Common mistakes:** one database for everything; assuming managed means automatic DR.

**Assessment:** design review.

**Workplace evidence:** a data platform design you led to production.

**Career relevance:** data architecture (ARC-023).

---

### ARC-017 · Identity architecture
`n: 271` · **Video:** 87 min · **Practice:** 4 h

**Prerequisites:** MID-051, ARC-012

**Learning outcomes** — the architect can:
1. Design workforce identity: SSO, federation with the corporate directory, and MFA.
2. Design customer identity (CIAM): registration, social login, account recovery, and privacy.
3. Choose between SAML, OAuth 2.0, and OIDC for each integration and explain why.
4. Design cloud IAM for people and workloads with least privilege.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-017-L01 | Identity as the new perimeter | 8 |
| ARC-017-L02 | Workforce identity and SSO | 12 |
| ARC-017-L03 | Federation: SAML, OAuth 2.0, OIDC | 14 |
| ARC-017-L04 | Customer identity | 12 |
| ARC-017-L05 | Cloud IAM for people and workloads | 12 |
| ARC-017-L06 | Demo: Larkspur's identity architecture end to end | 15 |
| ARC-017-L07 | Demo: SSO for store staff into the new back office | 14 |

**Lab** — `ARC-017-LAB1` *Larkspur identity design:* workforce SSO for store and head-office staff, customer identity for web and mobile, partner access, and cloud IAM roles. Acceptance: protocol choice justified per integration; no shared accounts; break-glass access defined.

**Common mistakes:** building customer login in-house without need; long-lived access keys for workloads.

**Assessment:** identity design review.

**Workplace evidence:** an identity or SSO design you delivered.

**Career relevance:** identity and access (ARC-027) and security architecture (ARC-028).

---

### ARC-018 · Network security
`n: 272` · **Video:** 64 min · **Practice:** 3 h

**Prerequisites:** SRB-016, ARC-013

**Learning outcomes** — the architect can:
1. Layer network controls: security groups/NSGs, firewalls, WAF, DDoS protection.
2. Segment networks by sensitivity and environment.
3. Design private connectivity to SaaS and partners.
4. Explain where network controls complement, not replace, identity-based controls.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-018-L01 | Defense in depth for networks | 10 |
| ARC-018-L02 | Security groups, firewalls, and WAF | 12 |
| ARC-018-L03 | Segmentation | 10 |
| ARC-018-L04 | DDoS and edge protection | 10 |
| ARC-018-L05 | Private connectivity to SaaS and partners | 8 |
| ARC-018-L06 | Demo: protecting Larkspur's storefront and payment paths | 14 |

**Lab** — `ARC-018-LAB1` *Larkspur network security:* segmentation plan, WAF and DDoS posture for public endpoints, and controls around the payment flow. Acceptance: payment-related components isolated; every public endpoint protected.

**Common mistakes:** flat networks; relying on the network perimeter alone.

**Assessment:** security design review.

**Workplace evidence:** a network security design you implemented or reviewed.

**Career relevance:** security architecture (ARC-028).

---

### ARC-019 · High availability and DR
`n: 273` · **Video:** 83 min · **Practice:** 4 h

**Prerequisites:** SRC-013, SRB-004, ARC-012

**Learning outcomes** — the architect can:
1. Translate business impact into RPO and RTO per capability.
2. Choose multi-AZ and multi-region patterns (backup-restore, pilot light, warm standby, active-active) to meet them at acceptable cost.
3. Design DR for dependencies the solution doesn't own (ERP, payment provider, identity).
4. Define DR testing and evidence.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-019-L01 | Availability and recovery as business decisions | 10 |
| ARC-019-L02 | Multi-AZ design | 10 |
| ARC-019-L03 | DR patterns from backup-restore to active-active | 14 |
| ARC-019-L04 | Dependencies you don't own | 10 |
| ARC-019-L05 | Testing DR | 10 |
| ARC-019-L06 | Demo: costing three DR patterns for Larkspur's checkout | 15 |
| ARC-019-L07 | Demo: what happens to stores when the cloud region is down | 14 |

**Lab** — `ARC-019-LAB1` *Larkspur HA/DR design:* RPO/RTO per capability, chosen DR pattern with cost, dependency fallbacks (e.g., stores selling offline), and a DR test plan. Acceptance: targets met at a cost the sponsor accepts, or trade-off escalated.

**Common mistakes:** one RPO/RTO for everything; DR plans that ignore the ERP and payment provider.

**Assessment:** HA/DR design defense.

**Workplace evidence:** an HA/DR design you produced and tested.

**Career relevance:** resilience architecture (ARC-031).

---

### ARC-020 · Infrastructure governance
`n: 274` · **Video:** 66 min · **Practice:** 3 h · `version:` provider-specific

**Prerequisites:** MID-058, ARC-012

**Learning outcomes** — the architect can:
1. Design a landing zone: account/subscription hierarchy, baseline networking, logging, and security services.
2. Enforce guardrails with policies (preventive and detective).
3. Define tagging standards for ownership, cost, and data classification.
4. Require infrastructure as code with review for all environments.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-020-L01 | Why landing zones exist | 10 |
| ARC-020-L02 | Account and subscription hierarchies | 12 |
| ARC-020-L03 | Policy guardrails | 12 |
| ARC-020-L04 | Tagging standards | 8 |
| ARC-020-L05 | Infrastructure as code as governance | 10 |
| ARC-020-L06 | Demo: Larkspur's landing zone design | 14 |

**Lab** — `ARC-020-LAB1` *Larkspur landing zone:* hierarchy, guardrail policies, tagging standard, central logging, and IaC workflow. Acceptance: a non-compliant resource is blocked or detected in a walkthrough.

**Common mistakes:** guardrails added after workloads are live; tags without enforcement.

**Assessment:** landing zone review.

**Workplace evidence:** a landing zone or guardrail set you designed.

**Career relevance:** cost architecture (ARC-021) and compliance (ARC-029).

---

### ARC-021 · Cost architecture
`n: 275` · **Video:** 79 min · **Practice:** 3.5 h

**Prerequisites:** SRB-015, ARC-012

**Learning outcomes** — the architect can:
1. Size a solution and build a cost model from explicit pricing assumptions.
2. Estimate cost per business transaction (cost per order) and its sensitivity to volume.
3. Set budgets, alerts, and cost controls.
4. Present cost estimates with ranges and confidence levels.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-021-L01 | Cost as a design input | 8 |
| ARC-021-L02 | Sizing and pricing assumptions | 12 |
| ARC-021-L03 | Building a cost model | 12 |
| ARC-021-L04 | Unit cost and sensitivity | 10 |
| ARC-021-L05 | Budgets and controls | 8 |
| ARC-021-L06 | Demo: Larkspur's cloud cost model, line by line | 15 |
| ARC-021-L07 | Demo: what the cost does at peak season and at 3× growth | 14 |

**Lab** — `ARC-021-LAB1` *Larkspur cost model:* monthly cost by component for normal and peak months, cost per order, sensitivity to growth, and controls. Acceptance: every figure traceable to an assumption; range given, not a single number.

**Common mistakes:** forgetting data transfer and logging; estimates without peak months.

**Assessment:** cost model review with a role-played finance partner.

**Workplace evidence:** a cost estimate you produced that was later compared with actuals.

**Career relevance:** financial analysis (ARC-039).

---

### ARC-022 · Cloud architecture frameworks
`n: 276` · **Video:** 57 min · **Practice:** 3 h

**Prerequisites:** ARC-019, ARC-021

**Learning outcomes** — the architect can:
1. Explain the pillars of a well-architected framework (operational excellence, security, reliability, performance efficiency, cost optimization, sustainability).
2. Run a well-architected review on a design and prioritize findings.
3. Turn findings into a remediation plan with owners.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| ARC-022-L01 | Well-architected frameworks and their pillars | 12 |
| ARC-022-L02 | Running a review | 12 |
| ARC-022-L03 | Prioritizing findings | 10 |
| ARC-022-L04 | From findings to remediation | 8 |
| ARC-022-L05 | Demo: a well-architected review of Larkspur's design | 15 |

**Lab** — `ARC-022-LAB1` *Larkspur review:* well-architected review of the complete Larkspur infrastructure design with prioritized findings and a remediation plan. Acceptance: high-risk findings either fixed in the design or accepted by a named owner.

**Common mistakes:** treating the review as a one-time checkbox; fixing low-risk findings first.

**Assessment:** review report.

**Workplace evidence:** a well-architected review you ran and the improvements it produced.

**Career relevance:** architecture assurance (ARC-042).
