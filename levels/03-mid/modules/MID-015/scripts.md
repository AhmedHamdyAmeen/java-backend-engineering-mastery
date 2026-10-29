# MID-015 · Isolation and locking — Lecture scripts

**Video:** 76 min · **Running project:** Shop Platform (stock reservation and order processing under concurrency)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-015-L01 · Concurrency anomalies (12 min)
**Goal:** name and recognize the five anomalies.

**Key points**
- **Dirty read:** reading another transaction's uncommitted data.
- **Non-repeatable read:** the same row read twice gives different values.
- **Phantom:** the same query returns a different set of rows the second time.
- **Lost update:** two transactions read, then both write; one overwrites the other.
- **Write skew:** two transactions read overlapping data and write different rows, breaking a rule that spans both (two doctors going off call).

**Show:** a timeline table for each anomaly with two columns (T1, T2) and the surprising result, using a Shop stock example for lost update.

**Check:** Two transactions each read stock = 5 and each write stock = 4. Which anomaly? *(Lost update.)*

---

## MID-015-L02 · Isolation levels in PostgreSQL (12 min)
**Goal:** know what each level prevents in PostgreSQL specifically.

**Key points**
- `READ COMMITTED` (default): each statement sees committed data; allows non-repeatable reads, phantoms, lost updates, write skew.
- `REPEATABLE READ`: one snapshot per transaction (snapshot isolation); prevents dirty, non-repeatable, phantom reads; detects some lost updates by failing with a serialization error; still allows write skew.
- `SERIALIZABLE`: prevents all anomalies by detecting dangerous patterns and aborting one transaction.
- PostgreSQL never allows dirty reads; `READ UNCOMMITTED` behaves as `READ COMMITTED`.
- Higher levels mean you must retry on failure (SQLSTATE `40001`).

**Show:** a table of five anomalies by three levels with yes/no.

**Check:** Does `READ COMMITTED` prevent lost updates for a read-modify-write in application code? *(No.)*

---

## MID-015-L03 · Row-level locks (10 min)
**Goal:** lock rows explicitly when needed.

**Key points**
- `SELECT ... FOR UPDATE` locks the selected rows until the transaction ends; others wait on writes or on their own `FOR UPDATE`.
- `FOR SHARE` blocks writers but allows other readers with `FOR SHARE`.
- `NOWAIT` fails immediately; `SKIP LOCKED` skips locked rows.
- Prefer an atomic `UPDATE ... SET qty = qty - 1 WHERE qty > 0` when it is enough: no lock dance and no round trip.
- Keep locking transactions short and lock rows in a consistent order.

**Show**
```sql
BEGIN;
SELECT qty FROM stock WHERE product_id = 7 FOR UPDATE;
UPDATE stock SET qty = qty - 1 WHERE product_id = 7;
COMMIT;
```

**Check:** What happens to a second `FOR UPDATE` on the same row? *(It waits until the first transaction ends.)*

---

## MID-015-L04 · `SKIP LOCKED` job queues (8 min)
**Goal:** build a safe multi-worker queue in a table.

**Key points**
- Workers claim a job with `FOR UPDATE SKIP LOCKED`, so no two take the same job and nobody waits.
- Claim and mark in one statement using a CTE with `UPDATE ... RETURNING`.
- Handle crashed workers: a claimed job rolls back (lock released) if the transaction dies.
- Fine for moderate volumes; for heavy messaging use a broker (later modules).

**Show**
```sql
WITH next AS (
  SELECT id FROM job WHERE status = 'NEW'
  ORDER BY id LIMIT 1 FOR UPDATE SKIP LOCKED
)
UPDATE job SET status = 'RUNNING' FROM next WHERE job.id = next.id RETURNING job.*;
```

**Check:** What does `SKIP LOCKED` do? *(Ignores rows other transactions have locked instead of waiting.)*

---

## MID-015-L05 · Deadlocks (10 min)
**Goal:** understand, diagnose, and prevent deadlocks.

**Key points**
- Deadlock: T1 holds A and wants B, T2 holds B and wants A. PostgreSQL detects it after `deadlock_timeout` (default 1 s) and aborts one transaction with SQLSTATE `40P01`.
- Prevention: lock in a consistent order (sort ids), keep transactions short, avoid user interaction inside them.
- Diagnose from the server log (it names the processes and queries) and from `pg_locks` joined with `pg_stat_activity`.
- The aborted transaction can be retried.

**Show**
```sql
SELECT a.pid, a.query, l.locktype, l.mode, l.granted
FROM pg_locks l JOIN pg_stat_activity a USING (pid) WHERE NOT l.granted;
```

**Check:** What is the simplest rule to prevent most deadlocks? *(Always lock rows in the same order.)*

---

## MID-015-L06 · Demo: lost update in two terminals (12 min)
**Goal:** reproduce a lost update and fix it.

**Steps**
1. Create `stock(product_id, qty)` with one row, qty 10.
2. In two `psql` terminals, both `BEGIN; SELECT qty` (10), then both `UPDATE stock SET qty = 9` and commit; final qty is 9, not 8.
3. Fix 1: atomic `UPDATE stock SET qty = qty - 1 WHERE qty > 0` (final 8).
4. **Planned mistake:** assume `REPEATABLE READ` always lets both commit; show T2 fails with a serialization error ("could not serialize access due to concurrent update"). Explain this is correct and needs a retry.
5. Fix 2: `SELECT ... FOR UPDATE` so the second waits.

Prepares MID-015-LAB1.

**Check:** Which fix needs no extra round trip? *(The atomic `UPDATE` expression.)*

---

## MID-015-L07 · Demo: write skew under serializable (12 min)
**Goal:** reproduce write skew and see `SERIALIZABLE` stop it.

**Steps**
1. Rule: at least one admin must stay active. Table `admin(id, active)` with two active admins.
2. Under `REPEATABLE READ`, both transactions check "count of active > 1" and each deactivates a different admin; both commit and no admin remains.
3. Repeat with `SET TRANSACTION ISOLATION LEVEL SERIALIZABLE`; one commit fails with `40001`.
4. **Planned mistake:** run the application code without retry; the user sees an error. Fix: retry the whole transaction a limited number of times.
5. Mention the alternative: lock a parent row or use a constraint.

**Check:** Why does `REPEATABLE READ` allow this? *(Each transaction writes a different row, so there is no write-write conflict.)*
