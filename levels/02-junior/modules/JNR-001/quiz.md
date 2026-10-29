# JNR-001 · Modern Java — Quiz

Outcomes: O1 release model and LTS · O2 records · O3 sealed types and switch · O4 patterns, text blocks.

**Q01 (O1)** How often does a new Java version appear? A. Every month B. Every year C. Every six months D. Every five years
**Q02 (O1)** What does LTS mean? A. Long-term support B. Latest test snapshot C. Language type system D. Local test server
**Q03 (O1)** Preview features in production code are: A. Recommended B. Required C. Faster D. Risky, because they may change
**Q04 (O2)** A record automatically gives you: A. Setters B. `equals`, `hashCode`, `toString` C. A database table D. Inheritance
**Q05 (O2)** Where do you validate record values? A. In a compact constructor B. In a getter C. In `main` D. In `toString`
**Q06 (O2)** A record has a `List` component. To keep it safe you: A. Do nothing B. Make it `public` C. Add a setter D. Copy it with `List.copyOf`
**Q07 (O3)** What does `sealed ... permits` do? A. Hides a class B. Limits which types may implement it C. Encrypts data D. Makes a class faster
**Q08 (O3)** A switch over a sealed type with a missing case: A. Fails to compile B. Returns null C. Throws at runtime always D. Is ignored
**Q09 (O3)** Why avoid `default` in that switch? A. It is slower B. It is a keyword error C. It hides new, unhandled types D. It needs preview
**Q10 (O4)** `if (o instanceof String s)` does: A. Checks and declares `s` as a String B. Copies the string C. Throws always D. Compares two objects

## Answers
Q01 C · Q02 A · Q03 D · Q04 B · Q05 A · Q06 D · Q07 B · Q08 A · Q09 C · Q10 A

## Practical part
Seven exercises `JNR-001-EX01` to `EX07`, the legacy-refactoring task, and the lab. Pass: at least 8 of 10 quiz answers, six exercises correct, and a lab that fails to compile when a discount type is unhandled.
