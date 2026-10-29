# JNR-043 · Unit testing — Quiz

Outcomes: O1 lifecycle · O2 parameterized · O3 AssertJ · O4 coverage.

**Q01 (O1)** Which annotation runs before every test method? A. `@BeforeAll` B. `@Test` C. `@Nested` D. `@BeforeEach`
**Q02 (O1)** `@Nested` is used to: A. Group tests by situation inside a class B. Skip a test C. Run tests in parallel D. Mock a class
**Q03 (O1)** Which is the best thing to test? A. Private methods B. Public behavior C. Getters only D. The JVM
**Q04 (O2)** Which source gives several columns per row? A. `@ValueSource` B. `@NullSource` C. `@CsvSource` D. `@EnumSource` only
**Q05 (O2)** Why use `@ParameterizedTest`? A. Replace copy-pasted tests that differ only by data B. Make tests slower C. Avoid assertions D. Test private code
**Q06 (O3)** Which AssertJ call starts an assertion? A. `check(x)` B. `assertThat(x)` C. `expect(x)` D. `verify(x)`
**Q07 (O3)** To check that code throws, use: A. `assertThatThrownBy` B. `containsExactly` C. `hasSize` D. `extracting`
**Q08 (O3)** Which verifies list contents in exact order? A. `hasSize` B. `isEmpty` C. `contains` D. `containsExactly`
**Q09 (O4)** A test with no assertions but full line coverage: A. Proves the code is correct B. Is useful as it is C. Gives coverage without protection D. Is impossible
**Q10 (O4)** A surviving mutant means: A. The tests are weak for that change B. The code is perfect C. Coverage is 0% D. The build failed

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 A · Q06 B · Q07 A · Q08 D · Q09 C · Q10 A

## Practical part
Seven exercises `JNR-043-EX01` to `EX07` plus the lab; for the assessment, write tests for an unseen class and have the mutation score checked. Pass: quiz 8/10, at least five exercises correct, and few mutation survivors.
