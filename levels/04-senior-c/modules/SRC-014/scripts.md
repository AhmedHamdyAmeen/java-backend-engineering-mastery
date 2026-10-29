# SRC-014 · Data integrity — Lecture scripts

**Video:** 84 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-014-L01 · Invariants across boundaries (12 min)
**Goal:** find the rules that must always hold across services and decide how each is protected.

**Key points**
- An invariant is a statement that must stay true, such as "every captured payment has exactly one order" or "stock is never negative".
- Within one database a transaction can enforce it; across services nothing enforces it by default.
- List invariants by walking a workflow and asking what must be true after each step and after each failure.
- For each, choose: prevent it by design, detect it by checks, or repair it when broken.

**Show** Table: invariant | services involved | enforced by | failure that breaks it. Example: *payment captured implies order exists | payments, orders, provider | nothing yet | order insert fails after capture.*

**Check:** Why do cross-service invariants need explicit design? *(No single transaction enforces them across services.)*

---

## SRC-014-L02 · Exactly-once effects (12 min)
**Goal:** distinguish unavailable exactly-once delivery from designable exactly-once effects.

**Key points**
- Over an unreliable network a sender cannot know whether a message arrived, so it retries; delivery is at-least-once or at-most-once.
- Exactly-once effects: make duplicates harmless with idempotency keys, deduplication tables, and conditional updates.
- Some platform features (for example Kafka transactions) give exactly-once processing inside their own boundary; effects outside, such as charging a card, still need idempotency. Verify the guarantees for your versions.
- Pass an idempotency key to external providers and store the result per key.

**Show** `INSERT INTO processed(event_id) ... ON CONFLICT DO NOTHING`, with the side effect applied only when the insert succeeds, in the same transaction. Provider call with `Idempotency-Key: order-123-attempt-1`.

**Check:** How do you get exactly-once effects from at-least-once delivery? *(Make handling idempotent, so repeated deliveries have the same effect as one.)*

---

## SRC-014-L03 · Prevent, detect, repair (10 min)
**Goal:** pick the right control for each invariant.

**Key points**
- Prevent: constraints, outbox pattern, idempotency, sagas with compensation.
- Detect: reconciliation, invariant checks, alerts on counters that should match.
- Repair: automated fixes for known drift, manual workflow for the rest, always logged.
- Cost-benefit: money-touching invariants need all three; low-impact ones may only need detection.

**Show** Matrix: invariant × prevent / detect / repair, filled for the order workflow.

**Check:** Why not rely on prevention alone? *(Bugs, outages, and external systems still cause drift, so you must also detect and repair.)*

---

## SRC-014-L04 · Reconciliation design (12 min)
**Goal:** build jobs that find and fix drift between your data and external systems.

**Key points**
- Compare two sources of record by a stable key (order ID, provider reference) over a defined window.
- Classify mismatches: missing on one side, amount differs, status differs; also timing differences that resolve themselves.
- Make jobs idempotent and re-runnable; produce a report with counts and a work queue for unresolved items.
- Repairs are explicit actions (refund, mark, re-send) carrying who or what did them and why.
- Handle late settlement files and currency or rounding quirks.

**Show** Pseudocode: load orders and payments for day D, load provider settlement for D, full outer join on reference, bucket results, write findings, apply auto-repair rules, write audit rows.

**Check:** Why must reconciliation tolerate timing differences? *(Settlement can lag, producing temporary mismatches that are not errors.)*

---

## SRC-014-L05 · Audit trails (8 min)
**Goal:** record financially significant changes so they can be explained later.

**Key points**
- Record who or what, when, what changed (before and after), and why, for money and status changes.
- Append-only: audit rows are never updated or deleted by the application.
- Keep it queryable by order and by time, and retain it per policy; mind personal data rules in the trail.
- Include automated actors such as the reconciliation job.

**Show** Audit row: `id, entity, entity_id, action, actor, at, before, after, reason, correlation_id`.

**Check:** Why include a correlation ID? *(To link an audit entry to the request, logs, and traces behind it.)*

---

## SRC-014-L06 · Demo: reconciling orders against the payment provider (15 min)
**Goal:** build and run a daily reconciliation on the running case; prepares SRC-014-LAB1.

**Steps**
1. Load the day's orders, payments, and the provider's settlement file into a staging area.
2. Join by provider reference and bucket: matched, orders without charge, charges without order, amount mismatch.
3. Inspect the planted discrepancies and decide an automatic repair for each type.
4. **Planned mistake:** compare totals only. Fix: compare per record, since offsetting errors hide in totals.
5. Apply repairs and write an audit row for each; re-run to show it is idempotent.
6. Produce the report with counts and open items.

**Check:** Why compare per record and not just totals? *(Offsetting errors cancel out in totals.)*

---

## SRC-014-L07 · Demo: tracing a double charge to its root cause (15 min)
**Goal:** trace a customer's double charge through telemetry and data to a systemic cause; prepares SRC-014-LAB1.

**Steps**
1. Start from the complaint: two charges for order 123; pull audit rows and provider references.
2. Follow the correlation ID through logs and traces to two payment calls.
3. Find the cause: the first call timed out client-side but succeeded at the provider, and the retry used a new idempotency key.
4. **Planned mistake:** blame the customer double-clicking. Fix: test the hypothesis from timestamps and traces before concluding.
5. Fix by deriving the key from the order and attempt and persisting it before the call.
6. Add a reconciliation rule to detect this class and a regression test; refund through the audited path.

**Check:** What was the root cause? *(A retry with a new idempotency key after a timeout that actually succeeded.)*
