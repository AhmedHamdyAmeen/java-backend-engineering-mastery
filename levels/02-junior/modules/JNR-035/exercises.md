# JNR-035 · Security fundamentals — Exercises and lab

## Lab
### JNR-035-LAB1 · Shop threat list
**Outcomes:** 1–4 · **Time:** ~1.5 h
Draw the Shop API's data flow with trust boundaries. List the top 10 threats, each with a planned control.
**Acceptance:** diagram and ten threat/control rows committed; becomes the capstone's "documented security controls" seed.

## Exercises (assessment: threat list review)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-035-EX01 | 1 | Map each to C, I, or A: leaked customer emails; a price changed in transit; a server flooded with requests. |
| JNR-035-EX02 | 1 | Write three goals an attacker might have against the Shop API. |
| JNR-035-EX03 | 2 | List the trust boundaries in: browser, Shop API, PostgreSQL, payment provider, log aggregator. |
| JNR-035-EX04 | 3 | The Shop app connects to the database as the admin user. Apply least privilege. |
| JNR-035-EX05 | 3 | Name three layers of defense for the "view order" endpoint. |
| JNR-035-EX06 | 4 | List five assets and five entry points of the Shop API. |

## Solutions
- **EX01** Emails: confidentiality; price changed: integrity; flooded server: availability.
- **EX02** For example: read others' orders, get goods for free, take the site down, take over accounts.
- **EX03** Browser | API; API | database; API | payment provider; API | log aggregator.
- **EX04** Create an app user with only the needed privileges on its schema; keep migrations on a separate account.
- **EX05** Authentication, ownership check, input validation, database account limits, audit logging.
- **EX06** Assets: customer data, orders, credentials, catalog integrity, availability. Entry points: login, register, catalog, cart, orders endpoints (and headers/tokens).
- Outcome 4 is also covered by the lab acceptance.
