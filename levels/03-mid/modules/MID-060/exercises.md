# MID-060 · DDD introduction — Exercises and lab

## Lab
### MID-060-LAB1 · Order aggregate
**Outcomes:** 1–3 · **Time:** ~3 h
1. Redesign `Order` with `OrderId`, `Money`, `OrderLine`; remove public setters.
2. Enforce inside `Order`: status transitions (NEW → PLACED → PAID → SHIPPED), line totals, and cancellation rules (no cancel after shipping).
3. Raise `OrderPlaced` and `OrderCancelled` events from the aggregate.
4. Keep `OrderRepository` as a domain interface; services only orchestrate.
5. Write unit tests per invariant; add a short glossary of the language used.
**Acceptance:** no invariant enforced in services; unit tests per invariant.

## Exercises (assessment: aggregate design for an unseen domain; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-060-EX01 | 1 | Classify as entity or value object: `Customer`, `Money`, `Address`, `Order`, `DateRange`. Justify each. |
| MID-060-EX02 | 1 | Implement `Email` as a record that rejects invalid input, plus an equality test. |
| MID-060-EX03 | 2 | For a hotel booking domain, list the invariants and draw the aggregates; keep them small. |
| MID-060-EX04 | 2 | Find and fix the problem: `class Order { Customer customer; List<Product> products; }`. |
| MID-060-EX05 | 3 | Decide where logic goes: "apply a voucher across several orders", "an order cannot ship unpaid". |
| MID-060-EX06 | 4 | Run a mini glossary session on a domain of your choice (6 terms) and rename five code identifiers to match. |

## Solutions
- **EX01** Entities: `Customer`, `Order` (identity). Value objects: `Money`, `Address`, `DateRange` (equal values interchangeable).
- **EX02** `record Email(String value) { Email { if (!value.matches(".+@.+\\..+")) throw new IllegalArgumentException(); } }`; two instances with the same value are equal.
- **EX03** Example: `Booking` protects "check-out is after check-in" and "status flow"; "no overlapping bookings for a room" is a cross-aggregate rule, handled by a `Room` availability aggregate or a domain service. Keep `Booking`, `Room`, `Guest` separate, linked by IDs. Accept any design that ties aggregates to invariants.
- **EX04** Replace with `CustomerId` and `List<OrderLine>` holding `ProductId`, quantity, and unit price snapshot; aggregates reference others by ID.
- **EX05** Voucher across orders: domain service (spans aggregates). "Cannot ship unpaid": inside `Order.ship()`.
- **EX06** Judged against the glossary; code names must match business terms.
