# JNR-030 · Entity relationships — Quiz

Outcomes: O1 relationship types · O2 owning side and sync · O3 cascade and orphan removal · O4 join entities.

**Q01 (O1)** The foreign key column lives on the: A. "One" side B. Neither, in a hidden table always C. Application server D. "Many" side
**Q02 (O1)** The default fetch type of `@ManyToOne` is: A. `EAGER` B. `LAZY` C. `NONE` D. `BATCH`
**Q03 (O1)** Recommended fetch type for `@ManyToOne`: A. `EAGER` always B. `LAZY` C. Random D. `SELECT`
**Q04 (O2)** The owning side is the one: A. With `mappedBy` B. With the larger table C. Without `mappedBy` (holding the foreign key) D. Declared first
**Q05 (O2)** If you add to the list but do not set the owning side: A. The foreign key stays null B. Both sides are saved C. An automatic fix is applied D. The list is cleared
**Q06 (O2)** Helper methods like `addLine` exist to: A. Speed up queries B. Keep both sides in sync C. Replace getters D. Create tables
**Q07 (O3)** `orphanRemoval = true` means: A. Remove the parent when the child is removed B. Delete the database C. Remove a child when removed from the parent's collection D. Disable cascades
**Q08 (O3)** Should `OrderLine` cascade `REMOVE` to `Product`? A. Yes B. Never C. Only in tests D. Yes, with `ALL`
**Q09 (O4)** `@ManyToMany` is a problem when the link: A. Has no data B. Is read-only C. Is a collection D. Needs extra columns like quantity
**Q10 (O4)** `OrderLine` with quantity and price is best modeled as: A. A join entity B. A `@ManyToMany` C. An enum D. An embeddable list in `Product`

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 A · Q06 B · Q07 C · Q08 B · Q09 D · Q10 A

## Practical part
Six exercises `JNR-030-EX01` to `EX06` plus the lab; the assessment is mapping a provided ER diagram (EX06). Pass: the ER mapping has correct owning sides and cascades, at least five of six exercises correct, lab tests green.
