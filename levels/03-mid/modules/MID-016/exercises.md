# MID-016 · Advanced transactions — Exercises and lab

## Lab
### MID-016-LAB1 · Concurrent product edits
**Outcomes:** 1–4 · **Time:** ~3 h
Add optimistic locking to `Product`: two admins editing the same product, the second gets HTTP 409 with the current version. Then make a deadlock-prone job (updates two products in opposite orders) retry safely with a limited, idempotent retry.
**Acceptance:** automated tests for both conflicts: the 409 case and the deadlock-then-retry case.

## Exercises (assessment: fix a transaction design)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-016-EX01 | 1 | Add `@Version` to an entity and show the SQL of an update with the version check. |
| MID-016-EX02 | 1 | Map the optimistic lock exception to a 409 response with the current version. |
| MID-016-EX03 | 2 | Choose optimistic, pessimistic, or atomic SQL for: profile edit, stock decrement, seat booking, nightly price update. Justify each. |
| MID-016-EX04 | 3 | Predict and verify what happens when a `@Transactional` method calls another method of the same class with `REQUIRES_NEW`. |
| MID-016-EX05 | 3 | With pool size 2, show a pool deadlock from `REQUIRES_NEW` and fix it. |
| MID-016-EX06 | 4 | Review a retry loop that retries a payment call and a DB write on any exception; list the problems and correct it. |

## Solutions
- **EX01** `update product set name=?, version=? where id=? and version=?`; version increments on success.
- **EX02** `@ExceptionHandler(ObjectOptimisticLockingFailureException.class)` returns 409 and re-reads the product for the body.
- **EX03** Profile edit: optimistic. Stock decrement: atomic `UPDATE`. Seat booking: pessimistic or unique constraint. Nightly price update: batch with optimistic check or lock by chunk (reasons vary; check justification).
- **EX04** No new transaction starts: self-invocation bypasses the Spring proxy; move to another bean.
- **EX05** Each request holds a connection and waits for another; with all connections taken, all wait until timeout. Fix: avoid nesting, enlarge pool only as a temporary measure, or write after commit.
- **EX06** Retry only transient exceptions, with a limit and backoff; payment needs an idempotency key; retry the whole transaction outside the transactional method.
- Common mistakes (non-idempotent retries, pool exhaustion) are in EX05 and EX06.
