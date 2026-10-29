# SRB-001 · Distributed architecture patterns — Quiz

Outcomes: O1 CQRS · O2 event sourcing · O3 materialized views · O4 orchestration choice.

**Q01 (O1)** What defines CQRS-lite? A. Separate read and write code over the same database B. Two databases always C. Using Kafka for every query D. Event sourcing for every aggregate
**Q02 (O1)** Which is the strongest reason for full CQRS? A. The team likes new patterns B. Writes are rare C. Read shape and scale differ sharply from writes D. Fewer tests are needed
**Q03 (O2)** In event sourcing, current state is obtained by: A. Reading a cache B. Replaying the aggregate's events C. Deleting old events D. Running a SQL update
**Q04 (O2)** A snapshot is used to: A. Replace the event store B. Encrypt events C. Order events across aggregates D. Start replay from a recent state rather than the beginning
**Q05 (O2)** Upcasting means: A. Raising event priority B. Deleting old events C. Converting old event versions to the current shape on read D. Compressing events
**Q06 (O3)** A cross-service materialized view is best described as: A. A disposable local copy that may be stale B. The source of truth C. A distributed transaction D. A shared database table
**Q07 (O3)** Staleness of a view should be: A. Ignored B. Always zero C. Hidden from users D. Defined as an acceptable lag agreed with the product owner
**Q08 (O4)** A hand-built saga is usually enough when: A. Hundreds of long human workflows exist B. There are few short workflows without timers C. You need visual process editing for analysts D. Workflows last months
**Q09 (O2)** A projection nobody can rebuild is a problem because: A. It uses too little storage B. It is faster C. Bugs cannot be repaired from the log D. It breaks CQRS-lite
**Q10 (O4)** Adopting a workflow engine for a single saga is typically: A. Required B. Cheaper than a state table C. Needed for outbox D. Over-investment with an extra platform to run

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Pattern-selection defense: present the ADR from SRB-001-LAB1 and defend it against challenges. Pass: 70% on the quiz and an ADR with costs estimated for both options.
