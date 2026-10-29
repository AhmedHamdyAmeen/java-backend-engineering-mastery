# SRB-001 · Distributed architecture patterns — Lecture scripts

**Video:** 100 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-001-L01 · Patterns as trade-offs, not upgrades (10 min)
**Goal:** treat every advanced pattern as a purchase with a price, not a level-up.

**Key points**
- Each pattern solves one named problem and adds cost elsewhere (code, operations, hiring, debugging).
- Ask first: what problem do we have today, and what is the simplest thing that solves it?
- Fashion is a bad reason; a measured pain is a good reason.
- Write the rejected options down in an ADR so the next team sees the reasoning.

**Show:** a decision table with columns problem, pattern, cost added, simpler alternative, evidence needed. Example row: slow dashboards, CQRS read model, second store plus sync lag, a database index or view.

**Check:** Name two costs a pattern adds besides code. *(Operational burden (running, monitoring, rebuilding) and team learning curve; also eventual consistency.)*

---

## SRB-001-L02 · CQRS in full (12 min)
**Goal:** separate the write model from the read model when their needs really differ.

**Key points**
- Command side protects invariants; query side is shaped for screens and reports.
- CQRS-lite: same database, separate classes or views; often enough.
- Full CQRS: separate stores kept in sync by events; reads are eventually consistent.
- Use full CQRS when read load, shape, or scaling differs sharply from writes.

**Show:** a diagram: commands -> aggregate -> write DB -> outbox -> events -> projector -> read store (search or denormalized tables) -> query API. Beside it, the CQRS-lite version with a SQL view.

**Check:** When is CQRS-lite enough? *(When one database can serve both sides within latency and scale needs; only the code is separated.)*

---

## SRB-001-L03 · Event sourcing (14 min)
**Goal:** explain storing changes as facts instead of storing only the latest state.

**Key points**
- The event store is an append-only log of what happened per aggregate; current state is derived by replaying.
- You gain audit, time travel, and new read models from old history.
- You pay: event design is forever, replays take time, and fixing a wrong event is awkward.
- Not every entity needs it; use it where history is the business (ledgers, tracking).

**Show:** events for one shipment: ShipmentCreated, PickedUp, ArrivedAtHub, Delivered, stored as rows (aggregate id, version, type, payload, time); state = fold over the list. Optimistic concurrency uses the version number.

**Check:** Name one operational cost of event sourcing. *(Replaying long histories to rebuild state or projections, and schema evolution of stored events.)*

---

## SRB-001-L04 · Projections, snapshots, and upcasting (12 min)
**Goal:** keep an event-sourced system fast, rebuildable, and evolvable.

**Key points**
- A projection is a read model built by consuming events; it must be rebuildable from the log.
- A snapshot stores state at version N so replay starts there, not at zero.
- Upcasting converts old event versions to the current shape when reading.
- Track projection position (checkpoint) and make handlers idempotent.

**Show:** outline: ShipmentDelivered v1 (no signature field) upcast to v2 with signature=null on read; a checkpoint table (projection name, last position); snapshot every 100 events.

**Check:** Why must projection handlers be idempotent? *(Because rebuilds and retries deliver the same event more than once.)*

---

## SRB-001-L05 · Materialized views across services (10 min)
**Goal:** build a local, query-friendly copy of another service's data and manage how stale it is.

**Key points**
- Consume events from the owner and keep only the fields you need.
- Staleness is a product decision: state the acceptable lag and show timestamps if needed.
- Handle missing or out-of-order events by versioning and periodic reconciliation.
- The owner stays the source of truth; the view is disposable.

**Show:** Shop order page view: order id, status, last carrier event and its time, built from ShipmentDispatched events; a nightly reconciliation compares counts with FulfillCo's API.

**Check:** Who owns the data in a materialized view? *(The source service; the view is a disposable copy.)*

---

## SRB-001-L06 · Workflow engines vs hand-built sagas (12 min)
**Goal:** decide between a workflow engine (such as Temporal or Camunda) and a hand-written saga.

**Key points**
- Engines give durable state, timers, retries, and visibility for long, branching processes.
- They add a new platform to run, a programming model to learn, and a dependency.
- One short saga with two steps rarely justifies an engine; many long ones often do.
- Criteria: number of workflows, duration, human steps, need for audit and visibility. Verify product details before recording.

**Show:** a comparison table with rows durability, retries/timers, visibility, learning curve, operations, lock-in; two columns: hand-built (outbox + state table) vs engine.

**Check:** Name a sign that an engine is justified. *(Many long-running, multi-step processes with timers or human tasks needing visibility.)*

---

## SRB-001-L07 · Demo: modeling shipment tracking with and without event sourcing (15 min)
**Goal:** design shipment tracking for FulfillCo two ways on the same requirements and compare.

**Steps**
1. Write requirements: current status, full history, carrier corrections, partner feed.
2. Sketch option A: event-sourced aggregate with projections for status and partner feed.
3. Sketch option B: state table plus history table plus outbox events.
4. **Planned mistake:** model every carrier scan as a domain event and bloat the aggregate; fix by separating domain events from raw carrier telemetry.
5. Estimate replay time, storage, and schema-change work for both; record the decision draft.

Prepares SRB-001-LAB1.

---

## SRB-001-L08 · Demo: rebuilding a broken projection from the event store (15 min)
**Goal:** recover a read model that has wrong data, without downtime.

**Steps**
1. Show the symptom: Shop's tracking page shows Delivered shipments as In transit.
2. Find the bug in the projection handler and fix it in a new projection version.
3. Rebuild into a new table in parallel from position zero, tracking progress.
4. **Planned mistake:** switch readers before the rebuild catches up; fix by comparing positions and counts, then switching with a flag.
5. Drop the old table after a soak period and add a rebuild runbook.

Prepares SRB-001-LAB1.

---
