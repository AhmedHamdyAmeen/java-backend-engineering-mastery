# BEG-029 · Exceptions — Quiz

Outcomes: O1 hierarchy · O2 try/catch/finally · O3 throw and throws · O4 custom exceptions · O5 try-with-resources.

**Q01 (O1)** Which is a checked exception? A. `IOException` B. `NullPointerException` C. `IllegalArgumentException` D. `OutOfMemoryError`
**Q02 (O1)** `NullPointerException` is: A. Checked B. An `Error` C. Unchecked D. Not a Throwable
**Q03 (O1)** Which should normal code not try to catch? A. `IOException` B. `NumberFormatException` C. `IllegalStateException` D. `OutOfMemoryError`
**Q04 (O2)** When does `finally` run? A. Only on error B. Only on success C. Never D. Always
**Q05 (O2)** With two catch blocks, the more specific type should come: A. First B. Last C. Order never matters D. In a separate method
**Q06 (O2)** The best catch is: A. `catch (Exception e) {}` B. The narrowest useful type with real handling C. `catch (Throwable t) {}` D. No catch at all
**Q07 (O3)** `throws IOException` on a method means: A. It always fails B. It catches IOException C. It may raise it; callers must handle or declare D. It is unchecked
**Q08 (O3)** A good exception message: A. Is empty B. Says what was wrong and the value involved C. Is always "Error" D. Is only a number
**Q09 (O4)** A custom checked exception extends: A. `Exception` B. `RuntimeException` C. `Error` D. `Object` only
**Q10 (O5)** try-with-resources requires the resource to implement: A. `Runnable` B. `Comparable` C. `Serializable` D. `AutoCloseable`

## Answers
Q01 A · Q02 C · Q03 D · Q04 D · Q05 A · Q06 B · Q07 C · Q08 B · Q09 A · Q10 D

## Practical part
Five exercises `BEG-029-EX01` to `EX05` plus the swallowed-exception review `EX06` and the lab. Pass: at least four exercises correct, the review fixed, and no empty catch in the lab.
