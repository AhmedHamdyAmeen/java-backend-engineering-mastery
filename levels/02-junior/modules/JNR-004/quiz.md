# JNR-004 · SOLID principles — Quiz

Outcomes: O1 state principles and find violations · O2 refactor · O3 dependency inversion and DI · O4 judgment.

**Q01 (O1)** The "S" in SOLID stands for: A. Simple B. Single Responsibility C. Static D. Sealed
**Q02 (O1)** A class that changes for tax, email, and database reasons breaks: A. LSP B. DIP C. SRP D. ISP
**Q03 (O1)** An override that throws `UnsupportedOperationException` usually breaks: A. Liskov Substitution B. Open/Closed C. SRP D. Nothing
**Q04 (O2)** To follow Open/Closed for a new discount type you: A. Edit a big `if` chain B. Copy the class C. Delete tests D. Add a new class implementing the interface
**Q05 (O2)** A huge interface with many unused methods is fixed by: A. More methods B. Splitting it into small interfaces C. Making it a class D. Adding `default`
**Q06 (O3)** Dependency inversion means high-level code depends on: A. Concrete classes B. Static methods C. Interfaces D. Global variables
**Q07 (O3)** Constructor injection helps testing because: A. It is faster B. It compiles less C. It removes interfaces D. You can pass a fake
**Q08 (O3)** Spring's dependency injection is built on: A. Dependency Inversion B. Sealed classes C. Records D. Text blocks
**Q09 (O4)** An interface with one implementation and no need to swap it is: A. Required B. Often needless C. A security rule D. Faster
**Q10 (O4)** When should you apply a principle? A. Always everywhere B. Never C. When it removes real pain D. Only in tests

## Answers
Q01 B · Q02 C · Q03 A · Q04 D · Q05 B · Q06 C · Q07 D · Q08 A · Q09 B · Q10 C

## Practical part
Six exercises `JNR-004-EX01` to `EX06` plus the lab, with the design quiz as the written assessment. Pass: at least 8 of 10 quiz answers, five exercises correct, and a core with no dependency on a concrete provider.
