# ARC-026 · Event architecture — Exercises and lab

## Lab
### ARC-026-LAB1 · Event catalog
**Outcomes:** 1–4 · **Time:** ~3 h
1. List Larkspur's business events: order placed, stock changed, shipment dispatched, return received, plus any others you find.
2. Assign one owner per event with the reason.
3. Write schemas, examples, and the consumer list for each event.
4. Write compatibility rules and an evolution process with a retirement policy.
5. Score the need for an event backbone and record the decision.
6. Defend the catalog in a catalog review.
**Acceptance:** no event has two owners; evolution process documented.

## Exercises (case-based; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-026-EX01 | 1 | Both the platform and the ERP publish "OrderConfirmed". Decide the owner and fix the situation. |
| ARC-026-EX02 | 2 | Write a catalog entry for ShipmentDispatched with schema, owner, consumers, and delivery guarantee. |
| ARC-026-EX03 | 3 | Classify seven schema changes as compatible or breaking and give the migration path for the breaking ones. |
| ARC-026-EX04 | 4 | A department with three systems and ten messages a day asks for a streaming platform. Write your recommendation. |
| ARC-026-EX05 | 1, 2 | Review an event "CustomerTableChanged" mirroring a CRM table; redesign it as business events. |

## Solutions
- **EX01** The system that decides the confirmation (platform) owns it; the ERP publishes its own fact such as OrderAccepted, or consumes the platform event.
- **EX02** Fields: shipmentId, orderId, carrier, trackingNumber, dispatchedAt, lines; owner fulfillment; consumers platform, CRM, customer notifications; at-least-once, so consumers deduplicate by shipmentId.
- **EX03** Compatible: add optional field, add enum value tolerated by readers, widen documentation. Breaking: remove, rename, retype, change meaning of a field, add required field. Use add-then-deprecate or a v2 event with overlap and retirement date.
- **EX04** Not justified: low volume and few consumers; use APIs or a managed queue; revisit when producers, consumers, or replay needs grow.
- **EX05** Table mirrors leak the CRM schema; publish CustomerRegistered, ConsentChanged, and AddressChanged with business fields.

Outcomes 3 and 4 are also covered by the quiz and the lab rules.

**Workplace evidence:** an event catalog or event standard you established.
