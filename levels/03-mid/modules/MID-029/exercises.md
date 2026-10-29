# MID-029 · Reliable messaging — Exercises and lab

## Lab
### MID-029-LAB1 · Reliable order events
**Outcomes:** 1–4 · **Time:** ~4 h
1. In `orders`, add an `outbox` table and write an `OrderPlaced` row in the same transaction as the order.
2. Build a polling relay (`SKIP LOCKED`, batch of 100) that publishes to Kafka keyed by order id and marks rows sent.
3. In `inventory` and `payments`, add an `inbox` table (event id primary key) and apply effects in the same transaction as the inbox insert.
4. Configure retries with exponential backoff and a limit, and a DLQ for permanent failures.
5. Write a chaos script that kills each service (orders, relay, inventory, payments, Kafka) at random points during a stream of orders, then restarts them.

**Acceptance:** after the chaos script, every placed order produced exactly one stock reservation and one payment authorization: no lost and no double-applied events.

## Exercises (assessment: failure-injection review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-029-EX01 | 1 | List the two orderings of "commit" and "publish" and the failure each allows. |
| MID-029-EX02 | 2 | Write the SQL for an outbox table and the service method that writes order and event atomically. |
| MID-029-EX03 | 2 | Compare polling and CDC relays in a table: latency, load, infrastructure, ordering. |
| MID-029-EX04 | 3 | Classify as naturally idempotent or not: set status to SHIPPED; add 5 to stock; insert a row with a fixed id; send an email. Make the non-idempotent ones safe. |
| MID-029-EX05 | 3 | Implement an inbox check that works under two concurrent deliveries of the same event. |
| MID-029-EX06 | 4 | Choose retry limits and backoff for a payment-authorization consumer; list two errors that go straight to the DLQ. |
| MID-029-EX07 | 1–4 | Failure-injection review: for each step of the pipeline, state what happens if the process dies right there. |

## Solutions
- **EX01** Commit then publish: crash between loses the event. Publish then commit: crash or rollback publishes an event for state that does not exist.
- **EX02** `outbox(id, aggregate_id, type, payload, created_at, sent_at)`; method annotated `@Transactional` calls `orders.save(o)` and `outbox.save(...)`; no broker call inside.
- **EX03** Polling: seconds of latency, extra DB queries, no new infrastructure, ordered by `created_at`. CDC: very low latency, reads the log, needs connectors and ops, ordered by log position.
- **EX04** SHIPPED and fixed-id insert are idempotent. Add 5 to stock and send email are not: record the event id in an inbox (or keep a per-event ledger row) so the effect runs once; for email, store a "sent" flag keyed by event id.
- **EX05** Insert the event id with a primary key in the same transaction as the effect; the second transaction hits a unique violation and rolls back or skips. `INSERT ... ON CONFLICT DO NOTHING` and check the row count.
- **EX06** Example: 5 attempts, 500 ms start, factor 2, capped at ~30 s; permanent: malformed JSON, unknown product id. Timeouts and 503s retry.
- **EX07** Table of steps: after save+outbox commit (event still in outbox, relay sends later), after publish before mark-sent (duplicate published, inbox absorbs), after inbox insert before commit (rolled back together, redelivered), after DLQ publish (offset committed).

All four outcomes are also exercised by the quiz and by the lab's chaos criterion.
