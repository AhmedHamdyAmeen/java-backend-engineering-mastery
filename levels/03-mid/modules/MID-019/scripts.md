# MID-019 · Data modeling at scale — Lecture scripts

**Video:** 58 min · **Running project:** Shop Platform (10-million-row order history)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-019-L01 · Normalization trade-offs (10 min)
**Goal:** know why normalization is the default and what it costs.

**Key points**
- Normalized data stores each fact once: no update anomalies, smaller writes, clear constraints.
- The cost is joins on reads; with good indexes this is usually fine.
- Denormalize only for a measured read problem, not by habit.
- Start from the access patterns: which queries are frequent and slow?
- Keep the normalized tables as the source of truth.

**Show:** the Shop order model: `orders`, `order_item`, `product`, with a report query needing four joins and its measured time.

**Check:** What is the main risk of storing the same fact in two places? *(The copies drift apart.)*

---

## MID-019-L02 · Denormalization patterns (10 min)
**Goal:** apply a denormalization and keep copies consistent.

**Key points**
- Common patterns: a copied column (`product_name` in `order_item` as a historical snapshot), a counter (`order_count`), a summary table, a materialized view.
- Historical snapshots (price at purchase) are not duplication: they are different facts.
- Keep derived copies consistent with transactions, triggers, or periodic refresh; choose by how stale the data may be.
- `REFRESH MATERIALIZED VIEW CONCURRENTLY` needs a unique index and avoids blocking readers.
- Document who owns each copy and how it is repaired.

**Show**
```sql
CREATE MATERIALIZED VIEW daily_sales AS
SELECT date_trunc('day', created_at) AS day, sum(total_cents) AS revenue
FROM orders GROUP BY 1;
CREATE UNIQUE INDEX ON daily_sales (day);
REFRESH MATERIALIZED VIEW CONCURRENTLY daily_sales;
```

**Check:** Why does `price_cents` in `order_item` belong there even in a normalized design? *(It records the price at purchase time, which differs from the current price.)*

---

## MID-019-L03 · Table partitioning (12 min)
**Goal:** split a large table by range or list and use partition pruning.

**Key points**
- Declarative partitioning: `PARTITION BY RANGE (created_at)` with child tables per month.
- Partition pruning: when the query filters on the partition key, the planner reads only the matching partitions.
- Benefits: faster maintenance (drop or detach an old partition instead of a huge `DELETE`), smaller indexes, easier archiving.
- Rules: the primary key and unique constraints must include the partition key; create partitions ahead of time (or automate).
- Do not partition small tables; the overhead is not worth it (a typical threshold is tens of millions of rows or hundreds of GB; measure).

**Show**
```sql
CREATE TABLE orders (
  id bigint, created_at timestamptz NOT NULL, customer_id bigint, total_cents bigint,
  PRIMARY KEY (id, created_at)
) PARTITION BY RANGE (created_at);
CREATE TABLE orders_2026_01 PARTITION OF orders
  FOR VALUES FROM ('2026-01-01') TO ('2026-02-01');
```

**Check:** Why must the primary key include `created_at`? *(Unique constraints must contain the partition key.)*

---

## MID-019-L04 · `jsonb`: when and how (8 min)
**Goal:** use `jsonb` for flexible attributes without abandoning the schema.

**Key points**
- Good for sparse, varying attributes (product specs per category) and stored external payloads.
- Not a way to avoid designing the schema: keep ids, foreign keys, and frequently filtered fields as real columns.
- Query with `->`, `->>`, `@>`; index with GIN (`jsonb_path_ops` for containment) or a B-tree expression index on one key.
- Updating one key rewrites the whole value; large frequently updated documents are costly.

**Show**
```sql
CREATE INDEX idx_product_attrs ON product USING gin (attrs jsonb_path_ops);
SELECT id FROM product WHERE attrs @> '{"color":"red"}';
```

**Check:** Which fields should not live only in `jsonb`? *(Keys, foreign keys, and fields used in joins and frequent filters.)*

---

## MID-019-L05 · Retention and archiving (6 min)
**Goal:** plan how long data stays and where it goes.

**Key points**
- Decide retention per table from business and legal needs (orders for years, sessions for days).
- Partitions make it cheap: `DETACH PARTITION`, archive to cheaper storage or a file, then drop.
- Large `DELETE`s create bloat and long locks; avoid them for retention.
- Test restoring archived data; archived but unreadable data is lost data.
- Personal data may require deletion on request (privacy rules); plan for both.

**Show:** a table: data class / hot period / archive period / method.

**Check:** Why is dropping a partition better than `DELETE` for old data? *(It is instant, creates no dead rows, and needs no vacuum.)*

---

## MID-019-L06 · Demo: partitioning the order history by month (12 min)
**Goal:** convert the order history to monthly partitions and observe pruning.

**Steps**
1. Show the unpartitioned 10 M-row `orders` and the plan for a one-month query (large index or sequential scan).
2. Create the partitioned table `orders_p` with a composite primary key and monthly partitions plus a default partition.
3. Copy data in batches and add indexes; swap names in a short transaction.
4. Run the one-month query: `EXPLAIN` shows only one partition scanned (pruning).
5. **Planned mistake:** filter with a function on `created_at`, so pruning does not happen. Fix: use a direct range.
6. `DETACH PARTITION orders_2025_01` and archive; compare with the old bulk `DELETE`.

Prepares MID-019-LAB1.

**Check:** What shows pruning in the plan? *(Only the matching partitions appear as scan nodes.)*
