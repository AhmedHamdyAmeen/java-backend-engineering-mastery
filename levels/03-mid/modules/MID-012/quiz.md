# MID-012 · Index internals — Quiz

Outcomes: O1 B-tree and column order · O2 index types · O3 partial and covering · O4 cost.

**Q01 (O1)** A B-tree lookup on millions of rows reads: A. A few pages along one path B. Every page C. Only the last page D. No pages
**Q02 (O1)** Index `(a, b)` best serves: A. `WHERE b = 1` B. `WHERE b < 1` only C. `WHERE a = 1 AND b = 2` D. No query
**Q03 (O1)** For `WHERE a = ? AND b > ?` the best order is: A. `(b, a)` B. Order never matters C. Two separate indexes always D. `(a, b)`
**Q04 (O2)** Best index for `jsonb` containment `@>`: A. BRIN B. GIN C. Hash D. B-tree on the column
**Q05 (O2)** BRIN fits best: A. Randomly ordered small tables B. Full-text search C. Huge append-only tables ordered by date D. Unique keys
**Q06 (O2)** Hash indexes support: A. Equality only B. Range queries C. Sorting D. Prefix search
**Q07 (O3)** A partial index is used when: A. Never with `SELECT` B. Always C. Only for `UPDATE` D. The query condition implies the index `WHERE`
**Q08 (O3)** `INCLUDE` columns in an index help: A. Sorting by them B. Index-only scans C. Uniqueness D. Partitioning
**Q09 (O4)** An index with `idx_scan = 0` over months is: A. A candidate to drop B. Free C. Required D. Faster than others
**Q10 (O4)** Adding indexes mostly makes writes: A. Faster B. Unchanged C. Slower D. Impossible

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 C · Q06 A · Q07 D · Q08 B · Q09 A · Q10 C

## Practical part
Design indexes for a new workload given as five queries and a write rate; justify order and type. Pass: quiz 8/10 and a design where each query is served and no index is redundant, plus the lab measurements.
