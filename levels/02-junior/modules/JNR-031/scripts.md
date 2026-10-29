# JNR-031 · Transactions — Lecture scripts

**Video:** 79 min · **Analogy used throughout:** a bank transfer in a sealed envelope: either every step inside happens, or the envelope is torn up and nothing happened.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-031-L01 · ACID by example (10 min)
**Goal:** explain A, C, I, and D with a failure story each.

**Key points**
- Atomicity: all steps or none. Money leaves account A but a crash stops before B is credited: rollback undoes the debit.
- Consistency: rules stay true (stock never below zero, foreign keys valid).
- Isolation: concurrent transactions do not see each other's half-done work (levels come in later modules).
- Durability: once committed, data survives a crash.
- A transaction is one unit of work that begins, then commits or rolls back.

**Show:** a table: letter / promise / failure it prevents.

**Check:** Which letter protects a half-finished transfer? *(Atomicity.)*

---

## JNR-031-L02 · Transaction boundaries (10 min)
**Goal:** put the transaction around one business operation.

**Key points**
- The boundary is the business operation, for example "place order", not a single SQL statement.
- Put `@Transactional` on service methods, not on controllers or repositories.
- Repository calls inside join the service's transaction.
- Without a boundary each repository call commits alone, and a failure leaves partial data.
- Keep the business operation as one public service method.

**Show**
```java
@Service
public class OrderService {
    @Transactional
    public Order placeOrder(PlaceOrderCommand cmd) {
        stockService.reserve(cmd.lines());   // same transaction
        return orderRepository.save(Order.from(cmd));
    }
}
```

**Check:** Which layer owns the transaction? *(The service layer.)*

---

## JNR-031-L03 · `@Transactional` and proxies (12 min)
**Goal:** understand how the annotation works and why it can silently fail.

**Key points**
- Spring wraps your bean in a proxy: begin before the method, commit or rollback after.
- Only calls that go through the proxy get a transaction.
- Self-invocation (`this.other()` in the same class) bypasses the proxy, so the annotation on `other()` is ignored.
- Private, package-private, or final-class problems: use public methods on a Spring-managed bean.
- Fix self-invocation by moving the method to another bean.

**Show**
```java
public void transfer(...) { debit(...); credit(...); }   // called from outside
@Transactional public void debit(...) { ... }            // IGNORED when called via this.debit()
```

**Check:** Why is `@Transactional` ignored on a method called with `this.`? *(The call skips the proxy.)*

---

## JNR-031-L04 · Rollback rules (8 min)
**Goal:** know what triggers a rollback.

**Key points**
- Default: rollback on unchecked exceptions (`RuntimeException`, `Error`).
- Checked exceptions commit by default.
- Change with `@Transactional(rollbackFor = Exception.class)` or make your business exceptions unchecked.
- If you catch an exception and do not rethrow it, the proxy never sees it: no rollback.
- Mark rollback only manually (`setRollbackOnly`) in rare cases.

**Show**
```java
@Transactional(rollbackFor = PaymentException.class)  // checked exception
public void pay(...) throws PaymentException { ... }
```

**Check:** Does a checked exception roll back by default? *(No, it commits.)*

---

## JNR-031-L05 · Propagation basics (8 min)
**Goal:** know what happens when a transactional method calls another.

**Key points**
- Default `REQUIRED`: join the existing transaction or start one.
- Inner failure marks the whole shared transaction for rollback.
- `REQUIRES_NEW` suspends the outer one and runs a separate transaction; use it rarely (for example an audit log that must survive).
- Read-only: `@Transactional(readOnly = true)` for queries; it is a hint that can skip dirty checking.
- Other modes exist; learn them when you need them.

**Show:** a diagram: `placeOrder` (REQUIRED) → `reserve` (REQUIRED) share one transaction; `audit` (REQUIRES_NEW) has its own.

**Check:** What does the default `REQUIRED` do? *(Joins the current transaction or starts a new one.)*

---

## JNR-031-L06 · Long transactions and remote calls (7 min)
**Goal:** keep transactions short.

**Key points**
- A transaction holds a database connection and locks while it is open.
- Never call a payment API, email service, or any slow remote system inside it.
- A remote call cannot be rolled back with the database.
- Do remote work before or after the transaction, or use an event/outbox later (MID level).
- Long transactions starve the connection pool.

**Show:** a timeline: prepare (no transaction) → transaction: reserve stock, save order → commit → call payment/email.

**Check:** Why not call a payment API inside the transaction? *(It holds a connection and locks, and the payment cannot be rolled back.)*

---

## JNR-031-L07 · Demo: making checkout atomic (12 min)
**Goal:** make "place order" all-or-nothing; prepares JNR-031-LAB1.

**Steps**
1. Show `placeOrder` without `@Transactional`: stock is reserved, then the order save fails; stock is wrong.
2. Add `@Transactional` to the service method.
3. Re-run the failing test: stock is unchanged.
4. **Planned mistake:** throw a checked exception and show the stock change committed; fix with `rollbackFor`.
5. Add `@Transactional(readOnly = true)` to the order query method.

---

## JNR-031-L08 · Demo: finding the self-invocation bug (12 min)
**Goal:** diagnose a transaction that never starts; prepares JNR-031-LAB1.

**Steps**
1. Run the money-transfer exercise: a failure after debit leaves money missing.
2. Check the code: `transfer()` calls `this.debitAndCredit()`, which has the annotation.
3. Prove it with the transaction log (`logging.level.org.springframework.transaction=TRACE`): no transaction begins.
4. **Planned mistake:** mark the private method `@Transactional` and show it still does nothing.
5. Fix it by moving the method to another bean (or annotating the public entry point); re-run the failure test.
