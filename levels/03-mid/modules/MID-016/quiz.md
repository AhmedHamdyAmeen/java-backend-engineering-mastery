# MID-016 · Advanced transactions — Quiz

Outcomes: O1 optimistic locking and 409 · O2 choosing a strategy · O3 propagation · O4 safe retries.

**Q01 (O1)** `@Version` makes Hibernate: A. Add a version check to updates B. Lock the table C. Disable caching D. Create indexes
**Q02 (O1)** A failed version check should usually return HTTP: A. 200 B. 404 C. 409 D. 500
**Q03 (O1)** For optimistic locking across two HTTP requests the client must: A. Hold a DB connection B. Retry forever C. Use sessions D. Send back the version it read
**Q04 (O2)** Best fit for optimistic locking: A. Hot stock counter B. Low-conflict profile edits C. A job queue D. A global counter
**Q05 (O2)** Best first choice for a hot stock decrement: A. Optimistic with retries B. Client-side check C. Atomic `UPDATE ... WHERE qty > 0` D. Serializable for everything
**Q06 (O3)** `REQUIRES_NEW` runs the method in: A. A new transaction on a separate connection B. The same transaction C. No transaction D. A savepoint
**Q07 (O3)** `NESTED` propagation is implemented with: A. A second connection B. A trigger C. A thread D. A savepoint
**Q08 (O3)** Calling a `@Transactional(REQUIRES_NEW)` method from the same class: A. Starts a new transaction B. Is ignored due to proxy bypass C. Throws at startup D. Uses two connections
**Q09 (O4)** Which errors are safe to retry? A. Deadlock or serialization failures B. Validation errors C. All exceptions D. Out-of-memory
**Q10 (O4)** Retried units of work should be: A. Asynchronous B. Random C. Idempotent D. Unbounded

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 C · Q06 A · Q07 D · Q08 B · Q09 A · Q10 C

## Practical part
Fix a given transaction design (a service with a missing version check, a self-invocation bug, and an unsafe retry). Pass: quiz 8/10, all three defects found and fixed, and the lab tests passing.
