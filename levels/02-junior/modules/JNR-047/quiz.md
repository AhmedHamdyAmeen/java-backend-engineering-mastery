# JNR-047 · Testing practices — Quiz

Outcomes: O1 AAA and naming · O2 test data · O3 brittle and flaky tests · O4 suite balance.

**Q01 (O1)** In Arrange-Act-Assert, "Act" means: A. Set up data B. Check results C. Clean up D. Call the code under test
**Q02 (O1)** Best test name: A. `test1` B. `rejectsOrderWhenStockIsZero` C. `orderTest` D. `works`
**Q03 (O2)** A test data builder gives: A. Valid defaults with overrides B. Random data only C. Production data D. No defaults
**Q04 (O2)** An object mother is: A. A superclass B. A mock C. A class of named test-object factories D. A database
**Q05 (O3)** Which causes a flaky test? A. A fixed clock B. Unique data C. Pure functions D. Dependence on test order
**Q06 (O3)** Best way to control time in tests: A. `Thread.sleep` B. Inject a `Clock` C. Change the system date D. Ignore it
**Q07 (O3)** A brittle test: A. Breaks on harmless refactors B. Never fails C. Is always fast D. Tests private code only
**Q08 (O3)** Better than `Thread.sleep` for async checks: A. A longer sleep B. A random delay C. Awaiting a condition D. Disabling the test
**Q09 (O4)** A healthy suite has the most: A. End-to-end tests B. Manual tests C. Mock tests only D. Unit tests
**Q10 (O4)** A suite with 150 slow integration tests and 5 unit tests suffers from: A. Slow feedback B. Too much coverage C. Too many builders D. Fast feedback

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 D · Q06 B · Q07 A · Q08 C · Q09 D · Q10 A

## Practical part
Seven exercises `JNR-047-EX01` to `EX07` plus the lab; for the assessment, review the quality of a given test suite. Pass: quiz 8/10, at least five exercises correct, and 10 consecutive green runs in the lab.
