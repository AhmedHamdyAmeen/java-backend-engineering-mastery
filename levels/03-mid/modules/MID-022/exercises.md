# MID-022 · Alternative persistence — Exercises and lab

## Lab
### MID-022-LAB1 · Dashboard read model
**Outcomes:** 1–3 · **Time:** ~3 h
Build an admin dashboard for Shop (orders and revenue per day, top products): a `dashboard_daily` read-model table updated when orders are placed, queried with jOOQ, with a rebuild command. Write a decision record comparing JDBC, jOOQ, and JPA for this feature.
**Acceptance:** a written decision record comparing the three approaches; the dashboard served from the read model with a working rebuild.

## Exercises (assessment: decision-record review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-022-EX01 | 1 | Configure jOOQ code generation from the Flyway-migrated schema in the build. |
| MID-022-EX02 | 1 | Write a jOOQ query with a join, group by, and filter, and map it to a DTO. |
| MID-022-EX03 | 2 | Choose JDBC, jOOQ, or JPA for: order placement, monthly report, bulk price update, product CRUD. Justify. |
| MID-022-EX04 | 2 | Explain how JPA and jOOQ can share one transaction in a Spring service. |
| MID-022-EX05 | 3 | Design a read-model table for the dashboard and decide how it is updated (same transaction or event) and why. |
| MID-022-EX06 | 3 | Write the rebuild query that recreates the read model from the write tables. |

## Solutions
- **EX01** jOOQ code generator plugin pointing to a Testcontainers/PostgreSQL database after Flyway migration; generated sources added to the build.
- **EX02** `dsl.select(...).from(...).join(...).on(...).where(...).groupBy(...).fetchInto(Dto.class)`.
- **EX03** Order placement: JPA. Monthly report: jOOQ. Bulk price update: set-based SQL via jOOQ or JDBC. Product CRUD: JPA. Check the justification.
- **EX04** Both use the same `DataSource` and Spring transaction manager; `DSLContext` uses the transaction-bound connection.
- **EX05** For example `dashboard_daily(day pk, orders, revenue)`; update in the same transaction for exact numbers or from an after-commit event for looser coupling; state staleness.
- **EX06** `INSERT ... SELECT date_trunc('day', created_at), count(*), sum(total_cents) FROM orders GROUP BY 1 ON CONFLICT (day) DO UPDATE ...`.
- Mixing without boundaries and full event-sourced CQRS for simple reads are covered by EX03, EX05, and the decision record.
