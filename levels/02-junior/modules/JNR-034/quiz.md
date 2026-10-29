# JNR-034 · Database constraints — Quiz

Outcomes: O1 constraints · O2 violations to API errors · O3 concurrency and application checks · O4 indexes and `EXPLAIN`.

**Q01 (O1)** Which constraint prevents two rows with the same SKU? A. `check` B. `not null` C. `unique` D. `default`
**Q02 (O1)** A `check (price >= 0)` constraint stops: A. Duplicate prices B. Negative prices C. Null prices D. Slow queries
**Q03 (O1)** A foreign key guarantees: A. The referenced row exists B. A fast join C. Unique values D. A sorted table
**Q04 (O2)** A duplicate SKU should become HTTP: A. 200 B. 404 C. 500 D. 409
**Q05 (O2)** Spring translates a unique violation into: A. `DataIntegrityViolationException` (or a subclass) B. `IOException` C. `ClassCastException` D. `TimeoutException`
**Q06 (O2)** Responses should: A. Include the raw SQL B. Contain the stack trace C. Carry a clear message without SQL details D. Be empty
**Q07 (O3)** "Check then insert" without a constraint fails because: A. Two requests can both pass the check B. SQL is slow C. Java is single-threaded D. Indexes are missing
**Q08 (O3)** The best protection against duplicates is: A. A `synchronized` method only B. A unique constraint C. A bigger pool D. A comment
**Q09 (O4)** In `EXPLAIN`, a `Seq Scan` means: A. The index is used B. The query failed C. The whole table is read D. The table is empty
**Q10 (O4)** PostgreSQL automatically indexes: A. Foreign keys B. Every column C. Nothing D. Primary keys and unique constraints

## Answers
Q01 C · Q02 B · Q03 A · Q04 D · Q05 A · Q06 C · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Six exercises `JNR-034-EX01` to `EX06` plus the lab; the assessment is adding constraints and indexes to a schema from requirements (EX01, EX05). Pass: constraints and indexes correct, at least five of six exercises correct, and the concurrent test producing one success and one 409 every run.
