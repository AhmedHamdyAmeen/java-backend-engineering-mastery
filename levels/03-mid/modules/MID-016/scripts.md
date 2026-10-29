# MID-016 · Advanced transactions — Lecture scripts

**Video:** 74 min · **Running project:** Shop Platform (product edits, order placement, audit log)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-016-L01 · Optimistic locking (12 min)
**Goal:** detect concurrent edits with a version column.

**Key points**
- Add `@Version long version` to the entity; Hibernate adds `WHERE id = ? AND version = ?` to every update and increments the version.
- If zero rows are updated, it throws `OptimisticLockException` (Spring: `ObjectOptimisticLockingFailureException`).
- No database lock is held while the user thinks; it suits low-conflict workloads.
- Expose the version to clients (ETag or a field) so edits across requests are protected too.
- Map the exception to HTTP 409 with the current state.

**Show**
```java
@Entity class Product {
  @Id Long id;
  @Version long version;
  String name;
}
```

**Check:** What does Hibernate add to the update statement? *(A check that the version is still the one that was read.)*

---

## MID-016-L02 · Pessimistic locking from JPA (8 min)
**Goal:** lock rows from JPA when conflicts are likely.

**Key points**
- `@Lock(LockModeType.PESSIMISTIC_WRITE)` on a repository query issues `SELECT ... FOR UPDATE`.
- `PESSIMISTIC_READ` maps to `FOR SHARE` (verify dialect behavior before recording).
- Set a lock timeout hint (`jakarta.persistence.lock.timeout`) so threads do not wait forever.
- Locks are held to the end of the transaction; keep it short.

**Show**
```java
@Lock(LockModeType.PESSIMISTIC_WRITE)
@Query("select s from Stock s where s.productId = :id")
Optional<Stock> findForUpdate(Long id);
```

**Check:** When is the lock released? *(When the transaction commits or rolls back.)*

---

## MID-016-L03 · Choosing a locking strategy (8 min)
**Goal:** choose between atomic SQL, optimistic, and pessimistic locking.

**Key points**
- Low conflict, user edits spanning requests: optimistic.
- High conflict on a hot row (stock): atomic `UPDATE` first, otherwise pessimistic.
- Optimistic under heavy conflict wastes work on retries.
- Pessimistic holds connections and risks deadlocks; keep it inside one short transaction.

**Show:** a decision table: workload / conflict rate / chosen strategy / reason, with product edits, stock decrement, and nightly price job.

**Check:** Which strategy for two admins editing a product description? *(Optimistic, with a 409 on conflict.)*

---

## MID-016-L04 · Propagation in depth (12 min)
**Goal:** use propagation settings and know their traps.

**Key points**
- `REQUIRED` (default): join the current transaction or start one.
- `REQUIRES_NEW`: suspend the current transaction and start an independent one, with its own connection; it commits or fails on its own.
- `NESTED`: a savepoint inside the current transaction (needs JDBC savepoint support); rollback goes back to the savepoint only.
- Traps: self-invocation bypasses the proxy so annotations are ignored; `REQUIRES_NEW` needs a second connection, which can exhaust the pool; a caught runtime exception may still mark the shared transaction rollback-only.

**Show:** a table of the three propagations and a code sketch of a service calling another bean's `@Transactional(propagation = REQUIRES_NEW)` method.

**Check:** Why can `REQUIRES_NEW` exhaust the pool? *(Each nested call holds a second connection while the outer one is still held.)*

---

## MID-016-L05 · Retrying transactions safely (10 min)
**Goal:** retry transient failures without causing duplicates.

**Key points**
- Retry only transient errors: serialization failure, deadlock, optimistic lock conflict.
- Retry the whole transaction, outside the transactional method (a new transaction per attempt).
- Limit attempts and add backoff with jitter.
- Make the unit of work idempotent (unique request key, upsert) or retries can double-charge.
- Spring Retry or Resilience4j can wrap the call.

**Show**
```java
for (int attempt = 1; ; attempt++) {
  try { return tx.execute(s -> placeOrder(cmd)); }
  catch (TransientDataAccessException e) {
    if (attempt == 3) throw e;
    sleep(backoff(attempt));
  }
}
```

**Check:** Why must the retry loop be outside the transaction? *(Each attempt needs a fresh transaction; the failed one is dead.)*

---

## MID-016-L06 · Demo: concurrent edits with `@Version` (12 min)
**Goal:** show two admins editing the same product and returning 409.

**Steps**
1. Add `@Version` to `Product` and include `version` in the response DTO.
2. Two clients fetch product 1 (version 3).
3. Client A updates the name with version 3 and succeeds (version 4).
4. **Planned mistake:** the update DTO omits the version, so the entity is loaded fresh and the conflict is missed. Fix: require the version in the request and compare it.
5. Client B updates with version 3: `ObjectOptimisticLockingFailureException`, mapped by `@ControllerAdvice` to 409 with the current version.
6. Write an integration test for the two-client conflict.

Prepares MID-016-LAB1.

**Check:** What must the client send back to make optimistic locking work across requests? *(The version it read.)*

---

## MID-016-L07 · Demo: the `REQUIRES_NEW` audit-log trap (12 min)
**Goal:** show how `REQUIRES_NEW` interacts with pool size and rollbacks.

**Steps**
1. An `OrderService.place` calls `AuditService.log` annotated `REQUIRES_NEW` so the audit row survives order failure.
2. Show it works: order fails, audit row persists.
3. Set pool size to 2 and run 5 concurrent requests: each holds one connection and waits for a second; threads time out (pool deadlock).
4. **Planned mistake:** call the audit method from within the same class; no new transaction starts (proxy bypass). Fix: move it to another bean.
5. Fix the pool problem: record audit events after commit (`@TransactionalEventListener(AFTER_COMMIT)` or an outbox table) instead of nesting.

**Check:** What is a safer way to keep an audit row independent of the order outcome? *(Write it outside the outer transaction, for example after commit or via an outbox.)*
