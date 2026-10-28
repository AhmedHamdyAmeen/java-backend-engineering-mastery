# Level 8 — Solution Architect: Interview Preparation

The questions most often asked when hiring Solution Architects, how to answer them, and where in this course you learned and practiced each one.

**How to use this guide**
1. Answer each question **out loud**, drawing on a whiteboard or paper where it helps. Architect interviews reward structured thinking you can show.
2. Always connect technology to **business requirements, risk, and cost**. A technically elegant answer that ignores them is a weak answer at this level.
3. Prepare one end-to-end solution story from real work and one from `ARC-CAP`.

> **About "How often":** frequencies reflect commonly reported interview patterns for Solution Architect roles, not measured statistics. Roles differ (pre-sales, delivery, enterprise); verify against current job posts and update this guide when the market moves.

---

## 1. What the market asks for — and where you proved it

| Skill employers list | Learned in | Proven by |
| --- | --- | --- |
| Requirements discovery with stakeholders | ARC-003, SRC-001 | `SRC-001-LAB1`, `ARC-CAP` requirements |
| End-to-end solution design | ARC-006, ARC-033 | `ARC-CAP` architecture package |
| Integration architecture | ARC-009, ARC-024, ARC-032 | `SRB-007-LAB1` CDC integration, `ARC-CAP` |
| Cloud architecture (AWS or Azure) | ARC-011 … ARC-022 | `MID-056-LAB1`, `MID-058-LAB1`, `ARC-CAP` |
| Identity and security architecture | ARC-017, ARC-027, ARC-028 | `SRB-016-LAB1`, `ARC-CAP` |
| HA, DR, resilience | ARC-019, ARC-031 | `SRC-013-LAB1`, `ARC-CAP` |
| Compliance and data governance | ARC-029, ARC-030 | `SRA-009-LAB1` |
| Cost, TCO, build/buy, vendors | ARC-008, ARC-021, ARC-039, ARC-040 | `SRA-008-LAB1`, `ARC-CAP` cost estimate |
| Architecture documentation | ARC-034, ARC-043 | `SRC-010-LAB1`, `ARC-CAP` ADRs and risk register |
| Presenting to executives | ARC-044, SRA-019 | `SRA-019-LAB1`, `ARC-CAP` executive presentation |

**Your portfolio at the end of Level 8:** the Enterprise Digital Commerce Platform architecture package (`ARC-CAP`) — requirements, C4 and deployment diagrams, integration and data architecture, security and cloud design, DR strategy, cost model, roadmap, ADRs, and risk register — plus real solutions you designed and saw delivered.

## 2. How Solution Architect interviews usually run

| Round | What happens | What they check | Prepare with |
| --- | --- | --- | --- |
| Hiring-manager screen | Background, solutions you designed | Breadth, delivery track record | Q14, your solution story |
| Case study / whiteboard design | Design a solution from a business scenario, often 60–90 min | Requirements first, options, trade-offs | Q1, Q2, Q14 |
| Cloud and infrastructure deep-dive | Networking, identity, HA/DR, cost | Depth on the chosen provider | Q4–Q7, Q9 |
| Integration and data | Connect to ERP, CRM, payments, legacy | Integration judgment | Q3, Q10 |
| Stakeholder / presentation | Present a design to a mixed audience | Communication, handling challenge | Q12, Q13 |
| Behavioral | Conflict, governance, delivery | Influence, pragmatism | Q11, Q13 |

---

## 3. Discovery and solution design

### Q1 · How do you gather requirements for a new solution when stakeholders disagree?
**How often:** Very common · **Round:** Screen, case study

**How to answer:**
- Identify stakeholders and their goals (business, operations, security, finance, users).
- Run workshops and interviews; capture functional requirements, **quality-attribute scenarios**, constraints, and assumptions separately.
- Make conflicts visible with their trade-offs; facilitate prioritization with the decision owner.
- Confirm in writing and keep a traceable link from requirements to design decisions.

**Common trap:** taking the first stakeholder's view as the requirement.

**Learned in:** ARC-003, ARC-041, SRC-001
**Practiced in:** `ARC-003-LAB1`, `ARC-041-LAB1`, `SRC-001-LAB1`, `ARC-CAP`
**Show it:** the ARC capstone's requirements and quality-attribute scenarios.

---

### Q2 · Design a digital commerce platform for a retailer that must integrate with its existing ERP.
**How often:** Very common · **Round:** Case study

**How to answer:** a repeatable structure the interviewer can follow.
1. **Clarify:** channels, volumes and peaks, regions, existing systems (ERP, CRM, payment providers), compliance (PCI DSS, privacy), budget, timeline, team skills.
2. **Quality attributes:** availability for checkout, latency, consistency of stock and orders, security.
3. **Options:** SaaS commerce platform vs packaged vs custom build — compare against requirements and cost.
4. **Context and containers (C4):** storefront, commerce services or SaaS, payment gateway, order management, ERP integration layer, identity provider, analytics.
5. **Integration:** events or APIs for orders and stock, batch for financial postings, anti-corruption layer around the ERP.
6. **Data:** ownership per domain, master data source (products and prices often from ERP).
7. **Infrastructure, security, DR, cost, roadmap:** briefly, then go deep where the interviewer wants.

**Common trap:** drawing services before asking a single question.

**Learned in:** ARC-006, ARC-033, ARC-032
**Practiced in:** `ARC-006-LAB1`, `ARC-033-LAB1`, `ARC-CAP`, `SRB-002-LAB1`
**Show it:** the ARC capstone package — this is the same scenario.

---

### Q3 · When would you integrate with synchronous APIs, events, batch files, or CDC?
**How often:** Very common · **Round:** Integration deep-dive

**How to answer:**
- **Synchronous API:** the caller needs an answer now (price check, payment authorization); accept coupling and design timeouts.
- **Events:** many consumers, eventual consistency acceptable, decoupled teams (order placed, stock changed).
- **Batch/file:** large volumes, legacy or partner constraints, scheduled processing (financial postings, partner feeds).
- **CDC:** the source system cannot be changed but its data must flow out in near real time.
- Mention reliability needs (idempotency, retries, DLQs), ownership of contracts, and monitoring.

**Common trap:** "events everywhere" or "REST everywhere".

**Learned in:** ARC-009, ARC-024, SRB-007
**Practiced in:** `ARC-009-LAB1`, `ARC-024-LAB1`, `SRB-007-LAB1`, `MID-029-LAB1`
**Show it:** the FulfillCo stock-sync integration built on CDC.

---

## 4. Cloud and infrastructure

### Q4 · How do you design a secure, highly available cloud architecture for a web application?
**How often:** Very common · **Round:** Cloud deep-dive

**How to answer:** walk the layers using Well-Architected pillars (operational excellence, security, reliability, performance efficiency, cost optimization, sustainability).
- Network: VPC/VNet with public subnets only for load balancers, private subnets for applications and databases, NAT for egress, private endpoints for managed services.
- Compute across **multiple availability zones** behind a load balancer; autoscaling.
- Managed database with multi-AZ standby, backups, and read replicas if needed.
- Edge: CDN and WAF; TLS everywhere.
- Identity: least-privilege roles for workloads; no long-lived keys.
- Observability, infrastructure as code, cost controls.

**Common trap:** listing services without explaining why each is there.

**Learned in:** ARC-012, ARC-013, ARC-022, MID-056
**Practiced in:** `ARC-012-LAB1`, `ARC-013-LAB1`, `MID-056-LAB1`, `MID-058-LAB1`, `ARC-CAP`
**Show it:** the cloud and network design in the ARC capstone.

---

### Q5 · Explain how you would set up SSO for employees and authentication for customers and APIs.
**How often:** Common · **Round:** Cloud / security deep-dive

**How to answer:**
- **Employees:** federate with the corporate identity provider using SAML or OIDC for SSO; enforce MFA; manage access by groups.
- **Customers:** a customer identity provider with OIDC; authorization code flow with PKCE for web and mobile.
- **APIs:** OAuth 2.0 access tokens validated by every API; client credentials for service-to-service; scopes and claims for authorization.
- Explain the difference: SAML and OIDC for *authentication/SSO*, OAuth 2.0 for *delegated authorization*.

**Common trap:** using ID tokens to call APIs or building a custom login system.

**Learned in:** ARC-017, ARC-027, JNR-039
**Practiced in:** `ARC-017-LAB1`, `ARC-027-LAB1`, `JNR-039-LAB1`, `MID-051-LAB1`
**Show it:** the identity architecture in the ARC capstone.

---

### Q6 · The business wants 99.99% availability and no data loss. How do you respond?
**How often:** Very common · **Round:** Cloud deep-dive, stakeholder

**How to answer:**
- Translate targets: 99.99% allows about 4.3 minutes of downtime a month; "no data loss" means RPO near zero.
- Ask which journeys need it — usually not all.
- Show options with cost: multi-AZ (often enough for 99.95–99.99%), multi-region active-passive (meets regional failure RPO/RTO of minutes), active-active (lowest RTO, highest cost and complexity).
- Include dependencies: the target cannot exceed what the payment provider and identity provider offer.
- Agree RPO/RTO per data set and prove them with DR drills.

**Common trap:** promising the number without discussing cost and dependencies.

**Learned in:** ARC-019, ARC-031, SRB-005
**Practiced in:** `ARC-019-LAB1`, `ARC-031-LAB1`, `SRC-013-LAB1`, `SRB-005-LAB1`
**Show it:** the availability calculation and DR strategy in the ARC capstone.

---

### Q7 · How would you estimate the cost of a cloud solution and keep it under control?
**How often:** Common · **Round:** Cloud deep-dive, executive

**How to answer:**
- Size from workload assumptions (requests, storage, data transfer, peaks), then price with the provider's calculator; state assumptions.
- Include often-missed items: data transfer, logging and monitoring, backups, support plans, non-production environments.
- Controls: tagging and cost attribution, budgets and alerts, rightsizing, autoscaling, commitments for steady load, storage lifecycle policies.
- Express cost in business units (cost per order).

**Common trap:** estimating compute only.

**Learned in:** ARC-021, ARC-039, SRB-015
**Practiced in:** `ARC-021-LAB1`, `ARC-039-LAB1`, `SRB-015-LAB1`, `ARC-CAP`
**Show it:** the ARC capstone's cost estimate and cost-per-order analysis.

---

## 5. Security, compliance, and governance

### Q8 · How do you build security and compliance into a solution from the start?
**How often:** Very common · **Round:** Security deep-dive

**How to answer:**
- Classify data; identify regulations (e.g., PCI DSS, GDPR, local laws) with compliance partners.
- Threat-model the design; apply zero-trust principles and defense in depth.
- Reduce scope: tokenize card data via the payment provider, segment networks, minimize personal data.
- Design for auditability (immutable logs), retention, and deletion across all stores.
- Include evidence for auditors in the architecture deliverables.

**Common trap:** treating compliance as a checklist after the design.

**Learned in:** ARC-028, ARC-029, SRA-009
**Practiced in:** `ARC-028-LAB1`, `ARC-029-LAB1`, `SRA-009-LAB1`, `MID-052-LAB1`
**Show it:** the marketplace compliance architecture and the ARC capstone's security section.

---

### Q9 · Build, buy, or SaaS? How do you evaluate vendors?
**How often:** Very common · **Round:** Case study, executive

**How to answer:**
- Start with whether the capability differentiates the business.
- Define weighted criteria before looking at vendors: functional fit, integration, security and compliance, scalability, TCO over 3–5 years, vendor viability, exit cost.
- Use RFI/RFP for structured comparison and a time-boxed proof of concept on the riskiest assumptions.
- Check SLAs, data ownership, and contract terms with procurement and legal.

**Common trap:** choosing from vendor demos.

**Learned in:** ARC-008, ARC-040, SRA-008
**Practiced in:** `ARC-008-LAB1`, `ARC-040-LAB1`, `SRA-008-LAB1`, `SRB-013-LAB1`
**Show it:** the ARC capstone's build-vs-buy analysis.

---

### Q10 · How would you modernize a legacy system? Explain the options.
**How often:** Very common · **Round:** Case study

**How to answer:**
- Describe the common "R" options: **retain**, **retire**, **rehost** (lift and shift), **replatform** (small changes to use managed services), **refactor/re-architect**, **replace** (often with SaaS). (Some frameworks also list repurchase and relocate.)
- Choose per component by business value, technical condition, risk, and cost.
- Migrate incrementally (strangler fig), keep systems coexisting, plan data migration and cutover with rollback.

**Common trap:** a big-bang rewrite plan.

**Learned in:** ARC-010, ARC-037, SRB-008
**Practiced in:** `ARC-010-LAB1`, `ARC-037-LAB1`, `SRB-008-LAB1`, `SRB-017-LAB1`
**Show it:** the FulfillCo extraction and the ARC capstone migration plan.

---

### Q11 · What deliverables do you produce for a solution, and how do you take it through an architecture review board?
**How often:** Common · **Round:** Screen, behavioral

**How to answer:**
- Deliverables: requirements and quality scenarios, high-level design (C4 context/container, deployment, integration views), low-level designs where risk demands, interface contracts, ADRs, risk register, cost estimate, roadmap.
- Review board: understand its principles and standards in advance; pre-review with key reviewers; present decisions with alternatives; handle exceptions with a documented rationale and expiry.

**Common trap:** documents nobody reads; arriving at the board unprepared for known objections.

**Learned in:** ARC-034, ARC-035, ARC-043
**Practiced in:** `ARC-034-LAB1`, `ARC-035-LAB1`, `SRC-010-LAB1`, `SRB-012-LAB1`, `ARC-CAP`
**Show it:** the ARC capstone's architecture pack and decision log.

---

## 6. Communication and stakeholders

### Q12 · Present your solution to executives in five minutes.
**How often:** Common · **Round:** Stakeholder presentation

**How to answer:**
- Business problem and goal in one sentence.
- Recommendation and why it is the right option (two or three reasons tied to business value).
- Cost, timeline, and main risks with mitigations.
- What you need from them.
- Keep architecture diagrams to one context view; keep detail for questions.

**Common trap:** starting with the technology stack.

**Learned in:** ARC-044, SRA-019
**Practiced in:** `ARC-044-LAB1`, `SRA-019-LAB1`, `ARC-CAP`
**Show it:** the ARC capstone's executive presentation.

---

### Q13 · Tell me about a time requirements conflicted — for example, security against time to market.
**How often:** Very common · **Round:** Behavioral

**How to answer (STAR, architect emphasis):**
- **Situation:** the conflicting requirements and who held each.
- **Action:** made the trade-off explicit with options, risks, and costs; involved the decision owner; found a design that met the essential part of both (e.g., launch with reduced scope behind a compensating control).
- **Result:** the outcome, how risk was tracked, and the relationship afterwards.

**Common trap:** a story where you simply sided with one stakeholder.

**Learned in:** ARC-041, SRA-015, SRA-013
**Practiced in:** `ARC-041-LAB1`, `SRA-015-LAB1`, `ARC-CAP`
**Show it:** a real trade-off you mediated, and the ARC gate's changing-priorities scenario.

---

### Q14 · Walk me through a solution you designed end to end.
**How often:** Asked in almost every interview · **Round:** Screen, deep-dive

**How to answer (8–10 minutes):**
1. Business context and goals.
2. Requirements and constraints that shaped the design.
3. Options considered and why you chose this one.
4. Architecture: context, key containers, integrations, data, security, infrastructure.
5. Delivery: roadmap, migration, how you worked with teams.
6. Outcome: measurable results and what you would change.

**Common trap:** describing what was built without your decisions.

**Learned in:** ARC-006, ARC-043
**Practiced in:** `ARC-006-LAB1`, `ARC-043-LAB1`, `ARC-CAP`
**Show it:** one real solution and the ARC capstone, each with diagrams ready.

---

## 7. Six-week preparation plan

| Week | Focus | Do this |
| --- | --- | --- |
| 1 | Your solutions | Prepare Q14 for two real solutions and `ARC-CAP`, with one diagram each |
| 2 | Case studies | Three timed whiteboard cases in the style of Q2 (commerce, logistics, banking) |
| 3 | Cloud depth | Q4–Q7 for your chosen provider; review its Well-Architected framework |
| 4 | Integration and modernization | Q3, Q10; draw integration views for a legacy ERP scenario |
| 5 | Security, cost, governance | Q8, Q9, Q11; rebuild the capstone's cost estimate from scratch |
| 6 | Communication and mocks | Q12, Q13; two full mock loops including an executive presentation |

**Ready when:** you can take an unfamiliar business scenario to a defensible design in 60 minutes while asking the right questions first, explain every component's purpose and cost, and present the result to a non-technical audience in five minutes.
