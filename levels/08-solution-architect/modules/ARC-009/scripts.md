# ARC-009 · Enterprise integration — Lecture scripts

**Video:** 87 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-009-L01 · Integration is where projects fail (8 min)
**Goal:** explain why integration is the main risk in enterprise programs.

**Key points**
- Every system has its own data model, timing, availability, and owner.
- Hidden integrations and undocumented file drops surface late.
- Failures cross boundaries: one slow system can stall many.
- Integration needs design, ownership, testing, and monitoring like any product.

**Show:** a Larkspur "integration iceberg": visible APIs above the line; below, spreadsheets emailed to finance, nightly files, a store script writing to a shared folder.

**Check:** Why do integrations fail late? *(Hidden dependencies and unclear ownership appear only when systems are connected.)*

---

## ARC-009-L02 · APIs and events (10 min)
**Goal:** compare request-response APIs with event-driven integration.

**Key points**
- Synchronous API: caller waits for an answer; simple, immediate, but couples availability.
- Events: a system publishes a fact (order placed); consumers react later; looser coupling and replay.
- Use APIs for queries and commands needing an immediate answer; events for notifications and propagation of facts.
- Events bring ordering, duplicates, and eventual consistency to handle.

**Show:** two flows for stock updates: store scan calls an API versus store scan emits "stock-adjusted" event consumed by inventory and reporting.

**Check:** What do events cost in return for looser coupling? *(Eventual consistency, duplicates, and ordering concerns.)*

---

## ARC-009-L03 · ESB and iPaaS (12 min)
**Goal:** understand intermediary platforms and their trade-offs.

**Key points**
- ESB: a central bus that routes and transforms messages, often on premises; strong mediation, risk of becoming a central bottleneck and monolith.
- iPaaS: cloud integration service with connectors and low-code flows; fast for SaaS-to-SaaS, with its own limits and cost.
- Keep business logic out of the middleware; use it for routing, mapping, and protocols.
- Decide who owns flows: central team or product teams.

**Show:** a comparison table: ESB, iPaaS, direct APIs, event broker across connector support, control, cost shape, skills needed, and risk. Verify product details before recording.

**Check:** What should not live in the integration layer? *(Core business logic.)*

---

## ARC-009-L04 · Batch and file exchange still matter (10 min)
**Goal:** respect batch and files where they fit.

**Key points**
- Batch suits large volumes and tolerant latency: nightly price lists, financial postings.
- Files are common with ERP, banks, and carriers; formats and schedules are contracts.
- Make them safe: names, checksums, idempotent loads, reconciliation, and alerts for late files.
- Replace them only when the need justifies the change.

**Show:** a daily sales file from the POS to the ERP: naming rule, checksum, control totals, late-file alert at 02:00, reprocessing procedure.

**Check:** When is batch a good choice? *(High volume with tolerant latency, or when a system only supports files.)*

---

## ARC-009-L05 · Canonical models: when and when not (10 min)
**Goal:** decide when a shared data model helps.

**Key points**
- Canonical model: one agreed format for a business concept (order, customer) used between many systems.
- Helps when many systems exchange the same entity and you want N-to-one instead of N-to-N mappings.
- Hurts when it becomes a slow, committee-owned lowest common denominator.
- Use it for a few stable core entities; otherwise map pairwise with clear contracts.

**Show:** for Larkspur: canonical Order and Customer events for the platform; pairwise mapping for the carrier API, owned by an adapter.

**Check:** What is a sign a canonical model has gone wrong? *(It is slow to change, owned by a committee, and satisfies nobody.)*

---

## ARC-009-L06 · Operating integrations (8 min)
**Goal:** plan error handling, monitoring, and ownership.

**Key points**
- Every interface has an owner and a runbook.
- Error handling: retries with backoff, idempotency, dead-letter queues, manual repair.
- Monitoring: volume, latency, error rate, backlog, and business-level checks like order counts reconciling.
- Define what happens when a downstream system is down.

**Show:** an operations table per interface: owner, SLA, alert, retry policy, dead-letter handling, reconciliation, escalation.

**Check:** What makes a retry safe? *(Idempotent processing, so repeats do not duplicate effects.)*

---

## ARC-009-L07 · Demo: Larkspur's integration landscape, interface by interface (15 min)
**Goal:** build the interface catalog and target diagram. Prepares `ARC-009-LAB1`.

**Steps**
1. List systems: web and mobile front ends, commerce platform, ERP, CRM, payment provider, store POS and handhelds, carriers.
2. Enumerate interfaces: direction, data, volume, latency need, owner.
3. Choose a style per interface with justification: payments synchronous API; orders to ERP as events with ERP adapter; carriers via API with polling fallback; store sales via batch.
4. Define failure handling for each.
5. **Planned mistake:** every interface is designed as a synchronous API because "APIs are modern". Fix: re-check latency and volume needs and apply batch or events where fit.
6. Draw the target integration diagram and verify the ERP's real API limits before committing.

**Check:** What decides the style for an interface? *(Latency, volume, coupling, ownership, and the capabilities of the systems.)*

---

## ARC-009-L08 · Demo: the nightly ERP file that can't go away yet (14 min)
**Goal:** handle a legacy batch interface pragmatically.

**Steps**
1. Document the file: schema, schedule, volume, consumers, downtime windows, owner.
2. Learn why it exists: the ERP offers no usable API for the posting module and finance depends on the cutoff.
3. Wrap it: the integration layer builds and delivers the file; upstream systems see events and APIs.
4. Add safety: control totals, reconciliation report, late-file alert, replay.
5. **Planned mistake:** plan to switch off the file in release one. Fix: keep it as a supported interface with an exit trigger (ERP upgrade or vendor API) and date review.
6. Record the decision and update the interface catalog.

**Check:** Why wrap a legacy file instead of removing it? *(It protects dependent processes while isolating the rest of the design from it.)*
