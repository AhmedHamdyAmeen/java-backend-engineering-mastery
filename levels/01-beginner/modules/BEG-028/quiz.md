# BEG-028 · OOP design practice — Quiz

Outcomes: O1 modeling · O2 responsibilities · O3 god classes · O4 explaining a design.

**Q01 (O1)** A good first step in modeling from a description is to: A. Write all code at once B. Add inheritance everywhere C. Underline nouns and verbs D. Skip the description
**Q02 (O1)** Nouns in a description become: A. Candidates: some are classes, some fields B. Always classes C. Always methods D. Packages only
**Q03 (O1)** Premature inheritance means: A. Using interfaces B. Using `extends` before a real variation exists C. Writing tests early D. Using packages
**Q04 (O2)** Where should `Ticket.isExpired(now)` live? A. In a global `Util` class B. In the garage's `Level` C. In `Main` D. In `Ticket`, which knows its time
**Q05 (O2)** The best home for a behavior is the class that: A. Has the information needed B. Is largest C. Is oldest D. Is abstract
**Q06 (O3)** A sign of a god class is: A. A single clear job B. Few lines C. Many unrelated responsibilities D. Immutable fields
**Q07 (O3)** An anemic class: A. Has no fields B. Holds data only, with logic elsewhere C. Is abstract D. Is a record always
**Q08 (O3)** To split a god class you: A. Delete it B. Make all fields `public` C. Make it `final` D. Separate it by responsibility, step by step
**Q09 (O4)** In a design explanation you should: A. State the main decisions and rejected alternatives B. Hide trade-offs C. Read the code aloud D. Avoid diagrams
**Q10 (O4)** A reviewer finds a flaw in your design. A good response: A. Ignore it B. Delete the diagram C. Discuss it and decide whether to change D. Argue without listening

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 A · Q06 C · Q07 B · Q08 D · Q09 A · Q10 C

## Practical part
Design review of the parking garage with the design dimension of `assessment/framework.md`, the exercises `BEG-028-EX01` to `EX05`, and a completed peer review. Pass: the design rubric's passing level plus the quiz at 7/10.
