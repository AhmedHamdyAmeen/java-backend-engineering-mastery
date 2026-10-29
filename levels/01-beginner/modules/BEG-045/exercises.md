# BEG-045 · Testing fundamentals — Exercises and lab

## Lab
### BEG-045-LAB1 · Test what you built
**Outcomes:** 1–4 · **Time:** ~4 h
1. Add JUnit 5 to the project through IntelliJ's library prompt.
2. Write tests for `MyArrayList` (empty, one item, resize, bad index), `MyHashMap` (put, replace, missing key, many keys), and the bank's `withdraw` (boundaries and exceptions).
3. Name each test by behavior and follow Arrange, Act, Assert.
4. Run all tests in the IDE; fix or plant a bug and show a test catching it.
**Acceptance:** at least 20 meaningful tests; one bug found or a planted bug caught.

## Exercises (assessment: write tests for a provided class with hidden bugs; score = bugs caught)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-045-EX01 | 1 | Give three reasons automated tests beat checking by hand, and say what a regression is. |
| BEG-045-EX02 | 1 | The test `void t() { new Account(10).deposit(5); }` has a problem. Name it and fix it. |
| BEG-045-EX03 | 2 | Write a JUnit 5 test for `int max(int a, int b)` with two cases. |
| BEG-045-EX04 | 2 | Write a test proving `Account.withdraw(-1)` throws `IllegalArgumentException`. |
| BEG-045-EX05 | 3 | A method `isAdult(int age)` returns true from 18 up and rejects negative ages. List the equivalence classes and the boundary inputs. |
| BEG-045-EX06 | 4 | A test reports `expected: <3> but was: <2>` for `list.size()` after three adds. List the steps to find the cause. |

## Solutions
- **EX01** Faster, repeatable, catches regressions, documents behavior. A regression is a feature that worked and broke after a change.
- **EX02** It has no assertion, so it can never fail. Add `assertEquals(15, account.getBalance());` after the deposit.
- **EX03** `@Test void returnsLarger() { assertEquals(7, max(3, 7)); } @Test void handlesEqual() { assertEquals(4, max(4, 4)); }`
- **EX04** `assertThrows(IllegalArgumentException.class, () -> account.withdraw(-1));`
- **EX05** Classes: negative (error), 0 to 17 (false), 18 and above (true). Boundaries: -1, 0, 17, 18, 19.
- **EX06** Read the message (code returned 2); click the failing line; check the three adds (one may be rejected, or `add` is not incrementing `size`); fix the code and rerun all tests.
