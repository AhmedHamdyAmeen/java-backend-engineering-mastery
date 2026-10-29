# MID-021 · Advanced Hibernate — Quiz

Outcomes: O1 fetch plans · O2 JDBC batching · O3 caches · O4 entity states and merge.

**Q01 (O1)** The default recommended fetch type for associations: A. `EAGER` B. `LAZY` C. `SELECT *` D. `NONE`
**Q02 (O1)** An entity graph or `JOIN FETCH` mainly prevents: A. Deadlocks B. Slow commits C. Dirty reads D. N+1 queries
**Q03 (O1)** For a read-only list screen the cheapest option is usually: A. A DTO projection B. Full entities C. `findAll()` and filter in Java D. Eager fetch everywhere
**Q04 (O2)** Which id strategy disables JDBC insert batching? A. `SEQUENCE` B. UUID assigned in code C. `IDENTITY` D. Assigned ids
**Q05 (O2)** Why flush and clear in a bulk job? A. To commit B. To disable batching C. To lock rows D. To keep persistence-context memory bounded
**Q06 (O2)** `hibernate.jdbc.batch_size` controls: A. Page size B. Statements grouped per round trip C. Pool size D. Cache size
**Q07 (O3)** A good second-level cache candidate: A. Read-mostly category list B. Frequently updated stock C. Order totals D. Session tokens
**Q08 (O3)** The query cache is invalidated when: A. Never B. The JVM restarts only C. Any table in the query is written D. A user logs in
**Q09 (O4)** `merge` returns: A. The same detached object B. A managed copy C. `void` D. A new transaction
**Q10 (O4)** Preferred approach to updating an entity from a DTO: A. Build a detached entity and merge B. Delete and insert C. Native update always D. Load inside the transaction and change fields

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Tuning exercise: given a slow job with N+1 loads, `IDENTITY` ids, and no batching, produce a tuned version with statement counts. Pass: quiz 8/10, three tuning changes made with measured effect, and the lab's before/after figures.
