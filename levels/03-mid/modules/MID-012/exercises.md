# MID-012 · Index internals — Exercises and lab

## Lab
### MID-012-LAB1 · Index the order history
**Outcomes:** 1–4 · **Time:** ~2 h
Load 10 M orders. For five frequent Shop queries (orders by customer newest first, open orders by age, orders by date range, product search by attributes in `jsonb`, order totals per customer), design the minimum set of indexes. Measure insert time for 100 k rows before and after adding them.
**Acceptance:** each query's plan uses the intended index; write overhead measured and reported.

## Exercises (assessment: index design for a new workload)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-012-EX01 | 1 | Draw a three-level B-tree for 12 keys and trace a lookup. |
| MID-012-EX02 | 1 | Given `WHERE a = ? AND b > ? ORDER BY b`, choose the order for `(a, b)` or `(b, a)` and justify. |
| MID-012-EX03 | 2 | Choose an index type for: JSON containment, date ranges on a 500 M-row log, `tsvector` search, plain equality. |
| MID-012-EX04 | 3 | Write a partial index for the 2% of orders that are unshipped and a query that uses it. |
| MID-012-EX05 | 3 | Make `SELECT customer_id, total_cents` for one customer an index-only scan. |
| MID-012-EX06 | 4 | List unused and duplicate indexes in a database using the statistics views. |
| MID-012-EX07 | 4 | Measure `INSERT` throughput with 0, 3, and 8 indexes and summarize. |

## Solutions
- **EX01** Root with 2 children, each with leaf pages; the lookup compares at each page and follows one pointer per level.
- **EX02** `(a, b)`: equality column first, then the range/sort column; `(b, a)` cannot use `a` to narrow.
- **EX03** GIN; BRIN; GIN on `tsvector`; B-tree.
- **EX04** `CREATE INDEX ... ON orders (created_at) WHERE shipped_at IS NULL;` the query must repeat `shipped_at IS NULL`.
- **EX05** `CREATE INDEX ... ON orders (customer_id) INCLUDE (total_cents);` then `VACUUM` and check for `Index Only Scan` with low `Heap Fetches`.
- **EX06** Query `pg_stat_user_indexes` for `idx_scan = 0`; find indexes with the same leading columns.
- **EX07** Throughput drops as indexes are added (measured values vary by machine); report cost per index.
- Outcomes 2 and 4 are also tested in the quiz.
