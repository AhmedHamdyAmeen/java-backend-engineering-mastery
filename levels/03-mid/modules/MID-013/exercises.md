# MID-013 · Query optimization — Exercises and lab

## Lab
### MID-013-LAB1 · Slow query clinic
**Outcomes:** 1–4 · **Time:** ~3 h
On a loaded Shop database (10 M orders), identify the five slowest statements with `pg_stat_statements`, including one ORM-generated query (N+1 or `SELECT *` from a repository). Fix each by rewriting, indexing, or changing the application code.
**Acceptance:** before/after `EXPLAIN (ANALYZE, BUFFERS)` plans and timings recorded for each of the five.

## Exercises (assessment: plan-reading test)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-013-EX01 | 1 | Annotate a given plan: scan types, join algorithm, the node with the largest time, estimate vs actual gaps. |
| MID-013-EX02 | 1 | Explain what `loops=1000` and `Buffers: shared read=50000` tell you. |
| MID-013-EX03 | 2 | Explain why `WHERE active = true` (95% true) uses a sequential scan, and what would change for `active = false`. |
| MID-013-EX04 | 2 | Fix a bad estimate on correlated columns using `CREATE STATISTICS`. |
| MID-013-EX05 | 3 | Reset `pg_stat_statements`, run a mixed workload, and list the top three queries by total time. |
| MID-013-EX06 | 3 | Rewrite `WHERE date_trunc('day', created_at) = ...` and a deep `OFFSET` query into index-friendly forms. |
| MID-013-EX07 | 4 | Show the SQL a Spring Data repository method generates (SQL logging) and fix an N+1 with a join fetch or projection. |

## Solutions
- **EX01** Name the nodes bottom-up; the slowest node is the one whose actual time minus children is largest; flag nodes where estimated rows differ from actual by 10x or more.
- **EX02** The node ran 1000 times (multiply per-loop time by 1000); about 50 000 pages (about 400 MB at 8 kB) were read from outside shared buffers.
- **EX03** An index would not narrow 95% of the rows, so the sequential scan is cheaper; for `false` (5%) an index or partial index can win.
- **EX04** `CREATE STATISTICS s (dependencies) ON a, b FROM t; ANALYZE t;` then re-check estimates.
- **EX05** `SELECT pg_stat_statements_reset();` then query the view ordered by `total_exec_time`.
- **EX06** Half-open range on the raw column; keyset pagination `WHERE (created_at, id) < (?, ?)`.
- **EX07** `spring.jpa.show-sql` or SQL logger; replace lazy loop with `JOIN FETCH`, entity graph, or a DTO projection.
- The "`EXPLAIN` without `ANALYZE`" mistake is exercised in EX01 and EX02.
