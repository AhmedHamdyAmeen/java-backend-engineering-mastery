# MID-012 · Index internals — Lecture scripts

**Video:** 62 min · **Running project:** Shop Platform (10-million-row order history)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-012-L01 · How a B-tree index works (12 min)
**Goal:** explain why a B-tree finds rows in a few page reads.

**Key points**
- A B-tree is a balanced tree of sorted pages: root, internal pages, leaf pages that point to table rows (heap tuples).
- A lookup descends only 3–4 levels even for millions of rows.
- Sorted leaves make equality, range, and `ORDER BY` fast.
- It cannot help with `LIKE '%abc'` or with a function wrapped around the column.
- Pages are 8 kB and hold many entries, so the tree stays shallow.

**Show:** a diagram of a root, two internal pages, and leaf pages with `customer_id` values; trace a lookup of 4711. Optionally inspect tree height with the `pageinspect` extension (verify availability before recording).

**Check:** Why does an index lookup on 10 M rows need only a few page reads? *(The tree is shallow and wide.)*

---

## MID-012-L02 · Composite indexes and column order (10 min)
**Goal:** choose the column order of a multi-column index.

**Key points**
- The index is sorted by the first column, then the second within it, and so on.
- It serves queries that use a leftmost prefix: `(a, b)` helps `a` and `a, b`, not `b` alone.
- Put equality columns first, then the range or sort column.
- Match the real predicates; query shape matters more than raw selectivity.
- A matching index can also supply the sort order and avoid a sort step.

**Show**
```sql
CREATE INDEX idx_orders_cust_created ON orders (customer_id, created_at DESC);
-- serves: WHERE customer_id = ? ORDER BY created_at DESC LIMIT 20
```

**Check:** Will `(customer_id, created_at)` efficiently serve `WHERE created_at > ?` alone? *(No; the leading column is missing.)*

---

## MID-012-L03 · GIN, GiST, BRIN, hash (12 min)
**Goal:** pick the right index type for a workload.

**Key points**
- **GIN:** many keys per row; `jsonb`, arrays, full-text search. Slower writes, fast containment lookups.
- **GiST:** geometric and range types, nearest-neighbour, exclusion constraints.
- **BRIN:** tiny index of min/max per block range; good for huge, naturally ordered tables (append-only `created_at`).
- **Hash:** equality only; B-tree is usually just as good.
- Default to B-tree; use the others when the operator demands it.

**Show:** a table of workload to index type, with `CREATE INDEX ... USING gin (attrs jsonb_path_ops)` and `USING brin (created_at)`.

**Check:** Which type suits a 10 M-row append-only table filtered by date range with minimal space? *(BRIN.)*

---

## MID-012-L04 · Partial and covering indexes (10 min)
**Goal:** shrink indexes and avoid table visits.

**Key points**
- Partial index: a `WHERE` clause on the index so it holds only the rows you query (for example, open orders).
- The query must imply the index predicate to use it.
- Covering index: `INCLUDE (cols)` stores extra columns in the leaf so the query can read only the index.
- An index-only scan also needs the visibility map to be current, so vacuum matters (see MID-014).

**Show**
```sql
CREATE INDEX idx_orders_open ON orders (created_at) WHERE status = 'OPEN';
CREATE INDEX idx_orders_cust_cov ON orders (customer_id) INCLUDE (total_cents);
```

**Check:** What must be true for an index-only scan to avoid heap visits? *(All needed columns are in the index and the pages are marked all-visible.)*

---

## MID-012-L05 · The cost of indexes (6 min)
**Goal:** weigh read speed against write and storage cost.

**Key points**
- Every insert, and every update that changes indexed columns, touches each index on the table.
- Indexes use disk and memory and add vacuum work.
- Unused indexes are pure cost; find them in `pg_stat_user_indexes` (`idx_scan = 0`).
- Drop duplicates and prefixes covered by a longer index.

**Show:** `SELECT indexrelname, idx_scan, pg_size_pretty(pg_relation_size(indexrelid)) FROM pg_stat_user_indexes ORDER BY idx_scan;`

**Check:** Why is an index with `idx_scan = 0` a problem? *(It costs writes and space and is never read.)*

---

## MID-012-L06 · Demo: one query, five indexes, five plans (12 min)
**Goal:** see how each index design changes the plan for the same query.

**Steps**
1. Query: recent paid orders of one customer on the 10 M-row table; the baseline plan is a sequential scan.
2. Add a single-column index on `customer_id`; compare plan and time.
3. Add `(customer_id, created_at DESC)`; the sort step disappears.
4. Add a partial index on `status = 'PAID'`, then a covering index with `INCLUDE`; observe an index-only scan.
5. **Planned mistake:** create `(created_at, customer_id)`; the planner ignores it for this query. Fix: reverse the column order.
6. Record plan type, buffers, and time for all five.

Prepares MID-012-LAB1.

**Check:** Which index gave the cheapest plan and why? *(The covering composite: right order and no heap visits.)*
