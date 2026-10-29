# ARC-032 · Integration with enterprise systems — Lecture scripts

**Video:** 72 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-032-L01 · Working with systems of record (10 min)
**Goal:** respect systems of record while building a new platform around them.

**Key points**
- A system of record is the one place where a data set is authoritative; others hold copies.
- For each flow state: who owns the data, who may change it, how copies are refreshed, what happens when the owner is down.
- The platform may be the system of engagement (customer-facing) while the ERP stays the record for products, prices, and finance.
- Writes to a system of record should be commands to its owner, not direct database edits.

**Show:** a table: data set, system of record, copies, direction, style, behavior when the other side is down.

**Check:** Why not write directly into the ERP database? *(It bypasses the owner's rules, breaks upgrades, and couples to internals.)*

---

## ARC-032-L02 · ERP integration (12 min)
**Goal:** integrate products, prices, stock, and financial postings with the ERP.

**Key points**
- Products and prices flow from ERP to platform (often batch or change events); the platform keeps a read-optimized copy.
- Stock: ERP holds the book position; the platform needs near-real-time availability; use events or CDC plus reservation logic on the platform.
- Orders and payments flow to the ERP as postings; finance needs completeness, correct accounts, and idempotency.
- Protect the ERP: queues, rate limits, maintenance windows, backlog monitoring. Interface technology and limits are product-specific: verify before recording.

**Show:** a flow diagram: ERP → product/price feed → platform catalog; platform order event → queue → posting adapter → ERP; daily stock reconciliation.

**Check:** Why queue postings to the ERP? *(It absorbs peaks and outages, so the platform keeps working and the ERP is not overloaded.)*

---

## ARC-032-L03 · CRM integration (10 min)
**Goal:** integrate the CRM for profiles, service cases, and marketing consent.

**Key points**
- Decide the master for each item: customer identity (platform or CRM), service cases (CRM), marketing consent (one authoritative store).
- Consent must propagate quickly and reliably; withdrawal is the urgent direction.
- Service agents need a single view: orders from the platform, cases from the CRM; show it through APIs rather than copying everything.
- Plan for merge and duplicate handling of customers.

**Show:** a ownership table with consent as a first-class event: "consent withdrawn" published by the preference center, consumed by CRM, email tool, and analytics.

**Check:** Which direction of consent change is the urgent one? *(Withdrawal, because continuing to market is a compliance breach.)*

---

## ARC-032-L04 · Payment gateways and identity providers (12 min)
**Goal:** integrate payment and identity providers with correct failure handling and reconciliation.

**Key points**
- Payments: use idempotency keys, handle timeouts as "unknown" states, process provider webhooks, and verify signatures.
- Reconciliation: compare gateway settlement, platform payments, and ERP postings regularly; investigate differences.
- Identity providers: federation, token validation, session handling, and a plan for provider outage (cached keys, limited offline sessions).
- Always define behavior when the other side is down and who is told.

**Show:** a payment state diagram: initiated, pending, authorized, captured, failed, unknown; "unknown" resolved by querying the provider.

**Check:** A payment call times out. What state is it in? *(Unknown. Query the provider with the idempotency key before retrying or cancelling.)*

---

## ARC-032-L05 · Demo: an anti-corruption layer between the platform and the ERP (14 min)
**Goal:** build a worked design of an ACL that keeps ERP models out of the platform; prepares ARC-032-LAB1.

**Steps**
1. Show the ERP's model: item master with 40 fields, cryptic status codes, customer and ship-to as separate entities.
2. Define the platform's own domain model: Product, Price, Availability, Order.
3. Design the ACL: translator mapping ERP structures to domain objects, status code dictionary, error translation, and a stable internal contract.
4. **Planned mistake:** reuse the ERP's field names and status codes directly in the platform API. Fix: translate at the boundary so an ERP upgrade changes one adapter only.
5. Add contract tests against the adapter and monitoring of translation failures.

---

## ARC-032-L06 · Demo: reconciling payments between the gateway, platform, and ERP (14 min)
**Goal:** run a reconciliation design and walk through a mismatch; prepares ARC-032-LAB1.

**Steps**
1. Define the three sources: gateway settlement file, platform payment records, ERP cash postings.
2. Match on payment reference and amount per day; classify results: matched, missing in one source, amount difference, duplicate.
3. Investigate a sample: platform shows captured, gateway shows nothing; cause was a timeout treated as failure.
4. **Planned mistake:** fix the one record by hand and move on. Fix: correct the cause (state handling for "unknown"), add an automated check, and route exceptions to a named finance owner.
5. Report daily match rate and aging of unresolved items.
