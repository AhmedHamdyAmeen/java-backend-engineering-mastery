# MID-031 · Distributed workflows — Exercises and lab

## Lab
### MID-031-LAB1 · Order saga
**Outcomes:** 1–4 · **Time:** ~4 h
Implement an orchestrated saga in `orders`: place order → reserve stock (`inventory`) → authorize payment (`payments`) → confirm. Persist saga state with a deadline. On payment failure, release stock and cancel the order. Handle timeouts with a sweeper. Use the outbox and inbox from MID-029 for all messages.

**Acceptance:** every failure path is tested end to end: stock failure, payment declined, payment timeout, duplicate and late replies, orchestrator restart mid-saga.

## Exercises (assessment: saga design for a new process, returns)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-031-EX01 | 1 | Explain in five sentences why 2PC across services is avoided and what replaces it. |
| MID-031-EX02 | 1 | Model "customer returns an item" as a saga: steps, local transactions, compensations, and non-undoable steps. |
| MID-031-EX03 | 2 | Compare choreography and orchestration for the returns saga and choose one with reasons. |
| MID-031-EX04 | 3 | Define the saga state enum and table for returns, including deadline and version. |
| MID-031-EX05 | 4 | Write an idempotent `refund` compensation that is safe if the payment was never captured. |
| MID-031-EX06 | 4 | A `Reserve` message arrives after `Release` for the same order. Describe the bug and the fix. |
| MID-031-EX07 | 3 | Define timeouts per step and what the sweeper does when each expires. |

## Solutions
- **EX01** 2PC holds locks across services, blocks on coordinator failure, multiplies unavailability, and often is unsupported. Use local transactions with compensations.
- **EX02** Steps: create return `REQUESTED`; receive item (`inventory`); refund (`payments`); restock; close. Compensations: cancel return; none for received item (flag for inspection); void refund request. A "refund email" is last and non-undoable.
- **EX03** Orchestration: five steps with branching (item rejected after inspection) and deadlines, so one owner of the flow is clearer. Choreography fits only if the flow stays linear.
- **EX04** `RETURN_REQUESTED, ITEM_RECEIVED, REFUNDED, COMPLETED, COMPENSATING, FAILED`; table `return_saga(id, state, deadline, attempts, version)`.
- **EX05** Look up capture by return id; if none or already refunded, return; otherwise refund with the return id as the idempotency key and store the refund id.
- **EX06** Without a record, the late reserve re-reserves stock that nobody releases. Store a tombstone (cancelled reservation by order id) and reject the reserve.
- **EX07** Example: reserve 30 s (retry twice, then compensate); payment 2 min (void and cancel); overall 10 min (mark `FAILED` and alert).

Quiz Q01 to Q03 also cover outcome 1; outcome 3 is mostly verified through the lab.
