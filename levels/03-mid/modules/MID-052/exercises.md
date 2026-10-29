# MID-052 · Application threats — Exercises and lab

## Lab
### MID-052-LAB1 · Threat model
**Outcomes:** 1–4 · **Time:** ~2.5 h
Draw the DFD of Shop Platform with trust boundaries. Apply STRIDE, record threats with mitigations, rank the top five, and write a security test for each. Include at least two business-logic abuse cases.
**Acceptance:** reviewed threat model stored in Git; the five tests run in CI.

## Exercises (assessment: threat model review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-052-EX01 | 1 | Draw the DFD for `POST /orders` and mark the trust boundaries. |
| MID-052-EX02 | 1 | Give one STRIDE threat and mitigation for the Kafka `OrderPlaced` flow. |
| MID-052-EX03 | 2 | `GET /orders/42` returns another customer's order. Name the weakness and the fix. |
| MID-052-EX04 | 2 | A normal user can call `DELETE /admin/products/7`. Name the weakness and the fix. |
| MID-052-EX05 | 3 | Design abuse prevention for a "10% first-order" promo and for login. |
| MID-052-EX06 | 4 | Turn the threat "price tampering" into a test and a rule for reviews of new endpoints. |

## Solutions
- **EX01** Browser → gateway (boundary) → orders → PostgreSQL and Kafka; payments is an external entity behind another boundary.
- **EX02** Tampering: a forged event. Mitigate with broker ACLs per producer, schema validation, and consumer-side checks.
- **EX03** BOLA. Check the order's owner against the token's subject on every access; return 404.
- **EX04** Broken function-level authorization. Enforce a role or scope on admin routes and test with a user token.
- **EX05** Promo: unique constraint on (customer, promo), verified identity, limits per device and payment method. Login: rate limit per account and IP, MFA, breached-password check, generic error messages.
- **EX06** Test: send a price of 0.01 in the body and assert the order total uses the catalog price. Add the threat to the model so reviews of new endpoints ask it again.

**Outcome 2** is also covered by quiz Q03–Q05; the lab covers outcomes 1, 3, and 4 end to end.
