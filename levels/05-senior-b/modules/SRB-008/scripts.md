# SRB-008 · Architecture migration — Lecture scripts

**Video:** 94 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-008-L01 · Why big-bang rewrites fail (10 min)
**Goal:** explain why rewrites usually fail and incremental migration works.

**Key points**
- The old system keeps changing while the new one is built, so the target moves.
- Hidden behavior in legacy is discovered late.
- No value is delivered until the end; risk piles up.
- Incremental migration delivers value early and can be stopped or reversed.

**Show:** a timeline comparing a 2-year rewrite with monthly extractions, showing risk and value over time.

**Check:** Why is incremental safer? *(Smaller steps, early value, reversible.)*

---

## SRB-008-L02 · The strangler fig (12 min)
**Goal:** route traffic gradually from legacy to new capabilities.

**Key points**
- A routing layer at the edge decides which system handles each request.
- Extract one capability at a time, starting with a low-risk, valuable one.
- Run in shadow or canary first; compare results.
- Retire the legacy path explicitly, or the migration never finishes.

**Show:** diagram: gateway routes /shipments/** to new service, rest to monolith; percentage rollout and a legacy retirement checklist.

**Check:** Which piece to extract first? *(A low-risk, valuable, well-bounded one rather than the hardest.)*

---

## SRB-008-L03 · Branch by abstraction (10 min)
**Goal:** change legacy internals safely behind an interface.

**Key points**
- Introduce an interface in the monolith in front of the capability.
- Implement the new behavior (calling the new service) behind the same interface.
- Switch with a flag; remove the old implementation when done.
- Keeps the main branch releasable throughout.

**Show:** outline: ShipmentTracker interface, LegacyShipmentTracker, RemoteShipmentTracker, a feature flag, and the removal step.

**Check:** What does the interface allow? *(Swapping implementations without long-lived branches.)*

---

## SRB-008-L04 · Dual writes and their alternatives (12 min)
**Goal:** explain why dual writes corrupt data and what to do instead.

**Key points**
- Two writes to two systems cannot be atomic; a failure in between leaves them different.
- Retries, ordering, and races create drift that is hard to detect.
- Alternatives: single writer, CDC from the owner, outbox plus events.
- If a temporary dual write is unavoidable, add reconciliation and a deadline.

**Show:** a failure timeline: write to monolith succeeds, write to new service times out; the systems now disagree. Next to it, the outbox version.

**Check:** Why are dual writes unsafe? *(No atomicity across two systems.)*

---

## SRB-008-L05 · Moving data ownership (12 min)
**Goal:** transfer a dataset to a new service safely.

**Key points**
- Steps: copy (backfill), keep in sync one way, verify, switch the writer, stop the sync, remove old.
- Only one system writes at any time.
- Cut-over has a freeze or a version gate; plan the rollback data path.
- Verify with counts, checksums, and sampled comparisons.

**Show:** a phase table: P1 backfill, P2 one-way sync via CDC, P3 verify, P4 switch writer, P5 reverse sync window, P6 delete legacy tables.

**Check:** How many writers at any moment? *(One.)*

---

## SRB-008-L06 · Rollback and exit criteria (8 min)
**Goal:** plan reversibility and decide when a step is done.

**Key points**
- Each step has a rollback that was tested.
- Exit criteria are measurable: traffic share, error rate, discrepancy count.
- Define when legacy code and tables are deleted.
- Write the criteria before starting.

**Show:** a step card: action, rollback, metric, threshold, owner, date.

**Check:** What makes exit criteria good? *(They are measurable and written before starting.)*

---

## SRB-008-L07 · Demo: extracting shipment tracking from the FulfillCo monolith (15 min)
**Goal:** walk through the first extraction step by step.

**Steps**
1. Map shipment tracking code and tables inside the monolith.
2. Add branch by abstraction and a gateway route in shadow mode.
3. Backfill history into the new service and sync new events via CDC.
4. **Planned mistake:** let both systems accept tracking updates; fix by choosing one writer and forwarding the other.
5. Shift traffic in stages with a rollback at each stage.

Prepares SRB-008-LAB1.

---

## SRB-008-L08 · Demo: catching a dual-write inconsistency in production data (15 min)
**Goal:** detect and repair drift caused by a dual write.

**Steps**
1. Run a reconciliation query comparing the monolith and the new store.
2. Find the mismatched shipments and classify causes (timeout, ordering, retry).
3. Repair using the system of record as the source.
4. **Planned mistake:** patch rows in both systems manually; fix by repairing from the owner and automating the check.
5. Replace the dual write with an outbox and add a drift metric.

Prepares SRB-008-LAB1.

---
