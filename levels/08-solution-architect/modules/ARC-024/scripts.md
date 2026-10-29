# ARC-024 · Integration patterns — Lecture scripts

**Video:** 70 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-024-L01 · Integration styles compared (12 min)
**Goal:** name the five integration styles and say when each fits.

**Key points**
- Synchronous API: caller waits for an answer; good for "I need this now" such as a price lookup at checkout.
- Asynchronous events: sender announces a fact and moves on; good for many consumers and loose timing.
- Batch ETL/ELT: move large sets on a schedule; good when daily freshness is enough.
- File exchange: agreed files over SFTP or storage; common with older partners and carriers.
- CDC (change data capture): read a database's change log and publish changes; good when you cannot change the source application.

**Show:** a comparison table with columns "freshness", "coupling", "volume", "when to choose", and a Larkspur example per row (carrier labels, stock changes, nightly finance load).

**Check:** Which style lets you stream changes from an ERP database you cannot modify? *(CDC.)*

---

## ARC-024-L02 · Coupling, latency, and failure (10 min)
**Goal:** compare the styles on coupling, latency, and what happens when the other side is down.

**Key points**
- Temporal coupling: with a synchronous call both systems must be up at the same moment.
- Data coupling: a shared file format or event schema ties both sides to the same fields.
- Latency range: API in milliseconds, events in seconds, batch in hours.
- Failure: a down API fails the caller now; a down consumer of events catches up later; a failed batch leaves yesterday's data in use.

**Show:** a table of styles against "if the other side is down for one hour", with Larkspur results (checkout cannot price; stock events queue; nightly file waits).

**Check:** Which style survives an ERP outage best for stock updates? *(Asynchronous events or batch, since they queue and catch up.)*

---

## ARC-024-L03 · Batch, ETL, and ELT (10 min)
**Goal:** know when batch is the right and cheaper choice and how ETL differs from ELT.

**Key points**
- ETL transforms before loading; ELT loads raw data first and transforms inside the target, common with warehouses.
- Batch is simple to test, replay, and reconcile; it fits reports, finance, and bulk master data.
- Design for restarts: batches must be idempotent, with run IDs and row counts checked.
- Pick the window from business need; "real time" costs more and is often not required.

**Show:** a timeline of Larkspur's nightly loads (product master 01:00, sales to warehouse 02:00, finance posting 03:00) with row-count checks after each.

**Check:** What makes a batch safe to re-run? *(Idempotence: loading the same input twice leaves the same result.)*

---

## ARC-024-L04 · Enterprise integration patterns (10 min)
**Goal:** apply three classic patterns where they simplify a design.

**Key points**
- Message translator: converts one system's format to another so neither learns the other's model.
- Content-based router: sends each message to a destination chosen from its content, such as order type.
- Aggregator: collects related messages, such as one per warehouse, into one combined result.
- Use a pattern to solve a named problem; a diagram full of patterns is a warning sign.

**Show:** a flow for a multi-part order: router sends "click-and-collect" orders to the store, "home delivery" to a warehouse; aggregator joins shipment confirmations; translator maps ERP codes to platform terms.

**Check:** Which pattern joins several shipment confirmations into one order status? *(Aggregator.)*

---

## ARC-024-L05 · Demo: choosing a style for each Larkspur interface (14 min)
**Goal:** walk the interface list and choose a style for each, with reasons; prepares ARC-024-LAB1.

**Steps**
1. List interfaces from the context diagram: ERP, CRM, payment gateway, carriers, stores, marketing platform.
2. For each, write the latency need, volume, and what happens if it is down.
3. Choose: payment authorization as a synchronous API; order and stock changes as events; finance posting as nightly batch; carrier labels as API with a file fallback; marketing audiences as a daily file.
4. **Planned mistake:** choose real-time events for the marketing export "to be modern". Fix: show that the campaign tool refreshes once a day, so a daily file costs less and is easier to reconcile.
5. Add owner, frequency, volume, and SLA columns; flag interfaces with no owner.
6. Present three decisions and their trade-offs to a role-played integration lead.

---

## ARC-024-L06 · Demo: replacing a nightly stock file with near-real-time CDC (14 min)
**Goal:** redesign one interface step by step and prove the benefit with numbers.

**Steps**
1. State the problem: the nightly ERP stock file means the web shop oversells items sold in stores during the day.
2. Quantify: count oversold orders per week and the cost of cancellations, with the business owner.
3. Design: capture stock-table changes in the ERP database, publish stock-changed events, and update the platform's stock cache; keep the nightly file as a reconciliation check.
4. **Planned mistake:** publish raw table-row changes as events. Fix: add a translator that emits a business event (StockChanged: item, location, quantity) so consumers do not depend on ERP columns.
5. Plan failure modes: lag alarm, replay from the log position, and a fallback to the nightly file.
6. Agree success measures with the store-ops lead: oversells down, lag under the agreed seconds, reconciliation differences near zero.
