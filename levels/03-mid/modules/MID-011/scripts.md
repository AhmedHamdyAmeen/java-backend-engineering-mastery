# MID-011 · SQL mastery — Lecture scripts

**Video:** 72 min · **Running project:** Shop Platform (reporting queries on orders, products, categories)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-011-L01 · CTEs for readable queries (10 min)
**Goal:** break a complex query into named steps with `WITH`.

**Key points**
- A CTE (common table expression) is a named subquery: `WITH name AS (...)`.
- Chain several CTEs; each can read the earlier ones.
- Readability, not speed, is the main gain. In PostgreSQL 12+ a CTE is inlined unless it is referenced twice or has side effects; `MATERIALIZED` / `NOT MATERIALIZED` force the choice (verify version before recording).
- Name each step after what it holds, not how it is computed.

**Show**
```sql
WITH paid AS (
  SELECT * FROM orders WHERE status = 'PAID'
), per_customer AS (
  SELECT customer_id, sum(total_cents) AS spent FROM paid GROUP BY customer_id
)
SELECT * FROM per_customer WHERE spent > 100000;
```

**Check:** Is a CTE always an optimization fence? *(No; since PostgreSQL 12 it is usually inlined.)*

---

## MID-011-L02 · Recursive CTEs (10 min)
**Goal:** walk a hierarchy such as the category tree.

**Key points**
- Shape: anchor query `UNION ALL` recursive query that reads the CTE itself.
- The recursion stops when a step returns no new rows.
- Carry a `depth` or `path` column to order output and to detect cycles.
- Bad data with a cycle loops forever; guard with a depth limit or the `CYCLE` clause (PostgreSQL 14+; verify version before recording).

**Show**
```sql
WITH RECURSIVE tree AS (
  SELECT id, parent_id, name, 0 AS depth FROM category WHERE parent_id IS NULL
  UNION ALL
  SELECT c.id, c.parent_id, c.name, t.depth + 1
  FROM category c JOIN tree t ON c.parent_id = t.id
)
SELECT * FROM tree ORDER BY depth, name;
```

**Check:** What are the two parts of a recursive CTE? *(An anchor query and a recursive query joined with `UNION ALL`.)*

---

## MID-011-L03 · Window functions (15 min)
**Goal:** compute per-row values over a group of rows without collapsing them.

**Key points**
- `GROUP BY` returns one row per group; a window function keeps every row and adds a computed column.
- `OVER (PARTITION BY ... ORDER BY ...)` defines the window.
- Ranking: `ROW_NUMBER` (unique), `RANK` (ties share, gaps follow), `DENSE_RANK` (no gaps).
- `LAG`/`LEAD` read the previous/next row; `sum(...) OVER (ORDER BY ...)` gives a running total.
- You cannot filter on a window result in `WHERE`; wrap it in a CTE or subquery.

**Show**
```sql
SELECT day, revenue,
       sum(revenue) OVER (ORDER BY day) AS running_total,
       revenue - lag(revenue) OVER (ORDER BY day) AS change
FROM daily_sales;
```

**Check:** Which keeps all rows: `GROUP BY` or a window function? *(The window function.)*

---

## MID-011-L04 · Advanced joins and LATERAL (10 min)
**Goal:** use joins beyond the basic inner/left, including `LATERAL`.

**Key points**
- `LEFT JOIN` keeps unmatched left rows; conditions on the right table go in `ON`, not `WHERE`, or it turns into an inner join.
- Self-joins compare rows of one table (for example, product pairs bought together).
- `LATERAL` lets a subquery on the right refer to columns of the left row: a "for each row" query.
- Typical use: top N per parent, with `ORDER BY ... LIMIT n` inside.

**Show**
```sql
SELECT c.name, top.*
FROM category c
CROSS JOIN LATERAL (
  SELECT p.name, p.price_cents FROM product p
  WHERE p.category_id = c.id ORDER BY p.price_cents DESC LIMIT 3
) top;
```

**Check:** What does `LATERAL` allow that a normal subquery in `FROM` does not? *(Referring to columns of earlier `FROM` items.)*

---

## MID-011-L05 · Set operations and FILTER (8 min)
**Goal:** combine result sets and compute several conditional aggregates in one pass.

**Key points**
- `UNION` removes duplicates; `UNION ALL` keeps them and is faster. Default to `UNION ALL`.
- `INTERSECT` and `EXCEPT` find common and missing rows; both sides need matching columns.
- `count(*) FILTER (WHERE status = 'PAID')` replaces repeated `CASE` expressions.
- One scan can produce many metrics.

**Show**
```sql
SELECT count(*) AS orders,
       count(*) FILTER (WHERE status = 'PAID')      AS paid,
       count(*) FILTER (WHERE status = 'CANCELLED') AS cancelled
FROM orders;
```

**Check:** Which is faster, `UNION` or `UNION ALL`, and why? *(`UNION ALL`; it skips duplicate removal.)*

---

## MID-011-L06 · Upserts (7 min)
**Goal:** insert or update in one atomic statement.

**Key points**
- `INSERT ... ON CONFLICT (key) DO UPDATE SET ...` or `DO NOTHING`.
- The conflict target needs a unique index or constraint.
- `EXCLUDED` refers to the row you tried to insert.
- It is atomic under concurrency; "select, then insert or update" is not.

**Show**
```sql
INSERT INTO daily_sales (day, revenue_cents) VALUES ($1, $2)
ON CONFLICT (day) DO UPDATE
SET revenue_cents = daily_sales.revenue_cents + EXCLUDED.revenue_cents;
```

**Check:** Why is `ON CONFLICT` safer than select-then-insert? *(It is one atomic statement; two sessions cannot both insert.)*

---

## MID-011-L07 · Demo: building the monthly sales report in SQL (12 min)
**Goal:** build the monthly report as one query that uses CTEs, windows, and `FILTER`.

**Steps**
1. Show the Java version that loads all orders and aggregates in memory; note its row count and time.
2. Write a CTE `monthly` that groups paid orders by `date_trunc('month', created_at)` and category.
3. Add `rank() OVER (PARTITION BY month ORDER BY revenue DESC)` and keep the top 3.
4. Add `lag(revenue)` for month-over-month change and `FILTER` for refunded counts.
5. **Planned mistake:** put the `rank()` condition in `WHERE`; PostgreSQL rejects it. Fix: wrap in a CTE and filter outside.
6. Compare time and data transferred with the Java version.

Prepares MID-011-LAB1.

**Check:** Why is aggregating in SQL usually better than in Java? *(Less data crosses the network and the database is built for it.)*
