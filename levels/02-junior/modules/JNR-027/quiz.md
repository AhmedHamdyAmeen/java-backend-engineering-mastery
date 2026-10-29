# JNR-027 · ORM fundamentals — Quiz

Outcomes: O1 impedance mismatch · O2 what an ORM does and costs · O3 persistence context.

**Q01 (O1)** The object-relational impedance mismatch is: A. A slow network B. A gap between object models and table models C. A Hibernate bug D. A JDBC driver error
**Q02 (O1)** Which is NOT one of the classic mismatches? A. Identity B. Granularity C. Associations D. Syntax highlighting
**Q03 (O1)** A `Money` value object stored as two columns shows a mismatch of: A. Inheritance B. Identity C. Granularity D. Transactions
**Q04 (O2)** An ORM automates: A. Schema design decisions B. Business rules C. Index selection D. Generating basic SQL and mapping rows
**Q05 (O2)** A real cost of an ORM is: A. Hidden or surprise queries B. No type safety C. Cannot read data D. No transactions
**Q06 (O2)** JPA is: A. A database B. A specification, implemented by Hibernate C. A web framework D. A JDBC driver
**Q07 (O2)** With an ORM you still need SQL knowledge to: A. Compile code B. Write controllers C. Read generated SQL and design the schema D. Start Spring
**Q08 (O3)** The persistence context works as: A. A global cache shared by all users B. A file on disk C. A connection pool D. An identity map and unit of work
**Q09 (O3)** `find(1)` twice in one transaction issues: A. One select B. Two selects C. Zero selects D. Three selects
**Q10 (O3)** Flush means: A. Delete all entities B. Close the connection C. Send pending SQL to the database D. Reload entities

## Answers
Q01 B · Q02 D · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 D · Q09 A · Q10 C

## Practical part
Six exercises `JNR-027-EX01` to `EX06` plus the lab; the assessment is this quiz. Pass: at least 8 of 10 quiz questions and a reasoned lab list.
