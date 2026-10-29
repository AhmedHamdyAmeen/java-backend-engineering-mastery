# MID-011 · SQL mastery — Exercises and lab

## Lab
### MID-011-LAB1 · Analytics queries
**Outcomes:** 1–4 · **Time:** ~3 h
Using the Shop schema with generated data, write: (a) top 3 products per category per month, (b) customer retention cohorts (first-order month vs months since), (c) the category tree with totals including all descendants. Write a plain Java implementation of each to cross-check.
**Acceptance:** one SQL query per report; results match the Java implementation on the same data.

## Exercises (assessment: timed SQL test plus these exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-011-EX01 | 1 | Rewrite a three-level nested subquery as chained CTEs. |
| MID-011-EX02 | 1 | List every descendant of category 5 with its depth using a recursive CTE. |
| MID-011-EX03 | 2 | For each customer, number orders by date and show days since the previous order. |
| MID-011-EX04 | 2 | Explain the difference between `ROW_NUMBER`, `RANK`, and `DENSE_RANK` on tied values 10, 10, 8. |
| MID-011-EX05 | 3 | For each category, get the 2 newest products using `LATERAL`. |
| MID-011-EX06 | 3 | Produce paid, cancelled, and refunded counts per month in one query with `FILTER`. |
| MID-011-EX07 | 4 | Write an idempotent upsert for `product_stock(product_id, qty)` that adds to the quantity. |

## Solutions
- **EX01** `WITH a AS (...), b AS (SELECT ... FROM a ...), c AS (...) SELECT ... FROM c;` each step named.
- **EX02** Anchor `WHERE id = 5, 0 AS depth`; recursive part joins `category c ON c.parent_id = t.id`, `depth + 1`.
- **EX03** `row_number() OVER (PARTITION BY customer_id ORDER BY created_at)` and `created_at - lag(created_at) OVER (PARTITION BY customer_id ORDER BY created_at)`.
- **EX04** `ROW_NUMBER` 1,2,3; `RANK` 1,1,3; `DENSE_RANK` 1,1,2.
- **EX05** `FROM category c CROSS JOIN LATERAL (SELECT ... WHERE category_id = c.id ORDER BY created_at DESC LIMIT 2) p`.
- **EX06** `date_trunc('month', created_at)` with three `count(*) FILTER (WHERE status = ...)` columns, grouped by month.
- **EX07** `INSERT ... VALUES (...) ON CONFLICT (product_id) DO UPDATE SET qty = product_stock.qty + EXCLUDED.qty`.
- The "window vs GROUP BY" and "aggregate in Java" mistakes are covered by EX03, EX06, and the lab cross-check.
