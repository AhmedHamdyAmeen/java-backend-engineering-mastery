# BEG-045 · Testing fundamentals — Quiz

Outcomes: O1 why test and test-case anatomy · O2 JUnit 5 · O3 boundaries and equivalence classes · O4 running tests and reading failures.

**Q01 (O1)** A regression is: A. A new feature B. A faster algorithm C. Something that worked and broke after a change D. A kind of exception
**Q02 (O1)** The three steps of a test are: A. Arrange, Act, Assert B. Build, Run, Ship C. Read, Write, Save D. Push, Pop, Peek
**Q03 (O1)** A test with no assertion: A. Checks everything B. Is the fastest kind C. Always fails D. Proves nothing
**Q04 (O2)** The annotation that marks a JUnit 5 test method is: A. `@Run` B. `@Check` C. `@Test` D. `@Assert`
**Q05 (O2)** In `assertEquals(a, b)` the first argument should be the: A. Actual value B. Expected value C. Message D. Exception
**Q06 (O2)** To check that code throws `IllegalArgumentException` use: A. `assertTrue` B. `assertNull` C. `try` with no catch D. `assertThrows`
**Q07 (O3)** A boundary test for "age must be at least 18" should include: A. 17 and 18 B. Only 30 C. Only 5 D. Only 100
**Q08 (O3)** An equivalence class is a group of inputs that: A. Are equal B. The code treats the same way C. Are all negative D. Are all `null`
**Q09 (O3)** Which tests a method best? A. Only the happy path B. Only one random input C. Happy path, boundaries, and invalid input D. Nothing; read the code
**Q10 (O4)** `expected: <5> but was: <4>` means the code returned: A. 5 B. 9 C. Nothing D. 4

## Answers
Q01 C · Q02 A · Q03 D · Q04 C · Q05 B · Q06 D · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Write tests for a provided class with hidden bugs (score = bugs caught) plus lab `BEG-045-LAB1` (at least 20 meaningful tests) and exercises `BEG-045-EX01` to `EX06`. Pass: at least half of the hidden bugs caught, the lab acceptance met, and at least 8 of 10 quiz answers correct.
