# MID-060 · DDD introduction — Quiz

Outcomes: O1 entities and value objects · O2 aggregates · O3 repositories and domain services · O4 ubiquitous language.

**Q01 (O1)** Which has an identity that persists as attributes change? A. Value object B. Record of money C. Entity D. Enum
**Q02 (O1)** Value objects should be: A. Mutable B. Immutable C. Identified by a database ID D. Always entities
**Q03 (O2)** An invariant is: A. A rule that must always hold B. A database index C. A REST route D. A Spring bean scope
**Q04 (O2)** An aggregate should reference another aggregate by: A. Object reference B. Embedded copy C. A shared table D. Its ID
**Q05 (O2)** One transaction should normally change: A. One aggregate B. All aggregates C. Every table D. Several services
**Q06 (O2)** The best sign of an aggregate that is too big: A. It has a root B. Many unrelated invariants and lock contention C. It has events D. It uses records
**Q07 (O3)** A repository is provided for: A. Every class B. Each `OrderLine` C. Each aggregate root D. Each DTO
**Q08 (O3)** Logic spanning several aggregates belongs in: A. A getter B. The database C. A controller D. A domain service
**Q09 (O4)** The ubiquitous language is: A. A programming language B. Vocabulary shared by experts and developers, used in code C. The SQL schema D. A UML tool
**Q10 (O2)** An anemic domain model means: A. Entities hold data and services hold rules B. Aggregates enforce invariants C. Models use value objects D. Events are in the past tense

## Answers
Q01 C · Q02 B · Q03 A · Q04 D · Q05 A · Q06 B · Q07 C · Q08 D · Q09 B · Q10 A

## Practical part
Six exercises `MID-060-EX01` to `EX06` plus the lab. Pass: at least five exercises correct, and the lab's `Order` enforcing every invariant with a unit test each.
