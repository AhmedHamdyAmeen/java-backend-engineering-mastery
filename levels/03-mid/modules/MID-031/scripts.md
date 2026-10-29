# MID-031 · Distributed workflows — Lecture scripts

**Video:** 88 min · **Analogy used throughout:** booking a holiday from several vendors: if the hotel is booked but the flight fails, you cancel the hotel; you cannot "undo" with one big transaction.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-031-L01 · Why distributed transactions don't scale (10 min)
**Goal:** explain why two-phase commit is avoided across services.

**Key points**
- **Two-phase commit (2PC):** a coordinator asks all participants to prepare, then to commit.
- Participants hold locks while waiting; a coordinator crash leaves them blocked.
- Availability is the product of all participants' availability, and latency is the slowest one.
- Services own separate databases and brokers; many do not support 2PC at all.
- The alternative is a series of local transactions with explicit recovery.

**Show:** a diagram: coordinator, `inventory`, `payments`, locks held across a network round trip.

**Check:** What happens to participants if the 2PC coordinator dies after prepare? *(They stay blocked holding locks.)*

---

## MID-031-L02 · Sagas (12 min)
**Goal:** model a process as local transactions plus compensations.

**Key points**
- A **saga** is a sequence of local transactions; each publishes the trigger for the next.
- If a step fails, earlier steps are undone by **compensating transactions**.
- Sagas give no isolation: others can see intermediate states (for example stock reserved but unpaid).
- Some steps cannot be undone (email sent); put those last or make them semantic ("send apology").
- Each step and compensation must be idempotent (MID-029).

**Show**
| Step | Local transaction | Compensation |
| --- | --- | --- |
| 1 | Create order `PENDING` | Mark `CANCELLED` |
| 2 | Reserve stock | Release stock |
| 3 | Authorize payment | Void authorization |
| 4 | Confirm order | none (final) |

**Check:** Why is a saga not isolated like a database transaction? *(Intermediate states are committed and visible to others.)*

---

## MID-031-L03 · Choreography (10 min)
**Goal:** coordinate a saga through events only.

**Key points**
- Each service reacts to events and emits its own: `OrderPlaced` → `StockReserved` → `PaymentAuthorized`.
- No central owner, low coupling, easy for 2 to 3 steps.
- The process lives nowhere in code: it is hard to see, test, and change as it grows.
- Risk of cyclic dependencies and "who handles the failure?" confusion.
- Add a correlation id (order id) to every event for tracing.

**Show:** an event flow diagram: `orders` → `inventory` → `payments` → `orders`, with failure events `PaymentDeclined` flowing back.

**Check:** What is the main weakness of choreography as steps grow? *(The overall flow is implicit and hard to follow or change.)*

---

## MID-031-L04 · Orchestration (10 min)
**Goal:** coordinate a saga with an explicit orchestrator.

**Key points**
- An **orchestrator** owns the process: sends commands, waits for replies, decides the next step.
- The flow is in one place: easier to read, test, add timeouts, and monitor.
- Cost: an extra component and the risk of putting business rules in it; keep it about sequencing only.
- Persist the saga state so a restart resumes where it stopped.
- Rule of thumb: choreography for short, stable flows; orchestration for longer, branching, or time-sensitive ones.

**Show**
```java
enum SagaState { STARTED, STOCK_RESERVED, PAID, COMPLETED, COMPENSATING, FAILED }
record OrderSaga(UUID orderId, SagaState state, Instant deadline, int version) {}
```

**Check:** Why persist saga state? *(So a crash or restart resumes the process instead of losing it.)*

---

## MID-031-L05 · Compensation design (10 min)
**Goal:** write compensations that are safe and meaningful.

**Key points**
- A compensation is a new business action, not a database rollback (a refund, not a deleted payment).
- It must be **idempotent**: it may run twice.
- It must tolerate the forward step **never having happened** (or still being in flight): releasing stock that was never reserved is a no-op.
- Record intent first (a reservation id) so the compensation knows what to undo.
- Late arrivals: a "reserve" message that arrives after "release" must not re-reserve.

**Show**
```java
@Transactional
void release(UUID orderId) {
    reservations.findByOrder(orderId).ifPresentOrElse(
        r -> { if (r.isActive()) { r.cancel(); stock.add(r.sku(), r.qty()); } },
        () -> reservations.recordCancelled(orderId)); // blocks a late reserve
}
```

**Check:** What should `release` do if nothing was reserved? *(Nothing harmful; record the cancellation so a late reserve is rejected.)*

---

## MID-031-L06 · Saga state, timeouts, and stuck sagas (10 min)
**Goal:** keep sagas from hanging forever.

**Key points**
- Store state, step, deadline, and attempt count in the orchestrator's database.
- A scheduled sweeper finds sagas past their deadline and triggers retry or compensation.
- Make every reply handler idempotent and ignore replies for a state that has moved on.
- Expose a stuck-saga metric and an admin way to retry or force compensation.
- Give each step its own timeout shorter than the overall one.

**Show**
```sql
SELECT id FROM order_saga
WHERE state NOT IN ('COMPLETED','FAILED') AND deadline < now()
FOR UPDATE SKIP LOCKED;
```

**Check:** What triggers action when a reply never arrives? *(A timeout sweeper acting on the saved deadline.)*

---

## MID-031-L07 · Demo: the order saga, happy path (14 min)
**Goal:** build and run the orchestrated order saga. Prepares MID-031-LAB1.

**Steps**
1. Show the saga table and the `OrderSaga` state machine inside `orders`.
2. `POST /orders` creates the order `PENDING` and a saga row, and writes a `ReserveStock` command via the outbox.
3. `inventory` replies `StockReserved`; the orchestrator moves to `STOCK_RESERVED` and sends `AuthorizePayment`.
4. **Planned mistake:** handle `StockReserved` without checking the current state; replay the reply and the saga re-sends the payment command. Fix: ignore replies unless the state matches, plus inbox dedup.
5. `payments` replies `PaymentAuthorized`; order becomes `CONFIRMED`, saga `COMPLETED`.
6. Show the trace by correlation id across the three services.

---

## MID-031-L08 · Demo: payment declined, compensations run (12 min)
**Goal:** exercise the failure path end to end. Prepares MID-031-LAB1.

**Steps**
1. Use a test card number that `payments` declines.
2. `payments` replies `PaymentDeclined`; the saga moves to `COMPENSATING`.
3. The orchestrator sends `ReleaseStock`; `inventory` releases the reservation; the order becomes `CANCELLED`.
4. **Planned mistake:** write the compensation assuming a reservation exists; trigger the decline before stock replied and it throws. Fix: tolerate a missing reservation and record the cancellation.
5. Replay `ReleaseStock` and confirm stock is unchanged the second time.
6. Add a timeout case: stop `payments`; after the deadline the saga compensates.
