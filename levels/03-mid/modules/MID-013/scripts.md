# MID-013 · Query optimization — Lecture scripts

**Video:** 89 min · **Running project:** Shop Platform (loaded database with 10 M orders)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-013-L01 · How the planner thinks (10 min)
**Goal:** explain how PostgreSQL picks a plan.

**Key points**
- The planner estimates the cost of many possible plans and picks the cheapest estimate.
- Costs come from table statistics and settings such as `random_page_cost`.
- Selectivity is the fraction of rows a condition keeps; low selectivity (many rows) favours a sequential scan.
- A sequential scan is correct when you need a large share of the table; an index is not always better.
- The plan is only as good as its estimates.

**Show:** a diagram: SQL, parse, rewrite, plan (candidates with costs), execute. Show `WHERE status = 'PAID'` on a table where 90% of rows are paid, and why the planner scans.

**Check:** Why can the planner prefer a sequential scan even when an index exists? *(The condition matches so many rows that reading the index plus the heap costs more.)*

---

## MID-013-L02 · Reading EXPLAIN ANALYZE (15 min)
**Goal:** read a plan tree and spot the problem node.

**Key points**
- `EXPLAIN` shows the estimated plan; `EXPLAIN (ANALYZE, BUFFERS)` runs the query and adds actual rows, time, and page reads.
- Read inner-most, most-indented nodes first; time is per loop, multiply by `loops`.
- Compare `rows=` (estimate) with `actual rows=`; big gaps point to bad statistics.
- Scan types: `Seq Scan`, `Index Scan`, `Index Only Scan`, `Bitmap Heap Scan`.
- `ANALYZE` really executes the statement; wrap `INSERT`/`UPDATE`/`DELETE` in a transaction and roll back.

**Show**
```sql
EXPLAIN (ANALYZE, BUFFERS)
SELECT * FROM orders WHERE customer_id = 4711 ORDER BY created_at DESC LIMIT 20;
```
Annotate node type, estimated vs actual rows, `Buffers: shared hit/read`, and execution time.

**Check:** Why is plain `EXPLAIN` not enough to find a slow node? *(It shows only estimates, not actual rows or time.)*

---

## MID-013-L03 · Join algorithms (10 min)
**Goal:** recognize the three join methods and when each wins.

**Key points**
- **Nested loop:** for each outer row, look up inner rows; great with a small outer side and an index on the inner side.
- **Hash join:** build a hash table of one side, probe with the other; good for large, unsorted inputs and equality joins.
- **Merge join:** both sides sorted on the join key; good when inputs are already ordered (index or sort).
- A nested loop with a huge outer row count and a seq scan inside is a classic disaster.

**Show:** three small plan excerpts with their node names and when you would expect each.

**Check:** Which join is best for one customer's few orders joined to products by primary key? *(Nested loop with an index lookup.)*

---

## MID-013-L04 · Statistics and estimates (10 min)
**Goal:** explain where estimates come from and how to improve them.

**Key points**
- `ANALYZE` samples each column into `pg_stats`: null fraction, distinct count, most common values, histogram.
- Autovacuum runs analyze automatically, but after bulk loads run it by hand.
- Columns that are correlated (city and postcode) are assumed independent; fix with `CREATE STATISTICS`.
- Raise precision for skewed columns with `ALTER TABLE ... ALTER COLUMN ... SET STATISTICS n`.

**Show**
```sql
SELECT most_common_vals, most_common_freqs, n_distinct FROM pg_stats
WHERE tablename = 'orders' AND attname = 'status';
```

**Check:** What do you run after loading 10 M rows so the planner has good estimates? *(`ANALYZE` on the table.)*

---

## MID-013-L05 · Finding slow queries with `pg_stat_statements` (8 min)
**Goal:** find the queries that cost the most overall.

**Key points**
- Enable the extension via `shared_preload_libraries` and `CREATE EXTENSION pg_stat_statements` (restart required).
- It aggregates by normalized query text: calls, total time, mean time, rows.
- Sort by total time, not only mean: a fast query called a million times can dominate.
- Reset with `pg_stat_statements_reset()` before a test to measure cleanly.
- Column names changed in PostgreSQL 13 (`total_exec_time`); verify version before recording.

**Show**
```sql
SELECT calls, round(total_exec_time) AS total_ms, round(mean_exec_time::numeric, 2) AS mean_ms, query
FROM pg_stat_statements ORDER BY total_exec_time DESC LIMIT 10;
```

**Check:** Why sort by total time? *(Frequent cheap queries can cost more in total than rare slow ones.)*

---

## MID-013-L06 · Query rewrites that help (10 min)
**Goal:** apply common rewrites that make queries index-friendly.

**Key points**
- No function on an indexed column: `WHERE created_at >= '2026-01-01' AND created_at < '2026-02-01'`, not `date_trunc(...) = ...` (or add an expression index).
- Keyset pagination (`WHERE (created_at, id) < (?, ?) ORDER BY ... LIMIT n`) instead of deep `OFFSET`.
- Select only needed columns; avoid `SELECT *`.
- `EXISTS` instead of `IN (big subquery)` or `COUNT(*) > 0`.
- Fix N+1 from the ORM at the source with a join or batch fetch (details in MID-021).

**Show**
```sql
-- slow: OFFSET 500000 reads and discards 500k rows
-- fast:
SELECT * FROM orders WHERE (created_at, id) < ($1, $2)
ORDER BY created_at DESC, id DESC LIMIT 20;
```

**Check:** Why is `OFFSET 500000` slow? *(PostgreSQL must produce and throw away all skipped rows.)*

---

## MID-013-L07 · Demo: from 4 seconds to 40 ms (14 min)
**Goal:** fix one slow Shop endpoint query step by step with evidence.

**Steps**
1. Find the statement in `pg_stat_statements`; capture its `EXPLAIN (ANALYZE, BUFFERS)` (about 4 s, sequential scan with a sort).
2. Read the plan: the filter removes most rows, and the sort spills to disk.
3. Add `(customer_id, created_at DESC)`; re-run and show the sort gone.
4. **Planned mistake:** wrap the date column in `date_trunc` in the `WHERE`; the index is skipped. Fix: use a half-open range.
5. Replace `OFFSET` with keyset pagination.
6. Record before/after plans and timings (about 40 ms).

Prepares MID-013-LAB1.

**Check:** Which single change removed the sort? *(The composite index matching the `ORDER BY`.)*

---

## MID-013-L08 · Demo: a bad estimate and how statistics fix it (12 min)
**Goal:** diagnose a bad plan caused by a wrong row estimate.

**Steps**
1. Create correlated columns (`country`, `currency`) and a query filtering on both; the planner estimates 5 rows, actual is 300 000.
2. Show the nested loop chosen because of the underestimate and its runtime.
3. Run `CREATE STATISTICS s (dependencies) ON country, currency FROM orders; ANALYZE orders;`.
4. **Planned mistake:** forget to run `ANALYZE` after creating the statistics; the estimate does not change. Fix: analyze.
5. Re-run: estimate close to actual, plan switches to a hash join, time drops.

**Check:** Why was the estimate wrong? *(The planner assumed the two columns were independent.)*
