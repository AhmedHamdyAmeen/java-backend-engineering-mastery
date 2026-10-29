# MID-026 · Messaging fundamentals — Exercises and lab

## Lab
### MID-026-LAB1 · Event catalog
**Outcomes:** 1–4 · **Time:** ~2 h
1. List Shop's business events: `OrderPlaced`, `StockReserved`, `StockReservationFailed`, `PaymentAuthorized`, `PaymentFailed`, `OrderCancelled`, and others you find.
2. For each give: owner service, past-tense name, schema (fields and types), version, key, consumers.
3. Mark which messages are commands, and keep them out of the event list.
4. Have a peer review the catalog.
**Acceptance:** reviewed catalog used by later labs.

## Exercises (assessment: quiz plus catalog review; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-026-EX01 | 1 | For notification emails, work distribution to image resizers, and order events, choose queue or topic and justify. |
| MID-026-EX02 | 2 | Classify and rename if needed: `SendEmail`, `OrderShippedEvent`, `UpdateInventoryNow`, `PriceChanged`. |
| MID-026-EX03 | 3 | Explain why exactly-once delivery is not available end to end, using a lost-ack timeline. |
| MID-026-EX04 | 3 | Write idempotent handling for `PaymentAuthorized` using the `eventId`. |
| MID-026-EX05 | 4 | Design `OrderPlaced` payloads in minimal and full-state versions and compare them. |

## Solutions
- **EX01** Emails and resizers: queue (competing consumers). Order events: topic (several independent subscribers).
- **EX02** `SendEmail` command; `OrderShippedEvent` event (name as `OrderShipped`); `UpdateInventoryNow` command; `PriceChanged` event.
- **EX03** Consumer processes and acks, but the ack is lost; the broker redelivers. The broker cannot know whether processing happened.
- **EX04** Store processed `eventId`s in a table with a unique constraint, in the same transaction as the effect; on duplicate key skip.
- **EX05** Minimal: `{eventId, orderId}`, consumers call `orders` back (coupling, load). Full: includes lines and totals (autonomous consumers, bigger, schema must be versioned).
