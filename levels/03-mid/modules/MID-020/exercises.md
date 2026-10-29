# MID-020 · Database migrations — Exercises and lab

## Lab
### MID-020-LAB1 · Zero-downtime rename
**Outcomes:** 1–4 · **Time:** ~3 h
Rename `customer.name` to `full_name` across several releases of Shop while a load test runs. Use Flyway for each step, a batched backfill, `lock_timeout`, and a written rollback for each release.
**Acceptance:** zero failed requests during the whole migration; a rollback note per step.

## Exercises (assessment: migration plan review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-020-EX01 | 1 | Write an expand-contract plan to split `address` into `street` and `city`. |
| MID-020-EX02 | 1 | Explain what each running app version needs from the schema at each step of your plan. |
| MID-020-EX03 | 2 | Classify these as safe or risky and give the safe form: add index, add `NOT NULL` column, add foreign key, change column type. |
| MID-020-EX04 | 2 | Show a migration that sets `lock_timeout` and creates an index concurrently; explain why it cannot run in a transaction. |
| MID-020-EX05 | 3 | Write a resumable batched backfill for 50 M rows and explain its batch size and pauses. |
| MID-020-EX06 | 4 | Fill a rollback table for each step of EX01. |
| MID-020-EX07 | 4 | Review a one-step migration plan (rename + drop + add NOT NULL) and list its failure modes. |

## Solutions
- **EX01** Release 1 add nullable `street`, `city`; 2 dual-write; 3 backfill by parsing; 4 read new; 5 stop writing `address`; 6 drop `address`.
- **EX02** Old app: needs the old columns until it is gone; new app: tolerates missing data in the new columns until backfill finishes.
- **EX03** Index: use `CONCURRENTLY`. `NOT NULL` column: add nullable, backfill, then constraint (or constant default). Foreign key: `NOT VALID` then `VALIDATE`. Type change: new column plus backfill plus swap, not an in-place rewrite.
- **EX04** `CREATE INDEX CONCURRENTLY` waits for existing transactions and cannot be wrapped in a transaction block; configure Flyway to run that script outside a transaction.
- **EX05** Loop by id range of 5 000 rows, each in its own transaction, `WHERE new IS NULL`, a short sleep, and a stored progress marker; check replication lag.
- **EX06** Expand steps: redeploy the prior app, leave columns; backfill: rerun or clear; switch reads: redeploy old; contract: restore from backup (point of no return).
- **EX07** Old instances fail on rename or drop; `NOT NULL` fails on existing nulls or blocks while scanning; no rollback; table lock queue pile-up.
- The "volatile default" mistake is discussed in EX03 and the quiz.
