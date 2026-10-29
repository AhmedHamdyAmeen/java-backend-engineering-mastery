# MID-011 · SQL mastery — Quiz

Outcomes: O1 CTEs and recursion · O2 window functions · O3 joins, set operations, FILTER · O4 upserts.

**Q01 (O1)** A recursive CTE consists of: A. Two anchors B. A view only C. A trigger D. An anchor and a recursive part joined by `UNION ALL`
**Q02 (O1)** To avoid infinite recursion on cyclic data you can: A. Use `DISTINCT` only B. Track a depth or path and stop C. Add an index D. Use `LIMIT 0`
**Q03 (O1)** In current PostgreSQL, a non-recursive CTE referenced once is usually: A. Always materialized B. Stored on disk permanently C. Inlined into the query D. Rejected
**Q04 (O2)** Unlike `GROUP BY`, a window function: A. Keeps every row B. Removes rows C. Cannot use `ORDER BY` D. Needs a temp table
**Q05 (O2)** `RANK` on values 10, 10, 8 gives: A. 1,2,3 B. 1,1,3 C. 1,1,2 D. 1,2,2
**Q06 (O2)** To filter on `row_number() = 1` you must: A. Use `WHERE` directly B. Use `HAVING` C. Use `GROUP BY` D. Wrap it in a CTE or subquery
**Q07 (O3)** `LATERAL` lets a subquery: A. Run in parallel B. Skip the planner C. Reference columns from earlier `FROM` items D. Write data
**Q08 (O3)** Faster set operation when duplicates do not matter: A. `UNION ALL` B. `INTERSECT` C. `UNION` D. `EXCEPT`
**Q09 (O3)** `count(*) FILTER (WHERE x)` is mainly a cleaner form of: A. `JOIN` B. `DISTINCT ON` C. `LIMIT` D. `CASE` inside an aggregate
**Q10 (O4)** In `ON CONFLICT DO UPDATE`, `EXCLUDED` refers to: A. The existing row B. The row proposed for insertion C. A deleted row D. The table name

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 B · Q06 D · Q07 C · Q08 A · Q09 D · Q10 B

## Practical part
Timed SQL test (three queries from the lab's families) plus exercises `MID-011-EX01` to `EX07` and the lab. Pass: quiz 8/10, the timed test answered correctly, and lab results matching the Java check.
