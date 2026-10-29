# MID-013 · Query optimization — Quiz

Outcomes: O1 reading plans · O2 selectivity and statistics · O3 finding and fixing slow queries · O4 ORM queries.

**Q01 (O1)** `EXPLAIN (ANALYZE)` differs from `EXPLAIN` because it: A. Only estimates B. Executes the query and reports actuals C. Creates indexes D. Clears the cache
**Q02 (O1)** A big gap between `rows=` and `actual rows=` usually indicates: A. A hardware fault B. An unused index C. A missing semicolon D. Poor statistics or estimates
**Q03 (O1)** The join best suited to a few outer rows with an indexed inner lookup: A. Nested loop B. Merge join C. Cross join D. Hash join
**Q04 (O2)** A sequential scan is correct when: A. There is a primary key B. The table has no rows C. The query needs a large share of the table D. Never
**Q05 (O2)** Correlated columns are mis-estimated because the planner assumes: A. They are unique B. They are text C. They are null D. They are independent
**Q06 (O2)** After a bulk load you should run: A. `DROP INDEX` B. `ANALYZE` C. `TRUNCATE` D. `REINDEX` always
**Q07 (O3)** In `pg_stat_statements`, to find the biggest overall cost sort by: A. Total execution time B. Query length C. Query id D. Rows only
**Q08 (O3)** Which is index-friendly? A. `WHERE date_trunc('day', ts) = d` B. `WHERE ts::text LIKE '2026%'` C. `WHERE ts >= d AND ts < d + 1` D. `WHERE lower(ts::text) = x`
**Q09 (O3)** Better than deep `OFFSET` pagination: A. Bigger `LIMIT` B. Keyset pagination C. `SELECT *` D. Sorting in Java
**Q10 (O4)** An ORM N+1 problem appears in logs as: A. One large query B. Only DDL C. No queries D. Many near-identical queries per request

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Plan-reading test: given three plans, name the bottleneck node and the fix; plus exercises `MID-013-EX01` to `EX07` and the lab. Pass: quiz 8/10, test bottlenecks identified correctly, and lab before/after evidence for all five queries.
