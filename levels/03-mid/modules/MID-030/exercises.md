# MID-030 · Distributed consistency — Exercises and lab

## Lab
### MID-030-LAB1 · Consistency budget
**Outcomes:** 1–3 · **Time:** ~2 h
List every Shop operation (browse catalog, search, add to cart, place order, pay, reserve stock, order history, admin price change, stock display). For each, specify the required consistency model, acceptable staleness, and how the UI behaves during lag (for example "order pending"). Get the table reviewed and apply it to the API: status fields, `202` responses, and read paths.

**Acceptance:** reviewed table applied to the API; each row maps to a concrete endpoint behavior.

## Exercises (assessment: scenario quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-030-EX01 | 1 | Give one Shop example each for strong, eventual, causal, and read-your-writes consistency. |
| MID-030-EX02 | 1 | A user changes their address and sees the old one on refresh. Name the missing guarantee and two ways to provide it. |
| MID-030-EX03 | 2 | A colleague says "Kafka is AP, so we have no consistency problems to design for." Correct the statement. |
| MID-030-EX04 | 2 | Explain PACELC in four sentences using sync vs async replication. |
| MID-030-EX05 | 3 | Choose the consistency level for: last-item stock reservation, product reviews count, payment status. Justify each. |
| MID-030-EX06 | 3 | Redesign "place order" so the UI is honest about asynchronous steps: statuses and endpoints. |

## Solutions
- **EX01** Strong: reserving the last unit. Eventual: view counters. Causal: a review reply after its review. Read-your-writes: my order list after checkout.
- **EX02** Read-your-writes. Return the updated resource in the write response; read from the primary right after a write; wait for a version.
- **EX03** AP/CP describes behavior during a partition for a specific operation and configuration; consumers still see lag, duplicates, and reordering, so consistency must be designed per use case.
- **EX04** During a partition choose availability or consistency. Otherwise choose latency or consistency. Sync replication waits for replicas: consistent, slower. Async replication returns early: faster, stale reads possible.
- **EX05** Stock: strong (one owner, transactional decrement). Review count: eventual. Payment status: strong at the payment service, shown to users as eventual with explicit states.
- **EX06** `POST /orders` returns `202` and `Location`; statuses `PENDING`, `CONFIRMED`, `REJECTED`; `GET /orders/{id}` shows status; UI polls or subscribes.

Outcome 2 is also covered by quiz Q04 to Q07; the lab covers outcome 3 at API level.
