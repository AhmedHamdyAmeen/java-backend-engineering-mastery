# JNR-033 · Schema migrations — Quiz

Outcomes: O1 Flyway on startup · O2 forward-only migrations · O3 seed vs test data · O4 schema validation.

**Q01 (O1)** Flyway records applied migrations in: A. A text file B. The `flyway_schema_history` table C. Git D. Memory only
**Q02 (O1)** A correct migration file name is: A. `V2_add_sku.sql` B. `add_sku.sql` C. `migration2.sql` D. `V2__add_sku.sql`
**Q03 (O1)** Migrations run: A. Once, in version order B. Every startup C. Randomly D. Only manually
**Q04 (O2)** An already applied migration has an error. You should: A. Edit it B. Delete it C. Add a new migration that fixes it D. Disable Flyway
**Q05 (O2)** Editing an applied migration causes: A. Nothing B. A checksum mismatch at startup C. An automatic rollback D. A new version number
**Q06 (O2)** Safe way to add a required column to a populated table: A. Add `not null` without default B. Drop the table C. Use `ddl-auto=update` D. Add nullable, backfill, then set `not null`
**Q07 (O3)** Order status codes needed everywhere are: A. Test data B. Reference (seed) data C. Temporary D. Logs
**Q08 (O3)** Fake demo customers belong in: A. Production migrations B. `V1` C. Test-only data D. `application.yml`
**Q09 (O4)** `ddl-auto=validate` does: A. Creates missing tables B. Drops unused columns C. Updates the schema D. Checks entities against the existing schema
**Q10 (O4)** `ddl-auto=update` in production is: A. Recommended B. Required C. A mistake D. Equivalent to Flyway

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 B · Q06 D · Q07 B · Q08 C · Q09 D · Q10 C

## Practical part
Six exercises `JNR-033-EX01` to `EX06` plus the lab; the assessment is writing a migration for a new requirement (EX06). Pass: EX06 correct and safe, at least five of six exercises correct, and fresh and existing databases reaching the same state.
