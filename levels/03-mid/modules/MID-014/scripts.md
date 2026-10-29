# MID-014 · MVCC — Lecture scripts

**Video:** 54 min · **Running project:** Shop Platform (orders and stock under concurrent access)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-014-L01 · Readers don't block writers (10 min)
**Goal:** explain the core promise of MVCC.

**Key points**
- MVCC (multi-version concurrency control) keeps several versions of a row so readers and writers do not wait for each other.
- A reader sees a consistent snapshot; a writer creates a new version.
- Writers still block other writers on the same row.
- The price: old versions pile up and must be cleaned (vacuum).

**Show:** two sessions: session A starts a transaction and selects a product; session B updates its price and commits; session A still sees the old price (under `REPEATABLE READ`) and was never blocked.

**Check:** Does a long `SELECT` block an `UPDATE` of the same row? *(No.)*

---

## MID-014-L02 · Row versions and snapshots (12 min)
**Goal:** explain visibility using `xmin`, `xmax`, and snapshots.

**Key points**
- Every row version (tuple) stores `xmin` (transaction that created it) and `xmax` (transaction that deleted or replaced it).
- A snapshot lists which transactions are committed from the viewpoint of a statement or transaction.
- A version is visible if its creator is committed in your snapshot and its deleter is not.
- Under `READ COMMITTED` a snapshot is taken per statement; under `REPEATABLE READ` once per transaction.

**Show**
```sql
SELECT xmin, xmax, ctid, * FROM product WHERE id = 1;
```
Run before and after an update in another session; point at the changed `xmin` and `ctid`.

**Check:** What does `xmax` hold on a live row that nobody has touched? *(Zero; no deleting transaction.)*

---

## MID-014-L03 · Vacuum and autovacuum (10 min)
**Goal:** explain what vacuum does and why to keep autovacuum on.

**Key points**
- An `UPDATE` writes a new row version and marks the old one dead; `DELETE` marks it dead.
- `VACUUM` marks dead versions reusable, updates the visibility map, and freezes old transaction ids.
- Autovacuum runs it automatically when enough rows change; tune per table for hot tables.
- Plain `VACUUM` does not shrink the file; `VACUUM FULL` does but takes an exclusive lock.
- Never disable autovacuum; fix its settings instead.

**Show:** `SELECT relname, n_dead_tup, last_autovacuum FROM pg_stat_user_tables ORDER BY n_dead_tup DESC;`

**Check:** Why does an `UPDATE` need vacuum later? *(It leaves the old row version behind as a dead tuple.)*

---

## MID-014-L04 · Bloat and long transactions (10 min)
**Goal:** find bloat and the long transactions that cause it.

**Key points**
- Bloat is dead space in tables or indexes that vacuum cannot reuse fast enough; it slows scans and wastes disk.
- Vacuum can only remove versions no transaction might still need; an old open snapshot holds the cleanup horizon back.
- Idle-in-transaction sessions are the usual cause, often from application code that opens a transaction and then calls a slow service.
- Protect with `idle_in_transaction_session_timeout` and short transactions.

**Show**
```sql
SELECT pid, state, xact_start, now() - xact_start AS age, query
FROM pg_stat_activity WHERE state <> 'idle' ORDER BY xact_start;
```

**Check:** Why can one idle transaction cause table bloat? *(Vacuum cannot remove versions the old snapshot may still see.)*

---

## MID-014-L05 · Demo: an idle transaction blocking vacuum (12 min)
**Goal:** create bloat with an idle transaction and fix it.

**Steps**
1. Create a hot table `stock_log` and a loop that updates rows continuously; show baseline size and `n_dead_tup`.
2. In another session run `BEGIN; SELECT count(*) FROM stock_log;` and leave it open.
3. Run `VACUUM (VERBOSE) stock_log`; it reports dead rows "not yet removable".
4. **Planned mistake:** disable autovacuum to "fix" growth; bloat gets worse. Fix: re-enable it.
5. Terminate the idle session (or set `idle_in_transaction_session_timeout`) and vacuum again; dead tuples drop.
6. Note table size stays large (reusable space, not returned to the OS).

Prepares MID-014-LAB1.

**Check:** Which message in `VACUUM VERBOSE` reveals the culprit? *(Dead row versions "not yet removable" because of an old transaction.)*
