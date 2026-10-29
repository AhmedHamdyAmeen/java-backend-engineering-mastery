# SRB-002 · Event-driven architecture — Lecture scripts

**Video:** 86 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-002-L01 · Event-driven architecture at organization scale (10 min)
**Goal:** see events as contracts between teams, not just messages in a broker.

**Key points**
- Events decouple deployment and timing, but not meaning: consumers still depend on the contract.
- More consumers means more coordination cost for every change.
- Choose events where the publisher should not know its consumers.
- Treat the event stream like a public API with owners and versions.

**Show:** diagram: Shop orders and FulfillCo warehouse and shipping publish to a broker; Platform, analytics, and partners consume; arrows annotated with owner team.

**Check:** Why are events still coupling? *(Consumers depend on their meaning and shape.)*

---

## SRB-002-L02 · Kinds of events and when to use each (12 min)
**Goal:** choose between notification, state transfer, and domain events.

**Key points**
- Notification: tiny, says something happened; consumers call back for details.
- Event-carried state transfer: full data included; consumers need no callback but copy data.
- Domain event: a business fact in the publisher's language, such as OrderReadyForFulfillment.
- Do not leak internal tables or entities as events.

**Show:** three versions of one event: {orderId} (notification); {orderId, lines, address} (state transfer); OrderReadyForFulfillment {orderId, items, promisedDate} (domain). Table of trade-offs: coupling, payload size, privacy.

**Check:** Which kind avoids a callback to the publisher? *(Event-carried state transfer.)*

---

## SRB-002-L03 · Ownership and event catalogs (10 min)
**Goal:** make every event findable and owned.

**Key points**
- One owning team per event type; the owner approves changes.
- A catalog lists name, owner, purpose, schema, topic, retention, sensitivity, and consumers.
- Naming follows business language and past tense.
- Catalog entries are reviewed like code, kept in a repository.

**Show:** an event catalog YAML entry: name ShipmentDispatched, owner FulfillCo-shipping, topic, schema ref, contains personal data: yes, replay-safe: no.

**Check:** Who owns an event type? *(The publishing team that produces the business fact.)*

---

## SRB-002-L04 · Schema evolution across teams (12 min)
**Goal:** change event schemas without breaking consumers you cannot coordinate with.

**Key points**
- Compatibility modes: backward, forward, full; pick one per topic and enforce in a registry.
- Safe changes: add optional fields; unsafe: rename, remove, change meaning.
- Breaking change: publish a new versioned topic or event type and run both during migration.
- Set a deprecation window and measure remaining consumers.

**Show:** schema registry compatibility check in CI failing a PR that renames carrierCode; a topic pair shipment-dispatched.v1 and .v2 with a sunset date.

**Check:** Name a safe schema change. *(Adding an optional field with a default.)*

---

## SRB-002-L05 · Replay and backfill (12 min)
**Goal:** re-process events safely, including for consumers with side effects.

**Key points**
- Replay is needed for new consumers, bug fixes, and recovery.
- Pure projections replay freely; side-effecting consumers (emails, payments) need protection.
- Techniques: idempotency keys, replay mode that disables side effects, deduplication tables.
- Throttle backfills so they do not starve live traffic.

**Show:** a consumer with a replay flag: in replay mode, update state but skip sending email; a dedupe table keyed by event id; backfill rate limit.

**Check:** How do you protect an email-sending consumer during replay? *(Replay mode skipping sends plus event-id deduplication.)*

---

## SRB-002-L06 · Demo: designing the Shop ↔ FulfillCo event contract (15 min)
**Goal:** produce a reviewed contract for order handoff and dispatch.

**Steps**
1. Run a short workshop: who needs to know when an order is ready and when it ships.
2. Draft OrderReadyForFulfillment as a domain event with minimal personal data.
3. Draft ShipmentDispatched with carrier, tracking code, and package list.
4. **Planned mistake:** put FulfillCo's internal warehouse row IDs in the event; fix by using business identifiers and a mapping.
5. Add both to the catalog with owners and replay rules; run a mock consumer review.

Prepares SRB-002-LAB1.

---

## SRB-002-L07 · Demo: a replay that would have resent 40,000 emails, and the fix (15 min)
**Goal:** catch a dangerous replay before it hurts customers.

**Steps**
1. Setup: a bug fix requires replaying ShipmentDispatched for a week.
2. Inspect the notification consumer: it sends an email per event.
3. Dry-run the replay in staging with a mail sink and show 40,000 captured messages.
4. **Planned mistake:** rely on 'we will pause the mail provider' as the safeguard; fix with a replay flag and a sent-notifications table.
5. Update the catalog: mark the consumer as side-effecting and document the replay procedure.

Prepares SRB-002-LAB1.

---
