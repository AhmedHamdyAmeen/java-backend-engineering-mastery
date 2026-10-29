# MID-019 · Data modeling at scale — Quiz

Outcomes: O1 normalization and denormalization · O2 partitioning · O3 `jsonb` · O4 retention.

**Q01 (O1)** Denormalization is justified by: A. Habit B. Shorter SQL C. Fewer tables D. A measured read problem
**Q02 (O1)** `REFRESH MATERIALIZED VIEW CONCURRENTLY` requires: A. Superuser B. A unique index on the view C. No readers D. A partition
**Q03 (O1)** `price_at_purchase` stored in an order item is: A. Harmful duplication B. A bug C. A snapshot of a different fact D. Required by SQL
**Q04 (O2)** Partition pruning happens when the query: A. Filters on the partition key B. Uses `SELECT *` C. Has an `ORDER BY` D. Joins three tables
**Q05 (O2)** In a range-partitioned table, the primary key must: A. Be a UUID B. Include the partition key C. Be absent D. Be text
**Q06 (O2)** A good reason to partition by month: A. The table has 100 rows B. To avoid backups C. To avoid indexes D. Old data can be dropped or detached quickly
**Q07 (O3)** The index type usually used for `jsonb` containment: A. BRIN B. Hash C. GIN D. GiST only
**Q08 (O3)** `jsonb` is a poor choice for: A. Foreign keys and join columns B. Sparse optional attributes C. Stored external payloads D. Per-category specs
**Q09 (O4)** Best way to remove a year of old orders from a partitioned table: A. `DELETE` in one statement B. Reindex C. `VACUUM FULL` D. Detach and drop the partitions
**Q10 (O4)** Archived data should be: A. Never tested B. Restore-tested periodically C. Kept only in memory D. Stored in `jsonb`

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 B · Q06 D · Q07 C · Q08 A · Q09 D · Q10 B

## Practical part
Modeling scenario: given a growing orders-and-events schema, decide what to denormalize, what to partition (and by what key), what goes in `jsonb`, and the retention plan. Pass: quiz 8/10, a scenario answer that justifies each decision, and the lab showing pruning.
