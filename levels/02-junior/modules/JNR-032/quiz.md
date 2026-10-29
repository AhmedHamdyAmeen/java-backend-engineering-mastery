# JNR-032 · ORM pitfalls — Quiz

Outcomes: O1 detect N+1 · O2 fix N+1 · O3 lazy loading and its exception · O4 pagination with collections and OSIV.

**Q01 (O1)** 100 orders loaded with N+1 on lines cause: A. 100 queries B. 2 queries C. 1 query D. 101 queries
**Q02 (O1)** A good way to catch N+1 in tests: A. Query counter assertion B. Manual clicking C. Larger heap D. Faster disk
**Q03 (O2)** Which fixes N+1? A. `join fetch` B. `EAGER` everywhere C. More RAM D. A bigger pool
**Q04 (O2)** `@EntityGraph` on a repository method: A. Draws a diagram B. Defines which relations load with the entity C. Creates tables D. Disables lazy loading globally
**Q05 (O3)** `LazyInitializationException` occurs when: A. The query is invalid B. The pool is full C. The database is down D. A lazy relation is accessed after the session closed
**Q06 (O3)** The default fetch of `@OneToMany` is: A. `LAZY` B. `EAGER` C. `NONE` D. `JOIN`
**Q07 (O3)** The wrong "fix" for a lazy exception is: A. DTO built in the service B. Entity graph C. Making relations `EAGER` globally D. Fetch join
**Q08 (O4)** Fetch-joining a collection with paging makes Hibernate: A. Page in SQL B. Page in memory after loading all rows C. Ignore the page D. Throw always
**Q09 (O4)** Safe paging with collections: A. Page parents' ids first, then load children B. Join fetch plus `LIMIT` C. Load all, then cut D. Turn off paging
**Q10 (O4)** Open Session in View should be: A. Left on B. Turned off and loading done in services C. Used in repositories D. Needed for transactions

## Answers
Q01 D · Q02 A · Q03 A · Q04 B · Q05 D · Q06 A · Q07 C · Q08 B · Q09 A · Q10 B

## Practical part
Six exercises `JNR-032-EX01` to `EX06` plus the lab; the assessment is diagnosing a slow endpoint from logs (EX06). Pass: correct cause, evidence, and fix in EX06, at least five of six exercises correct, lab test failing before and passing after.
