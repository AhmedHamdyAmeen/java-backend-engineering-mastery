# BEG-050 · SQL foundations — Quiz

Outcomes: O1 DDL · O2 DML · O3 queries and aggregates · O4 joins · O5 subqueries.

**Q01 (O1)** Which is DDL? A. `SELECT` B. `INSERT` C. `UPDATE` D. `CREATE TABLE`
**Q02 (O1)** To add a column to an existing table: A. `ALTER TABLE` B. `INSERT` C. `GROUP BY` D. `JOIN`
**Q03 (O2)** `DELETE FROM books;` does what? A. Deletes the table structure B. Deletes nothing C. Deletes all rows D. Errors always
**Q04 (O2)** To change one row you need: A. `UPDATE` without `WHERE` B. `UPDATE` with `WHERE` C. `DROP` D. `CREATE`
**Q05 (O3)** Sort newest first: A. `ORDER BY year ASC` B. `GROUP BY year` C. `WHERE year DESC` D. `ORDER BY year DESC`
**Q06 (O3)** Find rows with an empty return date: A. `= NULL` B. `IS NULL` C. `= ''` D. `== NULL`
**Q07 (O3)** Filtering on `COUNT(*) > 3` belongs in: A. `HAVING` B. `WHERE` C. `ORDER BY` D. `FROM`
**Q08 (O4)** Which keeps all members, even with no loans? A. `INNER JOIN` B. `UNION` C. `LEFT JOIN` from members D. `DROP JOIN`
**Q09 (O4)** An inner join can silently: A. Add rows B. Drop unmatched rows C. Delete tables D. Rename columns
**Q10 (O5)** `WHERE id IN (SELECT ...)` uses a: A. Subquery B. Join C. Alias D. Constraint

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 A

## Practical part
Timed SQL test plus the 25-query lab (EX01–EX08). Pass: 20 of 25 lab queries correct and at least 8 of 10 quiz questions.
