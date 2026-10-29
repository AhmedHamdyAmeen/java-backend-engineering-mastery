# MID-020 · Database migrations — Lecture scripts

**Video:** 60 min · **Running project:** Shop Platform (rename `customer.name` to `full_name` under live traffic)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-020-L01 · Why migrations cause outages (8 min)
**Goal:** see how a schema change can block production.

**Key points**
- Many `ALTER TABLE` forms take an `ACCESS EXCLUSIVE` lock, which blocks all reads and writes on the table.
- A waiting DDL statement also blocks later queries queued behind it, so one slow transaction can cause a pile-up.
- Table rewrites (changing a column type, some defaults on older versions) hold the lock while copying data.
- Old and new application versions run together during a deploy, so the schema must work for both.

**Show:** a timeline: a long transaction holds a lock, `ALTER TABLE` waits, new queries queue behind the `ALTER`, and the API times out.

**Check:** Why does a waiting `ALTER TABLE` hurt even before it runs? *(It queues in the lock queue and blocks everything behind it.)*

---

## MID-020-L02 · Expand and contract (12 min)
**Goal:** restructure a column without downtime.

**Key points**
- Expand: add the new column (nullable); deploy code that writes to both and reads the old.
- Migrate: backfill old rows in batches; verify.
- Switch: deploy code that reads the new column; keep writing both for a while.
- Contract: stop writing the old column, then drop it in a later release.
- Each step is backward compatible with the previous app version, so any step can be rolled back.

**Show:** a five-release table for renaming `customer.name` to `full_name`: add column, dual-write, backfill, switch reads, drop old.

**Check:** Why is `ALTER TABLE customer RENAME COLUMN` in one step unsafe while old app instances run? *(Old instances still use the old name and fail immediately.)*

---

## MID-020-L03 · Lock-safe DDL (10 min)
**Goal:** apply DDL with minimal locking.

**Key points**
- Set `lock_timeout` (for example 3 s) before DDL so it fails fast instead of queueing; retry in a quiet moment.
- `CREATE INDEX CONCURRENTLY` avoids blocking writes (cannot run inside a transaction; may leave an invalid index on failure to clean up).
- Add constraints in two steps: `ADD CONSTRAINT ... NOT VALID`, then `VALIDATE CONSTRAINT` (lighter lock).
- Adding a column with a constant default is fast on modern PostgreSQL (11+); a volatile default (like `random()`) rewrites the table (verify version before recording).
- For `NOT NULL` on a large table: add a check constraint `NOT VALID`, validate, then set `NOT NULL` (PostgreSQL 12+ can use the validated check to skip the scan).

**Show**
```sql
SET lock_timeout = '3s';
CREATE INDEX CONCURRENTLY idx_orders_customer ON orders (customer_id);
ALTER TABLE orders ADD CONSTRAINT fk_cust FOREIGN KEY (customer_id)
  REFERENCES customer(id) NOT VALID;
ALTER TABLE orders VALIDATE CONSTRAINT fk_cust;
```

**Check:** What does `lock_timeout` do for a migration? *(Makes it give up instead of waiting in the lock queue.)*

---

## MID-020-L04 · Batched backfills (8 min)
**Goal:** populate a new column on a huge table safely.

**Key points**
- One giant `UPDATE` holds locks, creates huge WAL and bloat, and can run for hours.
- Update in small batches (1 000–10 000 rows) by primary key range, each in its own transaction, with a short pause.
- Make the job resumable and idempotent (`WHERE full_name IS NULL`).
- Watch replication lag and load; throttle if needed.
- Run backfills from an operational job, not inside the startup migration.

**Show**
```sql
UPDATE customer SET full_name = name
WHERE id BETWEEN :from AND :to AND full_name IS NULL;
```

**Check:** Why batch the update? *(Small transactions limit lock time, WAL volume, bloat, and replication lag.)*

---

## MID-020-L05 · Rollback strategies (8 min)
**Goal:** plan rollback for each step before starting.

**Key points**
- Prefer roll-forward fixes, but each step must be reversible or harmless to leave.
- Expand steps roll back by deploying the previous app version; the extra column is harmless.
- Destructive steps (drop column, drop table) are the point of no return: take a backup and do them last, after a soak period.
- Flyway/Liquibase migrations are versioned and not rolled back automatically; write the compensating migration.
- Practice the rollback in staging.

**Show:** a table per step: change, how to verify, rollback action, point of no return.

**Check:** Which step cannot be rolled back easily? *(Dropping the old column.)*

---

## MID-020-L06 · Demo: renaming a column under live traffic (14 min)
**Goal:** rename `customer.name` to `full_name` with zero failed requests.

**Steps**
1. Start a load test hitting customer endpoints; baseline error count is zero.
2. Release 1: Flyway adds `full_name` (nullable); app writes both columns, reads `name`.
3. Run the batched backfill; verify with a count of rows where the columns differ.
4. Release 2: app reads `full_name` and still writes both.
5. **Planned mistake:** run `ALTER TABLE ... RENAME COLUMN` directly; the load test shows errors from old instances. Show it, restore, and continue with the safe path.
6. Release 3: stop writing `name`; later Release 4 drops it. The load test reports zero failures.

Prepares MID-020-LAB1.

**Check:** At which release can the old column finally be dropped? *(After no running version reads or writes it.)*
