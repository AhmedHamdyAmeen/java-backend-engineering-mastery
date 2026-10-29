# JNR-026 · Spring JDBC — Quiz

Outcomes: O1 DataSource configuration · O2 JdbcClient/JdbcTemplate · O3 row mapping · O4 exception translation.

**Q01 (O1)** Boot's default connection pool is: A. DBCP B. C3P0 C. Tomcat JDBC only D. HikariCP
**Q02 (O1)** Where should the database password come from? A. Hard-coded in the repository B. An environment variable or secret store C. The README D. A public Git file
**Q03 (O2)** Named parameters look like: A. `:id` B. `#1` C. `$id` D. `%id`
**Q04 (O2)** `JdbcClient.update()` returns: A. The generated key B. A `ResultSet` C. The affected row count D. `void`
**Q05 (O2)** Spring's JDBC helpers take care of: A. Business rules B. Opening, closing, and releasing resources C. Schema design D. Index creation
**Q06 (O3)** A `RowMapper` maps: A. One row to one object B. A whole table to a list by hand C. SQL to Java code D. An object to a row
**Q07 (O3)** Where should `ResultSet` handling live? A. Controllers B. Services C. In the repository only D. DTOs
**Q08 (O4)** A unique-key violation becomes: A. `SQLException` thrown to the controller B. `NullPointerException` C. `IllegalStateException` D. `DuplicateKeyException`
**Q09 (O4)** `DataAccessException` is: A. A checked exception B. An unchecked exception hierarchy C. A JDBC class D. An error code
**Q10 (O4)** Best practice for handling it: A. Catch it in every method B. Ignore it always C. Catch specific subclasses where you can act D. Convert all to `RuntimeException("error")`

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 B · Q06 A · Q07 C · Q08 D · Q09 B · Q10 C

## Practical part
Six exercises `JNR-026-EX01` to `EX06` plus the lab; the assessment is implementing a reporting query repository method (EX05). Pass: at least five exercises correct and the lab integration test green.
