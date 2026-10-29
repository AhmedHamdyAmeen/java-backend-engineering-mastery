# MID-025 · Service boundaries — Exercises and lab

## Lab
### MID-025-LAB1 · Split Shop
**Outcomes:** 1–4 · **Time:** ~3 h
1. Draw Shop's context map from language and ownership, not from tables.
2. Extract `orders`, `inventory`, and `payments` into separate services, each with its own database or schema and credentials.
3. Replace each cross-service join with an API call, an event, a local copy, or a snapshot.
4. Document the data ownership table and the context map.
**Acceptance:** no service reads another's tables; context map documented.

## Exercises (assessment: boundary review of an unseen system; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-025-EX01 | 1 | Given a glossary of a clinic system, propose three bounded contexts and justify them by language. |
| MID-025-EX02 | 2 | Make a data ownership table for Shop (stock level, price, order status, payment status, customer email). |
| MID-025-EX03 | 3 | An order-history page joins orders, products, and customers. Propose two replacements and compare them. |
| MID-025-EX04 | 3 | Design a local copy of `customerEmail` in `notifications`: source events, update rule, staleness risk. |
| MID-025-EX05 | 4 | Evaluate a proposed boundary "UserService, AddressService, PhoneService" by coupling and change patterns. |

## Solutions
- **EX01** For example Scheduling (appointment, slot), Clinical (visit, diagnosis), Billing (invoice, claim); "patient" differs per context.
- **EX02** Stock level: inventory; price: catalog; order status: orders; payment status: payments; customer email: customer/identity service. Others read via API or events.
- **EX03** (a) API composition in a gateway; (b) snapshots in order lines plus a local customer name copy. Compare freshness, latency, and coupling.
- **EX04** Consume `CustomerEmailChanged` events; upsert by `customerId`; stale for seconds to minutes; fall back to an API call if missing.
- **EX05** Boundary by entity: one change (a profile page) touches three services and needs many calls; merge them into one Customer context.
