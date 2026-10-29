# MID-022 · Alternative persistence — Quiz

Outcomes: O1 jOOQ · O2 comparing approaches · O3 read models.

**Q01 (O1)** jOOQ generates classes from: A. Annotations B. Spring beans C. The database schema D. HTML
**Q02 (O1)** A main benefit of jOOQ over SQL strings: A. Compile-time checking of columns and types B. Faster disks C. Automatic caching D. No SQL knowledge needed
**Q03 (O1)** jOOQ queries run in the same Spring transaction when they: A. Use a different pool B. Use the same `DataSource` and transaction manager C. Run in a new thread D. Use `REQUIRES_NEW` always
**Q04 (O2)** Best fit for JPA: A. Window functions B. Ten-join analytics C. Bulk set updates D. Transactional CRUD on aggregates
**Q05 (O2)** Best fit for jOOQ: A. Complex type-safe reporting SQL B. Simple entity CRUD only C. Schema design D. Caching
**Q06 (O2)** JDBC (`JdbcClient`) trades convenience for: A. Compile-time checks B. Automatic joins C. Control and minimal dependencies D. Lazy loading
**Q07 (O2)** Mixing persistence approaches in a service is acceptable when: A. Randomly chosen B. Each use case has a clear boundary and shared transactions C. Never D. Only in tests
**Q08 (O3)** CQRS-lite means: A. Event sourcing plus separate databases B. Two microservices C. No writes D. A read model separate from the write model, in one service
**Q09 (O3)** A read model updated in the same transaction as the order is: A. Eventually consistent B. Stale by hours C. Immediately consistent D. Unrecoverable
**Q10 (O3)** A needed safety feature for a read model: A. A rebuild path from write tables B. A larger heap C. A second JVM D. No indexes

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 A · Q06 C · Q07 B · Q08 D · Q09 C · Q10 A

## Practical part
Decision-record review: assess a written record comparing JDBC, jOOQ, and JPA for the dashboard (criteria, trade-offs, decision, consequences). Pass: quiz 8/10, a decision record covering all three options with a justified choice, and the lab dashboard running from its read model.
