# BEG-021 · Encapsulation — Quiz

Outcomes: O1 access modifiers · O2 invariants · O3 getters/setters vs behavior · O4 immutability.

**Q01 (O1)** Visible only inside its own class: A. `public` B. `protected` C. package-private D. `private`
**Q02 (O1)** The default access (no modifier) is: A. `public` B. package-private C. `private` D. `protected`
**Q03 (O1)** `protected` allows access from: A. The same package and subclasses B. Only the same class C. Everywhere D. Nowhere
**Q04 (O2)** An invariant is: A. A loop B. A static field C. A rule that is always true for the object D. A comment
**Q05 (O2)** Where should "balance never negative" be enforced? A. In every caller B. In the Account class C. In the database only D. In the README
**Q06 (O2)** On invalid input a method should: A. Ignore it silently B. Set the value to 0 C. Print and continue D. Throw an exception with a clear message
**Q07 (O3)** The best replacement for `setBalance` is: A. `deposit` and `withdraw` B. `public balance` C. `static balance` D. Nothing, keep it
**Q08 (O3)** "Tell, don't ask" means: A. Always use getters B. Never use methods C. Tell the object what to do rather than reading its data and deciding outside D. Ask the user first
**Q09 (O4)** An immutable class has: A. Setters for all fields B. `private final` fields and no setters C. Only static fields D. Public fields
**Q10 (O4)** A defensive copy is needed when a field: A. Is an `int` B. Is `private` C. Is a constant D. Holds a mutable object such as a `List`

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 B · Q06 D · Q07 A · Q08 C · Q09 B · Q10 D

## Practical part
Code review exercise `BEG-021-EX06` plus `EX01` to `EX05` and Bank Accounts v2. Pass: review finds at least four of the planted violations and the lab meets its acceptance.
