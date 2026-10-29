# ARC-026 · Event architecture — Lecture scripts

**Video:** 66 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-026-L01 · Events at enterprise scale (10 min)
**Goal:** explain what changes when events cross teams and organizations.

**Key points**
- An event is a record of something that happened, named in the past tense: OrderPlaced.
- Inside one team you can change events freely; across teams every event becomes a public contract.
- At scale the questions are who owns it, where it is described, and how it may change.
- Events differ from commands: a command asks someone to act; an event only reports a fact.

**Show:** two lines: "ReserveStock" (command, one receiver) and "StockReserved" (event, any number of listeners), with Larkspur consumers of each.

**Check:** Why name an event in the past tense? *(It reports a fact that already happened and cannot be refused by listeners.)*

---

## ARC-026-L02 · Event ownership (10 min)
**Goal:** assign exactly one owner to every event, including across organizations.

**Key points**
- The owner is the system of record for the fact: the system that decides it happened.
- The owner defines the schema, publishes, and handles change; consumers do not publish look-alike events.
- Cross-organization events (carrier, marketplace) need an agreement on who owns the contract.
- Two owners for one event means conflicting versions soon.

**Show:** an ownership table: OrderPlaced (platform), StockChanged (ERP, via adapter), ShipmentDispatched (fulfillment), ReturnReceived (store or warehouse system).

**Check:** Who owns StockChanged? *(The system of record for stock, here the ERP, published through its integration adapter.)*

---

## ARC-026-L03 · Event catalogs and schemas (12 min)
**Goal:** build an event catalog that consumers can trust.

**Key points**
- Catalog entry: name, owner, description, schema, example, delivery guarantees, consumers, status.
- A schema (JSON Schema, Avro, or Protobuf; choose by tooling) is stored in a registry, not in someone's head.
- Events carry business facts at a useful level, not mirrored table rows.
- Consumers register themselves so the owner knows who a change affects.

**Show:** a catalog entry for OrderPlaced with fields (orderId, customerId, lines, totals, placedAt), schema location, consumers (fulfillment, finance, CRM sync), and delivery guarantee at-least-once.

**Check:** Why register consumers? *(To know who is affected by a change and whom to notify.)*

---

## ARC-026-L04 · Compatibility and evolution (10 min)
**Goal:** define compatibility rules and an evolution process for schemas.

**Key points**
- Backward compatible: new readers can read old data; forward compatible: old readers can read new data.
- Safe changes: add optional fields. Unsafe: remove or rename fields, change types or meanings.
- Breaking changes get a new event version published alongside the old one with a retirement date.
- Automate compatibility checks in the build of the owning team.

**Show:** a rule table: add optional field (allowed), add required field (breaking), rename (breaking, use add-then-deprecate), plus a six-step evolution process.

**Check:** Is adding an optional field breaking? *(No, if consumers ignore unknown fields.)*

---

## ARC-026-L05 · When an event backbone pays off (10 min)
**Goal:** decide when a broker or streaming platform is justified.

**Key points**
- Justified by many producers and consumers, replay needs, high volume, or decoupled teams.
- Costs: a platform to operate, skills, governance, and monitoring.
- Few integrations with simple needs can use direct APIs or a small managed queue.
- Build ownership and catalog first; the technology is the smaller decision.

**Show:** a checklist with thresholds set by the team (number of producers, consumers, need to replay, peak rate) and Larkspur's score.

**Check:** Name one sign that a backbone is probably premature. *(Two systems exchanging a few messages a day with no replay need.)*

---

## ARC-026-L06 · Demo: Larkspur's order and stock events, from catalog to consumers (14 min)
**Goal:** build the Larkspur event catalog and trace one event to its consumers; prepares ARC-026-LAB1.

**Steps**
1. List business facts: order placed, stock changed, shipment dispatched, return received.
2. Assign one owner each and write the schema with examples.
3. **Planned mistake:** a team proposes an event "OrdersTableRowUpdated" carrying every column. Fix: replace it with OrderPlaced and OrderCancelled, business facts independent of the table layout.
4. Register consumers: fulfillment, finance, CRM sync, analytics; note each consumer's need.
5. Introduce a change: add "giftMessage" as optional and show consumers unaffected; then show a breaking change handled with a v2 event and a dated retirement of v1.
6. Decide, with the checklist, whether to adopt a backbone now and record the decision.
