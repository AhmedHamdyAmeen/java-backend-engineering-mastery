# MID-041 · NoSQL fundamentals — Exercises and lab

## Lab
### MID-041-LAB1 · Model comparison
**Outcomes:** 1–3 · **Time:** ~1.5 h
Model Shop's reviews (rating, text, product, customer, date) in a document, a wide-column, and a relational form. For each model list the queries it supports well, those it supports badly, and its consistency and scaling behavior.
**Acceptance:** comparison table covering at least five queries across the three models.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-041-EX01 | 1 | Match each use case to a model: session lookup, product with varying attributes, time-series sensor writes, "friends of friends". |
| MID-041-EX02 | 1 | Give one Shop feature fitting each of key-value, document, wide-column, and graph. |
| MID-041-EX03 | 2 | List three queries for order history, then design a wide-column table for each. |
| MID-041-EX04 | 2 | Explain what you give up when you model for queries only. |
| MID-041-EX05 | 3 | State, for a Cassandra-like store and a single-node PostgreSQL, the side each takes in CAP and what PACELC adds. |

## Solutions
- **EX01** Session: key-value. Varying attributes: document. Time series: wide-column. Friends of friends: graph.
- **EX02** Key-value: sessions/cart cache. Document: reviews/product attributes. Wide-column: activity/event log. Graph: "also bought" recommendations.
- **EX03** E.g. `orders_by_customer(customer_id, placed_at, order_id)`, `orders_by_status(status, placed_at, order_id)` (watch partition size), `order_by_id(order_id)`. Each table answers one query.
- **EX04** Ad hoc and new queries need new tables or a redesign; data is duplicated, so updates touch several places.
- **EX05** Cassandra-like: tunable, commonly leans to availability (AP) in a partition and low latency otherwise. Single-node PostgreSQL: no partition within one node; consistency is strong. PACELC: in the normal case, trade latency against consistency. Verify settings per product.

**Outcomes 1-3** are also checked by the quiz and the lab table.
