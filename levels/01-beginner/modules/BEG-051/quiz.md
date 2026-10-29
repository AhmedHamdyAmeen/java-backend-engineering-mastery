# BEG-051 · PostgreSQL basics — Quiz

Outcomes: O1 install and connect · O2 database, schema, user · O3 constraints · O4 transactions.

**Q01 (O1)** The command-line client for PostgreSQL is: A. `pgAdmin` B. `DBeaver` C. `pgcli.exe` D. `psql`
**Q02 (O1)** The default PostgreSQL port is: A. 8080 B. 5432 C. 3306 D. 1521
**Q03 (O1)** In `psql`, `\dt` lists: A. Databases B. Users C. Tables D. Constraints
**Q04 (O2)** An application should connect as: A. `postgres` B. Any admin C. A dedicated user with limited rights D. No user
**Q05 (O2)** The default schema name is: A. `main` B. `public` C. `default` D. `root`
**Q06 (O3)** To forbid duplicate ISBNs: A. `NOT NULL` B. `CHECK` C. `FOREIGN KEY` D. `UNIQUE`
**Q07 (O3)** To forbid negative copies: A. `CHECK (copies >= 0)` B. `UNIQUE` C. `PRIMARY KEY` D. `NOT NULL` only
**Q08 (O3)** An insert with a non-existent member id is rejected by: A. A `CHECK` B. A foreign key C. `ORDER BY` D. `LIMIT`
**Q09 (O4)** `ROLLBACK` will: A. Save all changes B. Delete the table C. Undo changes since `BEGIN` D. Close the server
**Q10 (O4)** Constraints in the database matter because: A. Application code can have bugs B. Java is slow C. SQL cannot insert D. They replace tables

## Answers
Q01 D · Q02 B · Q03 C · Q04 C · Q05 B · Q06 D · Q07 A · Q08 B · Q09 C · Q10 A

## Practical part
Practical check of the re-runnable schema script with constraints, recorded errors, and a demonstrated rollback (lab and EX01–EX07). Pass: script runs from scratch, at least 8 of 10 quiz questions.
