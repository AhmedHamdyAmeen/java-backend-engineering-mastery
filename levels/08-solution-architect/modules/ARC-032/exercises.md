# ARC-032 · Integration with enterprise systems — Exercises and lab

## Lab
### ARC-032-LAB1 · Larkspur enterprise integration
**Outcomes:** 1–4 · **Time:** ~4 h
1. Define the system of record for each shared data set (products, prices, stock, orders, customers, consent, payments, identities).
2. Design the ERP integration (products, prices, stock, financial postings) with rate limiting and queueing.
3. Design the CRM integration (profiles, service cases, consent) and the identity-provider integration.
4. Design the payment gateway integration with idempotency, timeout handling, and reconciliation.
5. Define the anti-corruption layer for the ERP.
6. For every flow write what happens when the other side is down.
**Acceptance:** every flow defines the system of record and what happens when the other side is down.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-032-EX01 | 1 | Product prices live in the ERP but marketing wants to change web prices daily. Decide the system of record and flow. |
| ARC-032-EX02 | 1 | The platform shows availability; the ERP holds the stock book. Design the stock flow and the behavior when the ERP is down. |
| ARC-032-EX03 | 2 | A customer withdraws marketing consent in the app. Design propagation to the CRM, email tool, and analytics, and how you prove it. |
| ARC-032-EX04 | 3 | A payment authorization times out. Write the handling rules, including the webhook and a reconciliation step. |
| ARC-032-EX05 | 3 | The identity provider is unavailable for 20 minutes. Decide what customers and staff can still do. |
| ARC-032-EX06 | 4 | The ERP names customer orders "SO documents" with status codes 10, 20, 30. Design the anti-corruption layer and list what must not appear in the platform's API. |

## Solutions
- **EX01** The ERP stays the record for base price; a pricing service on the platform holds approved web price overrides with effective dates; changes governed by the price owner; overrides posted to the ERP for finance. Alternatively move web promo pricing ownership to a pricing system and sync to the ERP. Decision recorded with owner.
- **EX02** Events or CDC from the ERP into an availability store; reservations on the platform; periodic reconciliation. ERP down: sell from last-known availability with safety buffer; queue reservations; reconcile on recovery.
- **EX03** Preference center is master; publish a consent-withdrawn event; consumers acknowledge; sync check daily; audit entry with timestamps; target time agreed with legal; failures alert an owner.
- **EX04** Treat the result as unknown; use an idempotency key; do not retry blindly or tell the customer failed; query the provider; process verified webhook; mark order pending; reconcile nightly.
- **EX05** Existing sessions continue within validity; token verification with cached keys; new logins blocked or fall back to a limited path; staff via a separate break-glass process; message the customers; alert and escalate to the provider.
- **EX06** An adapter translating SO documents to Order, mapping codes to named statuses in a dictionary, translating errors; the platform API must not expose ERP codes, document numbers as keys, or field names; contract tests guard it.

**Workplace evidence:** an ERP, CRM, or payment integration you designed and its operational results.
