# MID-P2 — Advanced PostgreSQL and Data Access

**Phase goal:** the learner writes advanced SQL, reads execution plans, understands how PostgreSQL handles concurrency, operates a database safely, and changes schemas without downtime.

**Running project:** *Shop Platform* gains reporting queries, a 10-million-row order history for realistic plans, and a zero-downtime schema change.

**Phase total:** ~12.8 h video · ~36 h practice

---

### MID-011 · SQL mastery
`n: 119` · **Video:** 72 min · **Practice:** 5 h

**Prerequisites:** BEG-050, JNR-029

**Learning outcomes** — the learner can:
1. Structure complex queries with CTEs and write recursive CTEs for hierarchies.
2. Use window functions (`ROW_NUMBER`, `RANK`, `LAG`, running totals, partitions).
3. Use set operations, lateral joins, and `FILTER` clauses.
4. Write upserts with `INSERT … ON CONFLICT`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-011-L01 | CTEs for readable queries | 10 |
| MID-011-L02 | Recursive CTEs | 10 |
| MID-011-L03 | Window functions | 15 |
| MID-011-L04 | Advanced joins and LATERAL | 10 |
| MID-011-L05 | Set operations and FILTER | 8 |
| MID-011-L06 | Upserts | 7 |
| MID-011-L07 | Demo: building the monthly sales report in SQL | 12 |

**Lab** — `MID-011-LAB1` *Analytics queries:* top 3 products per category per month, customer retention cohorts, category tree with totals. Acceptance: one query each; results verified against a Java implementation.

**Common mistakes:** pulling rows into Java to aggregate; window functions confused with `GROUP BY`.

**Assessment:** timed SQL test.

**Career relevance:** reporting, data platforms (SRB-007).

---

### MID-012 · Index internals
`n: 120` · **Video:** 62 min · **Practice:** 3 h

**Prerequisites:** BEG-042, JNR-034

**Learning outcomes** — the learner can:
1. Explain B-tree index structure and why column order matters in composite indexes.
2. Choose GIN, GiST, BRIN, or hash indexes for given workloads.
3. Design partial and covering indexes and explain index-only scans.
4. Weigh the write and storage cost of indexes.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-012-L01 | How a B-tree index works | 12 |
| MID-012-L02 | Composite indexes and column order | 10 |
| MID-012-L03 | GIN, GiST, BRIN, hash | 12 |
| MID-012-L04 | Partial and covering indexes | 10 |
| MID-012-L05 | The cost of indexes | 6 |
| MID-012-L06 | Demo: one query, five indexes, five plans | 12 |

**Lab** — `MID-012-LAB1` *Index the order history:* design indexes for five frequent Shop queries on 10 M rows. Acceptance: each query's plan uses the intended index; write overhead measured.

**Common mistakes:** one index per column; wrong composite order; indexes never used.

**Assessment:** index design for a new workload.

**Career relevance:** query optimization (MID-013) and database scaling (SRC-007).

---

### MID-013 · Query optimization
`n: 121` · **Video:** 89 min · **Practice:** 4 h

**Prerequisites:** MID-012

**Learning outcomes** — the learner can:
1. Read `EXPLAIN (ANALYZE, BUFFERS)` output: scan types, join algorithms, estimates vs actuals.
2. Explain selectivity, statistics, and why the planner chooses a sequential scan.
3. Find slow queries with `pg_stat_statements` and fix them by rewriting or indexing.
4. Recognize ORM-generated queries in plans and fix them at the source.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-013-L01 | How the planner thinks | 10 |
| MID-013-L02 | Reading EXPLAIN ANALYZE | 15 |
| MID-013-L03 | Join algorithms | 10 |
| MID-013-L04 | Statistics and estimates | 10 |
| MID-013-L05 | Finding slow queries with `pg_stat_statements` | 8 |
| MID-013-L06 | Query rewrites that help | 10 |
| MID-013-L07 | Demo: from 4 seconds to 40 ms | 14 |
| MID-013-L08 | Demo: a bad estimate and how statistics fix it | 12 |

**Lab** — `MID-013-LAB1` *Slow query clinic:* fix the five slowest statements in a loaded Shop database. Acceptance: before/after plans and timings for each.

**Common mistakes:** `EXPLAIN` without `ANALYZE`; functions on indexed columns; `OFFSET` pagination over deep pages.

**Assessment:** plan-reading test.

**Career relevance:** the MID graduation gate's performance bottleneck.

---

### MID-014 · MVCC
`n: 122` · **Video:** 54 min · **Practice:** 2 h

**Prerequisites:** JNR-031

**Learning outcomes** — the learner can:
1. Explain MVCC: row versions, snapshots, and visibility.
2. Explain why `UPDATE` creates new row versions and what vacuum does.
3. Detect table and index bloat and long-running transactions that prevent cleanup.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-014-L01 | Readers don't block writers | 10 |
| MID-014-L02 | Row versions and snapshots | 12 |
| MID-014-L03 | Vacuum and autovacuum | 10 |
| MID-014-L04 | Bloat and long transactions | 10 |
| MID-014-L05 | Demo: an idle transaction blocking vacuum | 12 |

**Lab** — `MID-014-LAB1` *Observe MVCC:* use `xmin`/`xmax` and two sessions to watch visibility; create bloat with an idle-in-transaction session and fix it. Acceptance: annotated session transcript.

**Common mistakes:** disabling autovacuum; leaving transactions open in application code.

**Assessment:** quiz.

**Career relevance:** isolation (MID-015) and database operations (MID-018).

---

### MID-015 · Isolation and locking
`n: 123` · **Video:** 76 min · **Practice:** 3 h

**Prerequisites:** MID-014

**Learning outcomes** — the learner can:
1. Describe the anomalies (dirty read, non-repeatable read, phantom, lost update, write skew) and which isolation levels prevent them in PostgreSQL.
2. Use row locks (`FOR UPDATE`, `FOR SHARE`, `SKIP LOCKED`) correctly.
3. Diagnose lock waits and deadlocks from `pg_locks` and logs.
4. Handle serialization failures with retries.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-015-L01 | Concurrency anomalies | 12 |
| MID-015-L02 | Isolation levels in PostgreSQL | 12 |
| MID-015-L03 | Row-level locks | 10 |
| MID-015-L04 | `SKIP LOCKED` job queues | 8 |
| MID-015-L05 | Deadlocks | 10 |
| MID-015-L06 | Demo: lost update in two terminals | 12 |
| MID-015-L07 | Demo: write skew under serializable | 12 |

**Lab** — `MID-015-LAB1` *Last item in stock:* reproduce overselling under concurrency, then fix it three ways (atomic update, `FOR UPDATE`, serializable + retry) and compare throughput. Acceptance: concurrent test never oversells.

**Common mistakes:** assuming `READ COMMITTED` prevents lost updates; retrying without limits.

**Assessment:** anomaly-identification scenarios.

**Career relevance:** data integrity (SRC-014).

---

### MID-016 · Advanced transactions
`n: 124` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-031, MID-015

**Learning outcomes** — the learner can:
1. Implement optimistic locking with `@Version` and handle conflicts as 409 responses.
2. Choose optimistic vs pessimistic locking for a workload.
3. Use Spring transaction propagation (`REQUIRES_NEW`, `NESTED`) correctly and recognize its traps.
4. Implement safe retries for transient failures (serialization, deadlock) with idempotent units of work.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-016-L01 | Optimistic locking | 12 |
| MID-016-L02 | Pessimistic locking from JPA | 8 |
| MID-016-L03 | Choosing a locking strategy | 8 |
| MID-016-L04 | Propagation in depth | 12 |
| MID-016-L05 | Retrying transactions safely | 10 |
| MID-016-L06 | Demo: concurrent edits with `@Version` | 12 |
| MID-016-L07 | Demo: the `REQUIRES_NEW` audit-log trap | 12 |

**Lab** — `MID-016-LAB1` *Concurrent product edits:* two admins editing the same product get a 409 with the current version; a deadlock-prone job retries safely. Acceptance: tests for both conflicts.

**Common mistakes:** retrying non-idempotent work; `REQUIRES_NEW` exhausting the connection pool.

**Assessment:** fix a transaction design.

**Career relevance:** distributed consistency (MID-030).

---

### MID-017 · Connection pooling
`n: 125` · **Video:** 50 min · **Practice:** 2.5 h

**Prerequisites:** JNR-026, MID-003

**Learning outcomes** — the learner can:
1. Explain why pools exist and how HikariCP manages connections.
2. Size a pool from database capacity and request concurrency, not by guesswork.
3. Configure timeouts and diagnose pool exhaustion from metrics and thread dumps.
4. Explain why "more connections" often makes things slower.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-017-L01 | The cost of a database connection | 8 |
| MID-017-L02 | HikariCP internals | 10 |
| MID-017-L03 | Sizing a pool | 12 |
| MID-017-L04 | Timeouts and leak detection | 8 |
| MID-017-L05 | Demo: pool exhaustion under load | 12 |

**Lab** — `MID-017-LAB1` *Pool tuning:* load-test Shop with pool sizes 5, 10, 50, and 200 and explain the results. Acceptance: chart plus recommendation.

**Common mistakes:** pools bigger than the database can serve; long transactions holding connections.

**Assessment:** sizing scenarios.

**Career relevance:** advanced troubleshooting (SRC-015).

---

### MID-018 · Database operations
`n: 126` · **Video:** 62 min · **Practice:** 3 h

**Prerequisites:** BEG-051, JNR-048

**Learning outcomes** — the learner can:
1. Take logical (`pg_dump`) and physical backups and restore them.
2. Explain point-in-time recovery with WAL archiving.
3. Explain streaming replication and read replicas, including replication lag.
4. Monitor key database health indicators (connections, locks, cache hit ratio, replication lag, disk).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-018-L01 | Backups: logical vs physical | 10 |
| MID-018-L02 | Restore drills | 8 |
| MID-018-L03 | WAL and point-in-time recovery | 12 |
| MID-018-L04 | Replication and read replicas | 12 |
| MID-018-L05 | What to monitor | 8 |
| MID-018-L06 | Demo: restoring to five minutes before a bad `DELETE` | 12 |

**Lab** — `MID-018-LAB1` *Restore drill:* back up Shop's database, simulate data loss, restore with PITR, and record the time taken. Acceptance: runbook plus measured recovery time.

**Common mistakes:** backups never restored; reading your own writes from a lagging replica.

**Assessment:** runbook review.

**Career relevance:** disaster recovery (SRC-013).

---

### MID-019 · Data modeling at scale
`n: 127` · **Video:** 58 min · **Practice:** 2.5 h

**Prerequisites:** MID-013

**Learning outcomes** — the learner can:
1. Decide when to denormalize for read performance and how to keep copies consistent.
2. Partition a large table by range or list and explain partition pruning.
3. Use `jsonb` columns appropriately and index them.
4. Plan data retention and archiving.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-019-L01 | Normalization trade-offs | 10 |
| MID-019-L02 | Denormalization patterns | 10 |
| MID-019-L03 | Table partitioning | 12 |
| MID-019-L04 | `jsonb`: when and how | 8 |
| MID-019-L05 | Retention and archiving | 6 |
| MID-019-L06 | Demo: partitioning the order history by month | 12 |

**Lab** — `MID-019-LAB1` *Partitioned orders:* partition the 10 M-row order table by month; compare query and maintenance costs. Acceptance: pruning visible in plans; old partitions detachable.

**Common mistakes:** partitioning small tables; `jsonb` as a schema-avoidance strategy.

**Assessment:** modeling scenario.

**Career relevance:** sharding and hot partitions (SRC-007).

---

### MID-020 · Database migrations
`n: 128` · **Video:** 60 min · **Practice:** 2.5 h

**Prerequisites:** JNR-033, MID-015

**Learning outcomes** — the learner can:
1. Apply expand-contract to rename or restructure columns without downtime.
2. Identify migrations that take heavy locks and use safe alternatives (`CREATE INDEX CONCURRENTLY`, lock timeouts).
3. Backfill large tables in batches.
4. Plan rollback for each migration step.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-020-L01 | Why migrations cause outages | 8 |
| MID-020-L02 | Expand and contract | 12 |
| MID-020-L03 | Lock-safe DDL | 10 |
| MID-020-L04 | Batched backfills | 8 |
| MID-020-L05 | Rollback strategies | 8 |
| MID-020-L06 | Demo: renaming a column under live traffic | 14 |

**Lab** — `MID-020-LAB1` *Zero-downtime rename:* rename `customer.name` to `full_name` across releases while a load test runs. Acceptance: zero failed requests during the migration.

**Common mistakes:** rename in one step; adding a `NOT NULL` column with a volatile default on a huge table.

**Assessment:** migration plan review.

**Career relevance:** large migrations (SRB-017).

---

### MID-021 · Advanced Hibernate
`n: 129` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** JNR-032, MID-016

**Learning outcomes** — the learner can:
1. Design fetch plans per use case with entity graphs and DTO projections.
2. Configure JDBC batching and explain why identity generation disables insert batching.
3. Use the second-level cache and query cache appropriately, or decide against them.
4. Handle detached entities and merging correctly.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-021-L01 | Fetch plans per use case | 10 |
| MID-021-L02 | Batching inserts and updates | 10 |
| MID-021-L03 | Second-level and query caches | 12 |
| MID-021-L04 | Entity states revisited: merge vs persist | 8 |
| MID-021-L05 | Hibernate statistics | 6 |
| MID-021-L06 | Demo: 10× faster bulk updates with batching | 12 |

**Lab** — `MID-021-LAB1` *Batch job tuning:* make the nightly price-update job 10× faster without leaving JPA. Acceptance: statement counts and timings before/after.

**Common mistakes:** caching mutable, frequently written entities; `saveAll` without batching configured.

**Assessment:** tuning exercise.

**Career relevance:** choosing persistence tools (MID-022).

---

### MID-022 · Alternative persistence
`n: 130` · **Video:** 52 min · **Practice:** 2.5 h

**Prerequisites:** JNR-026, MID-011

**Learning outcomes** — the learner can:
1. Write type-safe SQL with jOOQ, generated from the schema.
2. Compare JDBC, jOOQ, and JPA for a given use case and justify a choice.
3. Build a separate read model for queries (CQRS-lite) inside one service.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| MID-022-L01 | When JPA is the wrong tool | 8 |
| MID-022-L02 | jOOQ in practice | 14 |
| MID-022-L03 | Choosing a persistence approach | 8 |
| MID-022-L04 | Read models and CQRS-lite | 10 |
| MID-022-L05 | Demo: rewriting the sales report with jOOQ | 12 |

**Lab** — `MID-022-LAB1` *Dashboard read model:* an admin dashboard served from a read model table populated on order events, queried with jOOQ. Acceptance: written decision record comparing the three approaches.

**Common mistakes:** mixing approaches without boundaries; full CQRS with event sourcing for simple reads.

**Assessment:** decision-record review.

**Career relevance:** CQRS and materialized views (SRB-001).
