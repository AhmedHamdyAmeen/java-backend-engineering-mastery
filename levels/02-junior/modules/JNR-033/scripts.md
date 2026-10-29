# JNR-033 · Schema migrations — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** version history for the database, like Git commits that every environment replays in order.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-033-L01 · Why the schema needs version control (8 min)
**Goal:** explain why manual schema scripts and `ddl-auto` fail.

**Key points**
- Code is versioned in Git, but the database lives elsewhere; they must change together.
- Manual `schema.sql` runs drift: dev, test, and production end up different.
- `spring.jpa.hibernate.ddl-auto=update` guesses changes, cannot rename or drop safely, and must not be used outside throwaway experiments.
- A migration is a small numbered SQL script, applied once, in order.
- The database remembers which ones ran.

**Show:** a diagram: `V1` → `V2` → `V3` applied to dev, test, and production in the same order.

**Check:** Why not `ddl-auto=update` in production? *(It guesses changes and can be unsafe or incomplete; schema changes must be explicit and reviewed.)*

---

## JNR-033-L02 · Flyway basics (12 min)
**Goal:** run versioned migrations at startup.

**Key points**
- Add `flyway-core` (and the PostgreSQL module if your Flyway version needs it: verify version before recording).
- Place files in `src/main/resources/db/migration` named `V1__baseline.sql`, `V2__add_sku.sql` (two underscores).
- At startup Flyway applies pending files and records them in `flyway_schema_history` with a checksum.
- Changing an applied file changes its checksum, and startup fails.
- For an existing database use baseline (`baseline-on-migrate`, with a baseline version) to mark what already exists.

**Show**
```sql
-- V1__baseline.sql
create table category (id bigint generated always as identity primary key, name text not null);
create table product (
  id bigint generated always as identity primary key,
  name text not null,
  price numeric(12,2) not null,
  category_id bigint references category(id));
```

**Check:** Where does Flyway store what it has applied? *(In the `flyway_schema_history` table.)*

---

## JNR-033-L03 · Writing safe migrations (10 min)
**Goal:** write migrations that are forward-only and low risk.

**Key points**
- Never edit an applied migration; fix mistakes with a new one.
- Forward-only: do not rely on "down" scripts; to undo, write a new forward migration.
- Add columns as nullable (or with a default), backfill, then add `not null` in a later step.
- Keep each migration small and focused; one change per file.
- Test on a copy of real data before production; big changes (rename, drop) need care and are covered in MID-020.

**Show**
```sql
-- V2__add_sku.sql
alter table product add column sku text;
update product set sku = 'SKU-' || id where sku is null;
alter table product alter column sku set not null;
create unique index ux_product_sku on product(sku);
```

**Check:** Your V2 has a typo and already ran. What do you do? *(Write V3 to fix it; never edit V2.)*

---

## JNR-033-L04 · Seed data (5 min)
**Goal:** separate reference data from test data.

**Key points**
- Reference (seed) data is needed in every environment: countries, order statuses, default roles.
- Put it in a migration, because it is part of the schema's meaning.
- Test data (fake products, fake customers) never goes in production migrations.
- Load test data in tests, with test-only scripts or a profile.
- Keep seed inserts idempotent-safe or versioned so they run once.

**Show**
```sql
-- V3__seed_order_status.sql
insert into order_status(code) values ('NEW'), ('PAID'), ('SHIPPED');
```

**Check:** Fake demo products: migration or test data? *(Test data.)*

---

## JNR-033-L05 · Liquibase in brief (5 min)
**Goal:** know the main alternative.

**Key points**
- Liquibase is another migration tool used in many companies.
- Changes are written in changelog files (YAML, XML, or SQL) with ids and authors.
- It also keeps a history table and checksums.
- Concepts match Flyway: versioned, ordered, applied once.
- This course uses Flyway; if your team uses Liquibase, the ideas transfer.

**Show:** a short YAML changeset: `id: 2`, `author: ana`, `addColumn: product.sku`.

**Check:** Name one similarity between Flyway and Liquibase. *(Both keep a history table and never reapply a change.)*

---

## JNR-033-L06 · Demo: baselining Shop with Flyway and adding V2 (10 min)
**Goal:** convert Shop's manual schema to Flyway; prepares JNR-033-LAB1.

**Steps**
1. Add Flyway; copy the current `schema.sql` into `V1__baseline.sql`.
2. Set `spring.jpa.hibernate.ddl-auto=validate`.
3. Start on a fresh empty database; show the history table.
4. For the existing database, enable baseline on migrate with baseline version 1 and start; V1 is skipped.
5. **Planned mistake:** edit V1 after it ran; show the checksum error, revert, and add `V2__add_sku.sql` with a backfill instead.
6. Compare both databases: same state.
