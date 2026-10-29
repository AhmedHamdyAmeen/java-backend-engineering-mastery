# BEG-055 · JDBC essentials — Quiz

Outcomes: O1 driver and connection · O2 queries and mapping · O3 try-with-resources · O4 SQL injection · O5 transactions.

**Q01 (O1)** The JDBC driver: A. Compiles Java B. Is a database C. Translates JDBC calls for one database D. Stores passwords
**Q02 (O1)** Where should DB passwords come from? A. A constant in code B. A committed file C. A comment D. Environment variables
**Q03 (O1)** A PostgreSQL JDBC URL starts with: A. `jdbc:postgresql://` B. `http://` C. `psql://` D. `db:pg:`
**Q04 (O2)** `PreparedStatement` parameters are numbered from: A. 0 B. 1 C. -1 D. They have no numbers
**Q05 (O2)** Which method runs a `SELECT`? A. `executeUpdate()` B. `commit()` C. `executeQuery()` D. `close()`
**Q06 (O2)** `findById` should return: A. `null` B. `Optional<Book>` C. `void` D. A `String`
**Q07 (O3)** Try-with-resources: A. Closes resources automatically B. Opens more connections C. Skips errors D. Makes SQL faster
**Q08 (O4)** Concatenating user input into SQL is dangerous because: A. It is slower B. It uses more memory C. Input can change the query's meaning D. It needs a driver
**Q09 (O4)** Injection is prevented by: A. Longer passwords B. Parameters with `?` C. Removing spaces D. Uppercase SQL
**Q10 (O5)** To group statements into a transaction: A. `setAutoCommit(false)` B. `setAutoCommit(true)` C. `close()` D. `executeQuery()`

## Answers
Q01 C · Q02 D · Q03 A · Q04 B · Q05 C · Q06 B · Q07 A · Q08 C · Q09 B · Q10 A

## Practical part
Implement a new repository method with an integration test and explain why parameters prevent injection (EX08 and the lab). Pass: at least 8 of 10 quiz questions, no concatenated SQL, resources closed, tests pass.
