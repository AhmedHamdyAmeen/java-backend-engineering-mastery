# MID-062 · API evolution — Exercises and lab

## Lab
### MID-062-LAB1 · Money format change
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Classify the planned change (cents `long` to `{amount, currency}`) for the orders REST API and `OrderPlaced`.
2. Release 1: add `money` beside `total` in both; register the new schema version; extend contract tests for old and new shapes.
3. Migrate each consumer to `money` using a tolerant reader; track usage of `total`.
4. Release 2: announce deprecation, wait for usage to reach zero, then remove `total`.
**Acceptance:** contract tests and schema registry pass at every step.

## Exercises (assessment: change-classification quiz plus lab; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-062-EX01 | 1 | Classify eight changes (add optional field, rename field, enum value added, status 200 to 201, cents to euros, new endpoint, optional param made required, longer max length) as compatible or breaking. |
| MID-062-EX02 | 2 | Write an Avro (or Protobuf) v2 of `OrderPlaced` adding `currency` and show it passes BACKWARD checks; then show a change that fails. |
| MID-062-EX03 | 2 | Explain when you upgrade producers first and when consumers first, for BACKWARD and FORWARD modes. |
| MID-062-EX04 | 4 | Make a consumer DTO tolerant: ignore unknown properties and handle an unknown enum value. Test it with an extended payload. |
| MID-062-EX05 | 3 | Write a deprecation plan for `GET /orders?status=` parameter values: announcement text, metric, dates, removal criteria. |

## Solutions
- **EX01** Compatible: add optional field, new endpoint, usually a new enum value only if consumers are tolerant. Breaking: rename, cents to euros (meaning), optional made required, tighter max length for existing inputs. 200 to 201 is breaking for strict clients; treat as breaking unless agreed.
- **EX02** Add `{"name":"currency","type":"string","default":"EUR"}`; passes. Removing a field without a default, or adding a field without a default, fails BACKWARD.
- **EX03** BACKWARD: new schema reads old data, so upgrade consumers first. FORWARD: old schema reads new data, so upgrade producers first. FULL allows either order.
- **EX04** `@JsonIgnoreProperties(ignoreUnknown = true)` (or mapper config) and map unknown enum values to an `UNKNOWN` default; the test deserializes an extra field and a new enum value.
- **EX05** Announce in changelog and `Deprecation`/`Sunset` headers; metric of calls per client; message clients; sunset date after the measured migration; remove when usage is zero or the date passed with owners informed.
