# SRC-014 · Data integrity — Quiz

Outcomes: O1 cross-service invariants · O2 exactly-once effects · O3 reconciliation · O4 audit trails.

**Q01 (O1)** An invariant is: A. A log line B. A rule that must always hold C. A retry policy D. A cache key
**Q02 (O1)** Cross-service invariants need design because: A. Databases forbid them B. They are cosmetic C. No single transaction spans the services D. They are automatic
**Q03 (O2)** Exactly-once delivery over a network is: A. Provided by every broker B. Trivial C. Required by law D. Not achievable in general; design for exactly-once effects
**Q04 (O2)** The practical way to get exactly-once effects is: A. Idempotent handling of repeated deliveries B. Disabling retries C. Larger timeouts D. More servers
**Q05 (O2)** A payment retry after timeout should use: A. A new key every time B. No key C. The same idempotency key D. A random delay only
**Q06 (O3)** Reconciliation compares: A. Two sources of record by a stable key B. Source code versions C. Only totals D. Developer opinions
**Q07 (O3)** Comparing only totals is risky because: A. It is slow B. Offsetting errors cancel out C. It is illegal D. It needs more storage
**Q08 (O3)** A reconciliation repair should: A. Be silent B. Edit history C. Be logged with actor and reason D. Skip review for all cases
**Q09 (O4)** An audit trail should be: A. Updatable by the app B. Append-only C. Optional for money D. Deleted weekly
**Q10 (O1)** Messaging guarantees remove the need for reconciliation: A. Always B. Never; bugs and external systems still cause drift C. Only in tests D. Only for Kafka

## Answers
Q01 B · Q02 C · Q03 D · Q04 A · Q05 C · Q06 A · Q07 B · Q08 C · Q09 B · Q10 B

## Practical part
Invariant analysis of an unseen workflow (SRC-014 assessment), plus the `SRC-014-LAB1` reconciliation report. Pass: at least 8/10 on the quiz, invariants identified with a control for each, and repairs that are audited.
