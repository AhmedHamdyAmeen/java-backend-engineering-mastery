# JNR-028 · JPA and Hibernate — Quiz

Outcomes: O1 entity mapping · O2 entity states · O3 dirty checking and flush · O4 equals/hashCode · O5 SQL logging.

**Q01 (O1)** The safe way to store an enum is: A. `EnumType.ORDINAL` B. `EnumType.STRING` C. As a `double` D. Default always
**Q02 (O1)** An `@Embeddable` is stored: A. In its own table B. In a separate database C. As columns of the owner's table D. In memory only
**Q03 (O1)** `GenerationType.IDENTITY` has the drawback of: A. Needing UUIDs B. Disabling insert batching C. Not working with PostgreSQL D. Making ids negative
**Q04 (O1)** Entities should be returned directly from controllers: A. Always B. Only for GET C. Only with Lombok D. Never as a rule; use DTOs
**Q05 (O2)** An object created with `new Product()` is: A. Managed B. Detached C. Transient D. Removed
**Q06 (O2)** After the transaction ends, a loaded entity is: A. Detached B. Transient C. Removed D. Still managed forever
**Q07 (O3)** Dirty checking means Hibernate: A. Deletes unused rows B. Validates SQL syntax C. Compares entities with a snapshot to find changes D. Cleans the cache
**Q08 (O3)** `p.setName("X")` on a managed entity inside a transaction: A. Updates the row at flush B. Updates immediately every time C. Is ignored D. Throws an exception
**Q09 (O4)** Why is Lombok `@Data` risky on entities? A. It makes classes final B. It removes getters C. Its `equals`/`hashCode` use all fields D. It breaks `@Id`
**Q10 (O5)** To see generated SQL you: A. Enable the Hibernate SQL logger B. Open the JAR C. Disable the pool D. Use `System.out` in entities

## Answers
Q01 B · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 C · Q08 A · Q09 C · Q10 A

## Practical part
Seven exercises `JNR-028-EX01` to `EX07` plus the lab; the assessment is the "predict the SQL" exercise (EX04). Pass: EX04 correct, at least five of seven exercises correct, and the lab explanation matches the log.
