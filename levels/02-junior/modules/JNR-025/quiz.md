# JNR-025 · JDBC — Quiz

Outcomes: O1 DataSource and pool · O2 batches and generated keys · O3 type mapping · O4 injection prevention.

**Q01 (O1)** A connection pool mainly: A. Encrypts SQL B. Reuses open connections C. Caches query results D. Generates ids
**Q02 (O1)** Calling `close()` on a pooled connection: A. Returns it to the pool B. Always closes the socket C. Drops the table D. Leaks it
**Q03 (O1)** Best way to release JDBC resources: A. `finalize()` B. Garbage collection only C. try-with-resources D. Never close them
**Q04 (O2)** `executeBatch` is faster mainly because of: A. Compression B. Less parsing in Java C. Smaller tables D. Fewer network round trips
**Q05 (O2)** To read database-generated ids you use: A. `RETURN_GENERATED_KEYS` and `getGeneratedKeys()` B. `getId()` C. `select max(id)` after each insert D. `ResultSet.next()` alone
**Q06 (O3)** Java type for a `numeric(12,2)` price: A. `double` B. `float` C. `BigDecimal` D. `String`
**Q07 (O3)** `rs.getInt("x")` on a NULL column returns: A. An exception always B. 0 C. -1 D. null
**Q08 (O3)** Best Java type for `timestamptz`: A. `Instant` or `OffsetDateTime` B. `int` C. `LocalDate` D. `char`
**Q09 (O4)** A user-chosen `ORDER BY` column should be handled with: A. A `?` placeholder B. Raw concatenation C. Escaping quotes D. An allow-list map
**Q10 (O4)** `PreparedStatement` placeholders protect: A. Column names B. Values C. Table names D. `ASC`/`DESC` keywords

## Answers
Q01 B · Q02 A · Q03 C · Q04 D · Q05 A · Q06 C · Q07 B · Q08 A · Q09 D · Q10 B

## Practical part
Six exercises `JNR-025-EX01` to `EX06` plus the lab; the assessment is fixing an injectable dynamic query (EX05, EX06). Pass: at least five exercises correct, lab speed-up measured, no concatenated user input.
