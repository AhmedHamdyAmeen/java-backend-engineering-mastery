# BEG-026 · Java object model — Quiz (contract)

Outcomes: O1 `Object` · O2 identity vs equality · O3 `equals`/`hashCode` · O4 `toString`.

**Q01 (O1)** Every Java class extends, directly or indirectly: A. `Object` B. `Class` C. `System` D. `Main`
**Q02 (O1)** Which method does `Object` NOT have? A. `toString` B. `equals` C. `compareAll` D. `hashCode`
**Q03 (O2)** `==` on two object references checks: A. Same content B. Same length C. Same class name D. Same object in memory
**Q04 (O2)** The correct way to compare two strings' text: A. `a == b` B. `a.equals(b)` C. `a = b` D. `a.same(b)`
**Q05 (O2)** The default `equals` from `Object` behaves like: A. Always false B. Comparing all fields C. Always true D. `==`
**Q06 (O3)** If `a.equals(b)` is true, then: A. Their hash codes must be equal B. Their hash codes must differ C. Nothing is required D. They are the same object
**Q07 (O3)** Overriding `equals` but not `hashCode` can cause: A. A compile error B. Faster code C. Duplicates in a `HashSet` D. Nothing
**Q08 (O3)** Which field is risky to use in `hashCode`? A. A `final` id B. A mutable field that changes after storing C. A `String` name that never changes D. A constant
**Q09 (O4)** `toString` output should NOT contain: A. The class name B. Key fields C. A balance D. Passwords
**Q10 (O3)** A `record` automatically gets: A. `equals`, `hashCode`, and `toString` B. Only getters C. A database table D. Mutable setters

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 D · Q06 A · Q07 C · Q08 B · Q09 D · Q10 A

## Practical part
Contract quiz above plus implementation exercise `BEG-026-EX04` and the broken-set lab. Pass: quiz 8/10 and a correct `equals`/`hashCode` pair with the duplicate behavior explained.
