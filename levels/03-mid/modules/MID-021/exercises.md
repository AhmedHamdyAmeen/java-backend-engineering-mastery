# MID-021 · Advanced Hibernate — Exercises and lab

## Lab
### MID-021-LAB1 · Batch job tuning
**Outcomes:** 1–4 · **Time:** ~3 h
Make Shop's nightly price-update job (100 000 products) 10× faster without leaving JPA: fetch plan, JDBC batching, periodic flush/clear, and (if useful) a cache decision for the category lookup.
**Acceptance:** statement counts and timings before and after, recorded with Hibernate statistics.

## Exercises (assessment: tuning exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-021-EX01 | 1 | Fix an N+1 on `Order.items` with an entity graph and verify the statement count in a test. |
| MID-021-EX02 | 1 | Write a DTO projection for the order list screen and compare the SQL with loading entities. |
| MID-021-EX03 | 2 | Configure batching and show the effect on 10 000 updates. |
| MID-021-EX04 | 2 | Change an `IDENTITY` id to a sequence and show insert batching starting to work. |
| MID-021-EX05 | 3 | Decide for five entities whether to use the second-level cache and justify each. |
| MID-021-EX06 | 4 | Explain what happens with `persist`, `merge`, and `save` on a detached entity, and what each returns. |
| MID-021-EX07 | 4 | Fix a bug where code modifies the object passed to `merge` expecting changes to be saved. |

## Solutions
- **EX01** `@EntityGraph(attributePaths = "items")` on the repository method; assert `getPrepareStatementCount()` equals 1.
- **EX02** `select new ...OrderSummary(...)`: fewer columns, no entity instances, no lazy-loading risk.
- **EX03** `batch_size=50`, `order_updates=true`: the statement execution count drops from 10 000 to about 200 batches (measured values vary).
- **EX04** `@GeneratedValue(strategy = SEQUENCE)` with matching `allocationSize` and a sequence `INCREMENT BY` of the same size; Hibernate logs batched inserts.
- **EX05** Cache read-mostly reference data (category, country); avoid stock, orders, and anything written often. Check the reasons given.
- **EX06** `persist` on a detached entity throws; `merge` returns a managed copy; `save` calls `merge` for entities with an id and returns the saved instance.
- **EX07** Use the returned managed instance: `var managed = em.merge(x); managed.setName(...)`; the original remains detached.
- The "`saveAll` without batching" mistake is shown in EX03 and the lab; caching mutable entities in EX05.
