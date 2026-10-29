# JNR-032 · ORM pitfalls — Exercises and lab

## Lab
### JNR-032-LAB1 · Fix the order list
**Outcomes:** 1–4 · **Time:** ~3 h
1. Run the provided order-history endpoint with 100 orders; record the number of SQL statements (101).
2. Write a test with a query counter asserting at most 2 queries; it must fail first.
3. Fix with a fetch join, entity graph, or projection; keep pagination safe (page ids, then load).
4. Disable Open Session in View and make sure no `LazyInitializationException` appears.
5. Re-run the test; it passes.

**Acceptance:** test fails before, passes after; at most 2 queries for 100 orders.

## Exercises (assessment: diagnose a slow endpoint from logs)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-032-EX01 | 1 | From a provided SQL log, count the queries and point out the repeated one. |
| JNR-032-EX02 | 2 | Fix the same endpoint twice: with `join fetch` and with `@EntityGraph`. |
| JNR-032-EX03 | 2 | Replace entity loading with a projection for an order-summary list. |
| JNR-032-EX04 | 3 | Explain when `LazyInitializationException` happens and give two correct fixes (and one wrong). |
| JNR-032-EX05 | 4 | Write the two-step query that pages orders with their lines safely. |
| JNR-032-EX06 | 1-4 | Diagnose a slow endpoint from provided logs; write cause, evidence, and fix. |

## Solutions
- **EX01** One `select ... from orders` followed by N identical `select ... from order_line where order_id=?`; N+1.
- **EX02** `select distinct o from Order o join fetch o.lines` and `@EntityGraph(attributePaths = "lines")`.
- **EX03** `select new ...OrderSummary(o.id, o.createdAt, c.name) from Order o join o.customer c` returned as a `Page`.
- **EX04** Raised when a lazy relation is read after the context closed. Fixes: fetch join or entity graph; DTO built in the transaction. Wrong fix: switch to `EAGER` globally.
- **EX05** Step 1: page of order ids; step 2: `select distinct o from Order o join fetch o.lines where o.id in :ids`.
- **EX06** Look for repeated selects, missing paging, or OSIV; cite log lines as evidence.
