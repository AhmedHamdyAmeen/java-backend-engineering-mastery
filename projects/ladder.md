# Project Ladder

One evolving business domain — **commerce** — carried from a console app to an enterprise solution, so learners see the same product change as traffic, requirements, and team size grow. The Beginner project uses a library domain, deliberately small, to teach the same modeling skills before commerce begins.

| # | Project | Level | Core technologies | Outcome |
| --- | --- | --- | --- | --- |
| 01 | Library Management System | BEG | Java, OOP, collections, SQL, JDBC | Working command-line application |
| 02 | E-Commerce REST API | JNR | Spring Boot, PostgreSQL, JPA, Security, Docker | Deployed backend with tests and documentation |
| 03 | Distributed Commerce Platform | MID | Kafka, Redis, messaging, resilience, Kubernetes | Observable multi-service application |
| 04 | Reliability & Performance Redesign | SRC | SLOs, performance, recovery, failure analysis | Measured improvements and runbooks |
| 05 | Architecture Modernization | SRB | Migration, event contracts, zero-downtime delivery | Phased architecture migration |
| 06 | Multi-Year Platform Evolution | SRA | Architecture strategy, cost, governance | Technical strategy and roadmap |
| 07 | Internal Developer Platform | STF | Platform engineering, influence, adoption | Platform design and organizational rollout |
| 08 | Enterprise Commerce Solution | ARC | Business architecture, cloud, integration, risk | Complete solution architecture package |

Each project brief below lists **required** criteria (all must be met to pass) and **stretch** criteria (count toward a higher rubric score). All eight briefs are complete.

---

## 01 — Library Management System (`BEG-CAP`)

**Uses:** BEG-001 … BEG-055 · **Effort:** 30–40 h

A console application for a small library to manage books, members, and loans, backed by PostgreSQL.

**Required**
1. Register, update, and list books (title, ISBN, authors, copies) and members.
2. Borrow and return books, enforcing rules: a member may hold at most 5 books; no loan if the member has overdue books; a copy cannot be lent twice.
3. Overdue detection with a configurable loan period and fine calculation.
4. Search and filter books by title, author, and availability; list a member's loans.
5. Persistence in PostgreSQL via JDBC (`BEG-055`) using a schema script with constraints; credentials read from environment variables.
6. Business rules enforced in domain classes, raising custom exceptions with user-friendly messages.
7. At least 25 JUnit tests covering the borrowing rules and their boundaries.
8. Maven build; `mvn test` passes on a clean checkout.
9. Public Git repository with meaningful commit history and a README: purpose, setup (DB + env vars), usage, and a class diagram.

**Required — AI (BEG-056, BEG-057)**
1. An `AI-USE.md` file listing where an AI assistant helped, what it suggested, and how each suggestion was verified (read, traced, tested) — or stating that none was used.
2. At least one AI-suggested piece of code that you rejected or corrected, with the reason.

**Stretch**
- Export reports (overdue list, popular books) to CSV.
- Reservation queue for unavailable books (`Queue`).
- Repository interface with both in-memory and JDBC implementations, the in-memory one used in unit tests.

**Graduation gate (live, ~45 min)**
1. Explain the architecture: packages, key classes, and why responsibilities sit where they do.
2. Debug a bug the assessor plants, using the debugger.
3. Write three SQL queries the assessor asks for, against the capstone database.
4. Implement a small new requirement (e.g., "members can renew a loan once") with tests.

---

## 02 — E-Commerce REST API (`JNR-CAP`)

**Uses:** JNR-001 … JNR-054 · **Effort:** 60–80 h on top of the phase labs, which already build most of it (*Shop Core* in JNR-P1, *Shop API* from JNR-P2 onward)

**Architecture:** modular layered monolith, packaged by feature (`catalog`, `inventory`, `cart`, `orders`, `payments`, `users`), with controller → service → repository layers inside each feature and DTOs at the HTTP edge.

**Required — functional**
1. Registration and login; tokens issued by Keycloak or the application, validated as a resource server (JNR-038/039).
2. Product catalog: CRUD for admins; public paginated, sortable, filterable listing with capped page size.
3. Inventory: stock per product; stock can never go negative, even under concurrent orders (constraint plus test).
4. Cart: add, update quantity, remove, view totals with discounts and tax from Shop Core.
5. Orders: checkout creates the order and reserves stock in one transaction; status lifecycle `PLACED → PAID → SHIPPED`, or `CANCELLED` (which releases stock).
6. Mock payment provider behind an interface, with success, decline, and timeout behavior; no remote call inside a database transaction.
7. Customers see only their own carts and orders (ownership checks, IDOR tests); admin endpoints restricted by role.
8. Validation and consistent RFC 9457 Problem Details errors for 400, 401, 403, 404, 409, and 500.

**Required — engineering**
1. OpenAPI document with examples and error responses, served by Swagger UI and committed to the repository.
2. Flyway migrations; `ddl-auto=validate`; no N+1 queries on listing endpoints (query-count test).
3. Unit, slice, and Testcontainers integration tests, including the checkout journey matrix (JNR-046).
4. `docker compose up` starts the full stack with seed data.
5. GitHub Actions pipeline: build and full test suite on every PR, branch protection, tagged image published on merge.
6. Deployed instance with health checks, configured only by environment variables, and a documented rollback.
7. Structured logs with no secrets or personal data.
8. `SECURITY.md` listing the threat list and every control (from JNR-035 and JNR-042).
9. README: architecture overview diagram, local setup, configuration reference, and API usage.

**Required — AI (JNR-055 … JNR-057)**
1. One LLM feature in Shop API — e.g., natural-language product search or product-description drafting for admins — behind an interface, with a fake implementation used in all tests.
2. Timeouts, a per-request token budget, and graceful behavior when the model is unavailable.
3. Prompt-injection and output-handling defenses documented in `SECURITY.md`, with at least two tests.
4. `AI-USE.md` describing how AI assistants were used during development and how their output was reviewed.

**Stretch**
- Product image upload and download with limits (JNR-023).
- `ETag`-based conditional GET on products (JNR-017).
- Admin sales report endpoint built with Spring JDBC (JNR-026).
- Dependency vulnerability scanning failing the build on high severity.

**Graduation gate (live, ~90 min)**
1. The assessor gives an unseen feature request (e.g., "customers can apply a one-time coupon code at checkout").
2. The learner clarifies requirements, implements the feature within the existing architecture, writes meaningful tests, and adds a migration.
3. The learner opens a pull request with a description a reviewer can act on, and explains the database changes and any trade-offs.
4. Scored with the JNR weights in [`assessment/framework.md`](../assessment/framework.md).

---

## 03 — Distributed Commerce Platform (`MID-CAP`)

**Uses:** MID-001 … MID-066 · **Effort:** 80–100 h on top of the phase labs, which build most of it (*Shop Platform* from MID-P1 onward)

**Architecture:** start from the hexagonal modular monolith (MID-059) and extract services only where the split ADR (MID-061) justifies it — expected: `catalog`, `orders`, `inventory`, `payments`, plus `search` and `notifications` as supporting services, behind an API gateway. Each service owns its data; Kafka carries business events.

**Required — functional**
1. Order saga: place order → reserve stock → authorize payment → confirm, with compensations for decline and timeout (MID-031).
2. Inventory reservation that never oversells under concurrent load (MID-015).
3. Catalog cache in Redis with event-driven invalidation and stampede protection (MID-039, MID-040).
4. Product search fed by catalog events (MID-043).
5. Authentication at the gateway and token validation in every service; service-to-service calls use their own credentials (MID-051).

**Required — engineering**
1. Transactional outbox in every event-producing service and idempotent consumers everywhere (MID-029); a chaos script that kills services mid-flow loses and duplicates nothing.
2. Timeouts, retries with backoff and jitter, circuit breakers, and DLQs/DLTs on every remote interaction (MID-033).
3. Consumer-driven contracts for HTTP and events, enforced in CI; event schemas in a registry (MID-045, MID-062).
4. OpenTelemetry tracing across HTTP and Kafka; logs correlated by trace ID; per-service and business dashboards (MID-047, MID-048).
5. SLOs with burn-rate alerts for checkout and search (MID-049).
6. Load test report with percentiles and the identified bottleneck (MID-046).
7. Deployed on Kubernetes with probes, limits, and autoscaling; infrastructure in Terraform; promotion pipeline with automatic rollback (MID-055, MID-057, MID-058).
8. SBOMs, image scans, and secrets in a secrets manager (MID-053, MID-054).
9. Documentation: C4 diagrams, saga sequence diagrams, ADRs (including datastore choices), runbooks for every alert, and a recovery procedure for database loss tested once (MID-018, MID-063).

**Required — AI (MID-067 … MID-072)**
1. A RAG order-support assistant answering customer questions about orders and policies, with citations, over pgvector-indexed documents kept fresh by events (MID-067, MID-068).
2. Read-only, authorized tools (e.g., order-status lookup) and a human-approval step for any action with side effects (MID-069).
3. An evaluation set run in CI with a quality threshold, plus token, latency, and cost dashboards (MID-070).
4. Injection and data-exfiltration tests, including indirect injection through retrieved content (MID-071).

**Stretch**
- Reviews service on MongoDB with a datastore ADR (MID-042, MID-044).
- Virtual threads for I/O-bound services with before/after evidence (MID-007).
- Monthly partitioned order history with zero-downtime migration (MID-019, MID-020).
- Read model for the admin dashboard with jOOQ (MID-022).

**Graduation gate (live, ~2 h)**
1. **Incident simulation (45 min):** the assessor injects a fault into the running platform (e.g., a consumer stuck on a poison message, connection-pool exhaustion, a misconfigured retry storm). The learner leads triage using telemetry, mitigates, and later submits a postmortem.
2. **Performance improvement (45 min):** given a load test showing an SLO breach on one endpoint, the learner profiles, identifies the bottleneck, fixes it, and shows before/after measurements.
3. **Architecture defense (30 min):** the learner defends service boundaries, consistency choices, and the datastore decisions, including what they would *not* split and why.
4. Scored with the MID weights in [`assessment/framework.md`](../assessment/framework.md).

## 04 — Reliability & Performance Redesign (`SRC-CAP`)

**Uses:** SRC-001 … SRC-020 · **Effort:** 50–70 h on top of the phase labs, which build most of the evidence

**Scenario — *Order Processing at 10×*:** the business forecasts 10× order volume within 18 months, has committed to 99.95% monthly availability for checkout, and requires recovery from a regional database failure within 15 minutes with at most 1 minute of order data loss. The engineer owns the order subsystem (`orders`, `inventory` reservation, `payments` integration, and their data) and must redesign it to meet these targets.

**Required — design**
1. Requirements document with constraints, assumptions, and at least eight measurable quality-attribute scenarios (SRC-001).
2. Prioritized utility tree and tactics (SRC-002).
3. Capacity plan and performance model for 10× load, with the first three bottlenecks named (SRC-004, SRC-005).
4. At least three options evaluated; ADRs for the data-scaling, decomposition, and failover decisions (SRC-003, SRC-007, SRC-008).
5. FMEA with dependency map and graceful-degradation design (SRC-009).
6. Compatibility policy and migration plan for any contract change the redesign requires (SRC-006).

**Required — evidence**
1. Load test at the 10× forecast showing checkout p99 within its SLO, with before/after comparison (SRC-016).
2. SLOs, error-budget policy, and burn-rate alerts in place and tested (SRC-012).
3. Failure-injection tests for the top five FMEA risks, run in CI or on a schedule (SRC-009).
4. Timed DR drill meeting RTO 15 min and RPO 1 min, or a documented gap with a funded plan (SRC-013).
5. Reconciliation job between orders, payments, and the provider with an audit trail (SRC-014).
6. Canary rollout of the redesign with automated rollback (SRC-011).
7. Secure design review completed with a peer, findings closed or accepted by an owner (SRC-018).
8. Debt register with the next quarter's paydown plan (SRC-017).

**Required — handover**
1. Architecture pack for engineers, operators, and leadership (SRC-010).
2. Runbooks for every alert, each executed once by someone other than the author.
3. A 30-minute operational handover to an incoming owner (role-played), recorded.

**Required — AI (SRC-021, SRC-022)**
1. The order-support assistant meets explicit latency, cost-per-conversation, and availability targets, with fallbacks for a provider outage (SRC-021).
2. Prompt and model versions are released behind evaluation gates and can be rolled back; one bad-output incident is simulated and handled (SRC-022).

**Stretch**
- Performance regression check in CI catching a seeded regression.
- Mentoring a Mid learner through one component of this capstone (SRC-020).

**Graduation gate (scenario-based, ~3 h)**
1. **Design review (60 min):** present the redesign to a panel playing product, operations, and security; the panel introduces a new constraint (e.g., budget cut by 30% or a data-residency requirement) and the engineer adapts the design live.
2. **Incident command (45 min):** lead a multi-team simulated outage of the order subsystem as incident commander (SRC-019), then outline the postmortem.
3. **Troubleshooting (45 min):** diagnose a layered production fault from telemetry alone (SRC-015).
4. **Mentoring evidence (15 min):** discuss feedback from a mentee.
5. Scored with the SRC weights in [`assessment/framework.md`](../assessment/framework.md).

**Beyond the course:** the Senior C certificate records the capstone as *demonstrated in training*. Role readiness also requires the **workplace evidence** listed in each SRC module — for example, a launch you led, an incident you commanded, and an engineer you mentored.

## 05 — Architecture Modernization (`SRB-CAP`)

**Uses:** SRB-001 … SRB-020 · **Effort:** 60–80 h on top of the phase labs, which produce most of the artifacts

**Scenario — *The FulfillCo integration*:** Shop Platform's company has acquired FulfillCo, whose warehouse and fulfillment system is a 10-year-old Java modular monolith on one PostgreSQL database, exchanging nightly CSV files with partners. The business needs real-time stock and shipment status in Shop within six months, EU warehouses with EU data residency within a year, and no downtime for either business. Four teams are involved (Shop orders, FulfillCo warehouse, FulfillCo shipping, Platform). The engineer is the technical lead for the program and leads a simulated migration of the FulfillCo monolith to selected, independently deployable services.

**Required — architecture**
1. Target architecture with the chosen patterns justified in ADRs (event sourcing or not, workflow engine or not) (SRB-001, SRB-013).
2. Shop ↔ FulfillCo event catalog with owners, schemas, compatibility rules, and replay policy (SRB-002).
3. CDC-based integration of the legacy database with translation to domain events; no change to legacy code for phase one (SRB-007).
4. Regional topology meeting EU residency, with failover design and composite availability calculation (SRB-004, SRB-005).
5. Messaging design for the partner tracking feed at 50× Shop's order volume with lag alerts and a backlog-recovery plan (SRB-006).
6. Merged identity and service-to-service authorization model with no network-location-based trust (SRB-016).

**Required — migration and delivery**
1. Phased migration plan (strangler fig + branch by abstraction) with per-phase rollback, exit criteria, and no dual writes (SRB-008).
2. Phase one executed: feature flags, shadow comparison with measured mismatch rate, backfill, cut-over, and legacy path decommissioned (SRB-017).
3. Compatibility guarantees: contract tests and schema registry rules prevent consumer breakage at every phase.
4. Observability across both systems: traces through CDC and events, migration dashboards (old vs new path), SLOs for the integrated flow.
5. Golden-path template used by at least one new FulfillCo service (SRB-010).

**Required — leadership**
1. Cross-team dependency map and interface agreements, with one recorded design session (SRB-011).
2. RFC and review process run for at least two decisions (SRB-012).
3. Risk register with contingencies; one risk triggered by the assessor and handled (SRB-019).
4. DORA and reliability dashboard for the program with one improvement experiment (SRB-014).
5. Cost-per-order analysis before and after integration (SRB-015).
6. Biweekly status reports and a final outcomes report against the measurable goals (SRB-020).

**Required — AI (SRB-021, SRB-022)**
1. A shared LLM gateway used by at least two of the four teams, with quotas, redaction of personal data, cost attribution per team, and model routing (SRB-021).
2. A rollout plan for AI coding assistants across the program with policy and an honest impact measure (SRB-022).

**Stretch**
- Service mesh trial with adopt/reject ADR (SRB-009).
- Second migration phase planned in detail with updated risk register.

**Graduation gate (scenario-based, ~3 h)**
1. **Migration review (60 min):** present the program to a panel of role-played team leads, product, finance, and security. Midway, a new constraint arrives (e.g., a partner requires API access in eight weeks, or the FulfillCo shipping team loses two engineers). The engineer re-plans live.
2. **Stakeholder negotiation (45 min):** two team leads disagree on ownership of the stock ledger; facilitate to a committed decision (SRB-018).
3. **Executive update (30 min):** deliver a status update with bad news and options to role-played executives (SRB-020).
4. **Outcomes defense (30 min):** show the measured results of phase one against its exit criteria.
5. Scored with the SRB weights in [`assessment/framework.md`](../assessment/framework.md).

**Beyond the course:** Senior B role readiness also requires the **workplace evidence** listed in each SRB module — in particular, a cross-team design led to agreement and a migration carried through to decommissioning.

## 06 — Multi-Year Platform Evolution (`SRA-CAP`)

**Uses:** SRA-001 … SRA-020 · **Effort:** 60–80 h on top of the phase labs, which produce most of the inputs

**Scenario — *Commerce 2030*:** the group formed by Shop and FulfillCo has 25 engineering teams. Over three years it will launch a third-party seller marketplace, expand to five countries, and double order volume each year, while its earliest services and frameworks approach end of life. The engineer is the senior technical leader for the commerce product area and produces its three-year architecture evolution strategy — and gets it adopted.

**Required — strategy package**
1. Current-state landscape: systems, teams, platforms, shared capabilities, and coordination hot spots (SRA-001).
2. Strategic domain model: subdomains, context map, and build/buy stance per subdomain (SRA-003).
3. Diagnosis, guiding policies, coherent actions, and investment split between platform and product work (SRA-010).
4. Capacity assumptions: three-year forecast and workload model with cost per order at target latency and sensitivity to growth (SRA-007).
5. Modernization sequencing: target and transition architectures per year, obsolescence calendar, and fitness functions that guard the direction (SRA-002).
6. Regional strategy for five countries with per-capability consistency decisions and residency mapping (SRA-005).
7. Security and reliability objectives: SLO targets per journey, resilience posture and chaos program, privacy and compliance architecture for the marketplace (SRA-006, SRA-009).
8. Data ownership map and data contracts for the most-used data sets (SRA-004).
9. Cost estimates per year with at least one build-vs-buy analysis and five-year TCO (SRA-008).
10. Governance: engineering standards with exception process, review practice, and decision records with explicit assumptions (SRA-012, SRA-013, SRA-017).

**Required — adoption**
1. Technical vision document, one-page summary, and engineering talk (SRA-011).
2. Team-boundary proposal aligned with the context map, reviewed with engineering managers (SRA-018).
3. Joint plan for the marketplace launch signed off by product, finance, security, and legal role-players (SRA-015).
4. Capability development plan tied to the strategy's actions (SRA-016).
5. Succession plan for three critical areas, including the engineer's own (SRA-020).
6. Executive funding pitch for year one (SRA-019).

**Required — AI (SRA-021, SRA-022)**
1. An AI strategy section: where AI creates value in commerce, build vs buy per use case, hosted vs open-weight choices, and three-year cost (SRA-021).
2. Responsible-AI controls for the marketplace: transparency to sellers and customers, human oversight, privacy and residency of model calls, auditability (SRA-022).

**Stretch**
- A quarterly strategy review template with leading indicators for each guiding policy.
- A one-page "what we will not do" list with reasons.

**Graduation gate (scenario-based, ~3 h)**
1. **Strategy defense (60 min):** present the strategy to a panel playing CTO, CFO, VP Product, and Head of Security. Midway, the panel changes a premise (e.g., a competitor launches a marketplace first and the timeline halves, or budget is cut by 25%). The engineer revises priorities live and explains what is dropped.
2. **Executive pitch (20 min):** secure funding for year one in a fixed slot.
3. **Architecture review (40 min):** review a team's design that conflicts with the strategy; separate blocking issues from preferences and reach an agreement.
4. **Organizational design discussion (30 min):** defend the team-boundary proposal with role-played engineering managers.
5. Scored with the SRA weights in [`assessment/framework.md`](../assessment/framework.md).

**Beyond the course:** Senior A role readiness also requires the **workplace evidence** listed in each SRA module — in particular, a technical strategy that guided real investment and an area you handed over that continued without you.

## 07 — Internal Developer Platform (`STF-CAP`)

**Uses:** STF-001 … STF-020 · **Effort:** 70–90 h on top of the phase labs, which produce most of the inputs

**Scenario — *Platform 2.0*:** the Commerce group (Shop + FulfillCo) now has about 20 product teams. Delivery has slowed, every team maintains its own pipelines and tooling, the same incidents repeat across teams, and onboarding a new engineer takes weeks. As a Staff engineer, the learner identifies the organization-wide problems and designs, gets funded, and rolls out an internal developer platform for 10–20 product teams. **The assessment weighs organizational leverage over code quality.**

**Required — diagnosis and strategy**
1. Evidence-based diagnosis of the top organization-wide problems (delivery metrics, incident patterns, developer survey, onboarding time) (STF-002, STF-009, STF-019).
2. Technical strategy for the platform: guiding policies, what the platform will and will not do, and investment over two years (STF-002, STF-004).
3. Technology portfolio decisions: what to standardize, consolidate, adopt, and retire (STF-007).

**Required — platform design**
1. Platform architecture with clear boundaries between platform and product teams (STF-004, STF-006).
2. Self-service deployment model: from template to production without tickets (STF-004).
3. CI/CD standards, observability standards, and security guardrails as paved roads with documented exceptions (STF-003, STF-005, STF-008).
4. Service templates (at least one working golden path, reusing `SRB-010-LAB1` if available).
5. Reliability program built into the platform: SLO defaults, incident process, shared runbooks (STF-005, STF-018).
6. Cost model: platform team cost, infrastructure cost, and expected savings per product team (STF-010, STF-019).

**Required — adoption and governance**
1. RFC for the platform, reviewed by role-played team leads and approved through the governance process (STF-003, STF-012).
2. Adoption roadmap with early adopters, migration support, incentives, and handling of resistance (STF-013, STF-014).
3. Governance process: decision rights, standards lifecycle, and exception handling (STF-003, STF-016).
4. Success metrics with baselines and targets (DORA, onboarding time, incident repeat rate, developer satisfaction, cost) (STF-019).
5. Capability plan: platform champions, documentation, and a community of practice (STF-015).
6. Executive business case and quarterly update format (STF-017).

**Required — AI (STF-021, STF-022)**
1. AI governance for the platform: approved tools, usage policy, evaluation standards for AI features, and guardrails offered as paved roads (STF-021).
2. An AI adoption program for the product teams with enablement, risk controls, and outcome metrics (STF-022).

**Stretch**
- A technical due-diligence report on one team's stack recommending platform migration or not (STF-010).
- A personal Staff promotion packet drafted from the capstone and real work (STF-020).

**Graduation gate (scenario-based, ~3 h)**
1. **Platform RFC review (60 min):** defend the RFC to a panel of skeptical role-played team leads and an engineering director; one team refuses to adopt. Negotiate without authority (STF-011).
2. **Executive business case (20 min):** secure funding for the platform team in a fixed slot (STF-017).
3. **Org-scale design (40 min):** an unseen organization-wide problem (e.g., a third of services lack on-call coverage) — diagnose, propose leverage, and define how you would measure success.
4. **Impact deep-dive (30 min):** walk through real organizational impact from your work with evidence.
5. Scored with the STF weights in [`assessment/framework.md`](../assessment/framework.md).

**Beyond the course:** Staff role readiness requires demonstrated organizational impact — the **workplace evidence** in each STF module. The capstone shows Staff-level reasoning; only real work shows Staff-level results.

## 08 — Enterprise Digital Commerce Platform (`ARC-CAP`)

**Uses:** ARC-001 … ARC-044 · **Effort:** 80–100 h on top of the phase labs, which produce most of the package

**Scenario — *Larkspur Retail* (fictional):** a mid-size retailer with 120 stores and a dated on-premises web shop needs a platform for web and mobile customers, inventory, payments, order fulfillment, customer service, and reporting, integrated with its existing ERP and CRM. The learner is the solution architect and produces a complete solution architecture package, then defends it.

**Required — architecture package**
1. Business context: capabilities, value streams, stakeholders (ARC-002).
2. Business requirements and quality-attribute scenarios, with conflicts and assumptions recorded (ARC-003).
3. Context, container, component, and deployment diagrams (C4 plus deployment and integration views) (ARC-005, ARC-034).
4. Application and integration architecture: APIs, events, batch, and CDC choices per interface, including ERP, CRM, payment gateway, and identity provider (ARC-009, ARC-024, ARC-026, ARC-032).
5. API management approach (ARC-025).
6. Data architecture and ownership model: operational vs analytical, lifecycle, governance (ARC-023, ARC-030).
7. Identity, security, and compliance architecture: customer and workforce identity, zero trust, PCI DSS scope reduction, privacy and data residency (ARC-017, ARC-027, ARC-028, ARC-029).
8. Cloud infrastructure and network design on the chosen provider: compute, storage, database, network segmentation, landing zone and governance (ARC-012 … ARC-020).
9. Availability, scalability, and disaster-recovery strategy with RPO/RTO per capability (ARC-019, ARC-031).
10. Cost estimate and build-vs-buy-vs-SaaS analysis with TCO, plus vendor evaluation for at least one component (ARC-008, ARC-021, ARC-039, ARC-040).
11. Assessment against Well-Architected pillars (ARC-022).
12. Delivery roadmap and migration plan from the legacy web shop, including cutover, coexistence, rollback, and data migration (ARC-010, ARC-036, ARC-037).
13. Operational architecture: monitoring, support model, incident process, service ownership (ARC-038).
14. Architecture decision records and risk register; solution options with a decision matrix (ARC-033, ARC-043).
15. Executive presentation and technical design pack (ARC-044).

**Required — governance**
1. Architecture principles for the program (ARC-007).
2. Passage through a simulated architecture review board, with conditions closed (ARC-035, ARC-042).
3. Stakeholder map and engagement plan (ARC-041).

**Required — AI (ARC-045 … ARC-047)**
1. AI customer-service assistant for Larkspur Retail: reference architecture over order, product, and policy data, integrated with CRM (ARC-045).
2. AI security, privacy, and compliance architecture: prompt-data classification, residency, vendor terms, guardrails, audit (ARC-046).
3. AI vendor and model evaluation with own evaluation results, total cost, and exit plan (ARC-047).

**Stretch**
- A second solution option fully costed for comparison (e.g., SaaS commerce suite vs custom build).
- A 90-day transition plan for handing the solution to delivery teams.

**Graduation gate (simulated architecture review, ~3 h)**
1. **Design defense (60 min):** present to a board playing CIO, CFO, head of security, head of stores, and the ERP vendor.
2. **Competing requirements (30 min):** marketing wants launch in four months; security requires a PCI assessment first — reconcile.
3. **Budget constraint (30 min):** budget is cut by 30% — show what changes and what risk is accepted.
4. **Changing priorities (20 min):** the business adds marketplace sellers — show impact on the architecture.
5. **Failure scenarios (30 min):** walk through a regional outage, an ERP outage on Black Friday, and a payment-provider failure.
6. Scored with the ARC weights in [`assessment/framework.md`](../assessment/framework.md).

**Beyond the course:** architect role readiness requires real solution delivery — the **workplace evidence** in each ARC module.
