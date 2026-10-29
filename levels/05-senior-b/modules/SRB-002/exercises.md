# SRB-002 · Event-driven architecture — Exercises and lab

## Lab
### SRB-002-LAB1 · Integration events
**Outcomes:** 1, 2, 3, 4 · **Time:** ~4 h
1. List the business facts exchanged between Shop and FulfillCo (OrderReadyForFulfillment, ShipmentDispatched, ...).
2. Define schemas, owners, topics, and compatibility rules for each.
3. Write replay rules, flagging consumers with side effects.
4. Hold a review with two role-played consuming teams and record their changes.
**Acceptance:** catalog reviewed by two role-played consuming teams; each event has owner, schema, and replay rule.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-002-EX01 | 1 | Classify three proposed events (OrderUpdated row dump, OrderPlaced, ShipmentDelayed ping) as notification, state transfer, or domain event. |
| SRB-002-EX02 | 1 | Write the OrderReadyForFulfillment schema for the warehouse team with privacy in mind. |
| SRB-002-EX03 | 2 | Who owns ShipmentDispatched? Write the catalog entry. |
| SRB-002-EX04 | 3 | A team wants to rename carrierCode to carrier. Describe the migration. |
| SRB-002-EX05 | 4 | Plan a backfill of 90 days of events to a new analytics consumer. |
| SRB-002-EX06 | 4 | Review a consumer that charges cards on PaymentRequested. Is replaying the topic safe? |

## Solutions
- **EX01** Row dump: leaked internal state; OrderPlaced: domain event; ping: notification. Redesign the row dump as a domain event.
- **EX02** Order id, line items with SKU and quantity, promised date, minimal delivery reference; no payment data.
- **EX03** FulfillCo-shipping; entry with topic, schema, sensitivity, consumers, replay-safe flag.
- **EX04** Add the new optional field, publish both, migrate consumers, deprecate with a date, then remove in a new version.
- **EX05** Throttle, use a separate consumer group, idempotent writes, verify counts, no side effects.
- **EX06** No; require idempotency keys at the payment provider and a processed-event table.

**Workplace evidence:** an event contract you designed that another team consumes.
