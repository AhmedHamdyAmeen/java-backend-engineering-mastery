# MID-064 · Estimation and delivery — Exercises and lab

## Lab
### MID-064-LAB1 · Returns feature plan
**Outcomes:** 1–4 · **Time:** ~2 h
1. Turn a one-paragraph request for returns and refunds into questions.
2. Write acceptance criteria from the answers.
3. Slice the feature vertically; estimate each slice as a range.
4. List the top risks; plan a spike for the riskiest.
5. Send a progress update after the first slice.
**Acceptance:** reviewed plan; first slice delivered.

## Exercises (assessment: planning exercise; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-064-EX01 | 1 | Write ten clarifying questions for "let customers apply discount codes". |
| MID-064-EX02 | 1 | Write three Given/When/Then criteria for a gift-wrapping option. |
| MID-064-EX03 | 2 | Split "order history page with filters and export" into five vertical slices. |
| MID-064-EX04 | 3 | Estimate three slices as ranges with confidence and assumptions; name the riskiest assumption and a one-day spike to test it. |
| MID-064-EX05 | 4 | Write a progress update for a feature that is two days behind, including cause and options. |

## Solutions
- **EX01** For example: stackable, expiry, per-user limits, percent versus fixed, applies to shipping, behavior on refunds, who creates codes, abuse limits, reporting, out of scope.
- **EX02** Given an order, when wrapping is chosen, then price rises by the wrap fee; given an out-of-stock wrap type, then checkout shows an error; given a cancelled order, then the fee is refunded.
- **EX03** Basic list; paging; one filter; more filters; export of current filter. Each is releasable.
- **EX04** For example 1-2 days (90%), 2-4 days (80%), 3-8 days (60%, depends on provider); spike: call the provider sandbox with a partial refund.
- **EX05** Done, next, new range, cause, options: cut scope, move date, or add a helper; ask for a decision by a date.
