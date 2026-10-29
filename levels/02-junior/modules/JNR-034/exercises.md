# JNR-034 · Database constraints — Exercises and lab

## Lab
### JNR-034-LAB1 · Race the duplicate
**Outcomes:** 1–4 · **Time:** ~2 h
1. Implement product creation with an application check only (`existsBySku` then `save`).
2. Write a concurrent test: two threads released together create the same SKU; show it can create two rows.
3. Add a unique constraint through a Flyway migration.
4. Map the violation to a 409 response with a problem-details body.
5. Add an index on `order_line.order_id`; show the plan with `EXPLAIN`.

**Acceptance:** the concurrent test reliably produces one success and one 409.

## Exercises (assessment: add constraints and indexes to a schema from requirements)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-034-EX01 | 1 | Add unique, foreign-key, not-null, and check constraints to a provided `customer`/`orders` schema. |
| JNR-034-EX02 | 1 | Write a composite unique constraint: one review per customer per product. |
| JNR-034-EX03 | 2 | Write an exception handler that maps a duplicate email to 409 and a check violation to 400. |
| JNR-034-EX04 | 3 | Explain with a timeline why `existsBy` then `save` can produce duplicates. |
| JNR-034-EX05 | 4 | Create indexes for foreign keys and a common lookup; explain why you did not index every column. |
| JNR-034-EX06 | 4 | Run `EXPLAIN` before and after an index and say what changed in the plan. |

## Solutions
- **EX01** `unique (email)`, `foreign key (customer_id) references customer(id)`, `not null` on required columns, `check (total >= 0)`.
- **EX02** `alter table review add constraint ux_review_customer_product unique (customer_id, product_id);`
- **EX03** `@ExceptionHandler(DataIntegrityViolationException.class)` returning `ProblemDetail` with `HttpStatus.CONFLICT` for the unique constraint name and `BAD_REQUEST` for the check constraint name.
- **EX04** T1 checks: none. T2 checks: none. T1 inserts, T2 inserts. Both succeeded because neither saw the other's uncommitted insert.
- **EX05** Index foreign keys (`order_line.order_id`) and columns in frequent `where` and `join`; extra indexes slow writes and use space.
- **EX06** Before: `Seq Scan` on the table; after (on a large enough table): `Index Scan` using the new index, lower cost.
