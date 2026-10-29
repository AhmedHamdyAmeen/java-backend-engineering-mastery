# MID-019 · Data modeling at scale — Exercises and lab

## Lab
### MID-019-LAB1 · Partitioned orders
**Outcomes:** 1–4 · **Time:** ~2.5 h
Partition the 10 M-row order table by month. Compare query time for a one-month report and for a customer lookup before and after, and compare the cost of removing one old month (detach versus `DELETE`). Add a materialized view for daily sales and refresh it concurrently.
**Acceptance:** pruning visible in plans; old partitions detachable; comparison table of timings.

## Exercises (assessment: modeling scenario)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-019-EX01 | 1 | For a slow report needing five joins, propose one denormalization and name how you keep it consistent. |
| MID-019-EX02 | 1 | Decide which of these are duplication and which are valid snapshots: `product_name` in order items, `customer_email` in orders, `price_at_purchase`. |
| MID-019-EX03 | 2 | Create a range-partitioned table with three monthly partitions and a default partition. |
| MID-019-EX04 | 2 | Write a query that prunes to one partition and one that cannot, and show both plans. |
| MID-019-EX05 | 3 | Store variable product attributes as `jsonb`, index them, and query by containment. |
| MID-019-EX06 | 3 | List three fields in a `jsonb`-heavy design that should become columns. |
| MID-019-EX07 | 4 | Write a retention plan for orders, audit log, and sessions with archive method for each. |

## Solutions
- **EX01** For example a `daily_sales` materialized view refreshed nightly or an `order_total` column maintained in the same transaction; state the allowed staleness.
- **EX02** `price_at_purchase` and arguably `product_name` are snapshots; `customer_email` in orders is a copy that should be justified (snapshot of the address used) or removed.
- **EX03** `PARTITION BY RANGE (created_at)`, three `FOR VALUES FROM ... TO ...` partitions, and `CREATE TABLE ... PARTITION OF orders DEFAULT`.
- **EX04** `WHERE created_at >= '2026-02-01' AND created_at < '2026-03-01'` scans one partition; `WHERE customer_id = 7` scans all partitions (no key filter).
- **EX05** `attrs jsonb`, `CREATE INDEX ... USING gin (attrs jsonb_path_ops)`, `WHERE attrs @> '{"color":"red"}'`.
- **EX06** Foreign keys, status fields used in filters and joins, amounts used in calculations.
- **EX07** For example orders: keep hot 2 years in the database, archive older partitions to files; audit log: monthly partitions kept 1 year; sessions: delete after 30 days. Values are examples; check reasoning.
- The "partitioning small tables" and "jsonb as schema avoidance" mistakes are covered by EX06 and the quiz.
