# JNR-031 · Transactions — Quiz

Outcomes: O1 ACID · O2 boundaries at the service layer · O3 rollback rules · O4 proxies and self-invocation · O5 short and read-only transactions.

**Q01 (O1)** Atomicity means: A. Fast queries B. Encrypted data C. Parallel threads D. All steps happen or none
**Q02 (O1)** Durability means committed data: A. Survives a crash B. Is cached C. Is encrypted D. Is deleted after a day
**Q03 (O2)** `@Transactional` usually belongs on: A. Controllers B. Entities C. Service methods D. Repositories only
**Q04 (O2)** The transaction boundary should match: A. One SQL statement B. One business operation C. One HTTP header D. One class
**Q05 (O3)** By default Spring rolls back on: A. Checked exceptions only B. Unchecked exceptions C. Every exception D. No exception
**Q06 (O3)** Catching an exception inside the method without rethrowing: A. Always rolls back B. Throws a new error C. Prevents a rollback D. Commits twice
**Q07 (O4)** Self-invocation fails because: A. The method is too long B. The call skips the proxy C. The database refuses D. Java forbids it
**Q08 (O4)** A reliable fix for self-invocation: A. Make the method private B. Add `final` C. Add `static` D. Move the method to another bean
**Q09 (O5)** A payment API call inside a transaction is bad because: A. It holds a connection and cannot be rolled back B. HTTP is forbidden C. It is slower to type D. It uses more heap
**Q10 (O5)** `readOnly = true` is meant for: A. Writes B. Deleting C. Query-only methods D. Schema changes

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 B · Q06 C · Q07 B · Q08 D · Q09 A · Q10 C

## Practical part
Six exercises `JNR-031-EX01` to `EX06` plus the lab; the assessment is fixing a broken transaction implementation and explaining why it failed (EX06). Pass: the fix works, the explanation names the proxy rule, and the lab failure tests prove atomicity.
