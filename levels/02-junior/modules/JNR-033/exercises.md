# JNR-033 · Schema migrations — Exercises and lab

## Lab
### JNR-033-LAB1 · Migrate Shop
**Outcomes:** 1–4 · **Time:** ~2 h
1. Add Flyway and convert the manual schema to `V1__baseline.sql`.
2. Set `ddl-auto=validate`; fix any mapping/schema mismatch it reports.
3. Add `V2__add_sku.sql`: add `sku`, backfill existing rows, then set `not null` and a unique index.
4. Put reference data (order statuses) in `V3`; keep demo data in test-only scripts.
5. Reach the same schema on a fresh database and on an existing one (baseline).

**Acceptance:** fresh database and existing database both reach the same state.

## Exercises (assessment: write a migration for a new requirement)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-033-EX01 | 1 | Name three migration files correctly and explain how Flyway orders them. |
| JNR-033-EX02 | 2 | An applied `V4` has a typo. Explain what happens if you edit it and what to do instead. |
| JNR-033-EX03 | 2 | Write the safe three-step migration to add a `not null` column to a table with rows. |
| JNR-033-EX04 | 3 | Classify as reference or test data: order statuses, 50 fake customers, country list, a demo admin password. |
| JNR-033-EX05 | 4 | Show what `ddl-auto=validate` reports when an entity has a field that the table lacks. |
| JNR-033-EX06 | 1, 2 | Write a migration for a new requirement: "products have an optional `weight_grams` that must be positive when present". |

## Solutions
- **EX01** `V1__baseline.sql`, `V2__add_sku.sql`, `V3__seed_status.sql`; ordered by version number, not alphabetically as text.
- **EX02** The checksum differs and Flyway refuses to start; add `V5__fix_typo.sql` instead.
- **EX03** `alter table ... add column x text;` then `update ... set x = ...;` then `alter table ... alter column x set not null;`.
- **EX04** Reference: statuses, countries. Test: fake customers, demo admin password (never in production).
- **EX05** Startup fails with a schema-validation error naming the missing column.
- **EX06** `alter table product add column weight_grams integer; alter table product add constraint ck_product_weight check (weight_grams is null or weight_grams > 0);`
