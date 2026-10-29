# JNR-043 · Unit testing — Exercises and lab

## Lab
### JNR-043-LAB1 · Pricing rules suite
**Outcomes:** 1–4 · **Time:** ~3 h
Write parameterized tests for every discount and tax combination in Shop Core. Use `@Nested` groups, AssertJ assertions, and a JaCoCo report.
**Acceptance:** one table-driven test replaces at least 10 copy-pasted ones; a planted bug is caught.

## Exercises (assessment: write tests for an unseen class, graded by mutation survivors)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-043-EX01 | 1 | Add `@BeforeEach`, `@DisplayName`, and two `@Nested` classes to a `Cart` test; explain how many times `@BeforeEach` runs. |
| JNR-043-EX02 | 2 | Turn five copy-pasted `isValidEmail` tests into one `@ParameterizedTest` with `@ValueSource`. |
| JNR-043-EX03 | 2 | Write a `@CsvSource` test for a shipping-cost rule (weight, zone, expected cost) and a `@MethodSource` variant with objects. |
| JNR-043-EX04 | 3 | Rewrite three JUnit `assertEquals` checks on a list of orders using AssertJ `extracting` and `containsExactly`. |
| JNR-043-EX05 | 3 | Assert that `Cart.add(null)` throws `IllegalArgumentException` with a message containing "product". |
| JNR-043-EX06 | 4 | Write a test with no assertions that gives 100% line coverage of a method; then add the assertion that kills a mutant. |
| JNR-043-EX07 | 1 | A test calls a private method through reflection. Explain why that is a problem and how to restructure. |

## Solutions
- **EX01** `@BeforeEach` runs once before each test, so with N tests it runs N times (for a nested class it also runs the outer `@BeforeEach` first).
- **EX02** `@ParameterizedTest @ValueSource(strings = {"", " ", "a@", "@b.com", "a b@c.com"})` asserting `isFalse()`.
- **EX03** `@CsvSource({"1.0,LOCAL,5.00", "5.0,LOCAL,9.00", "1.0,INTL,20.00"})`; the `@MethodSource` method returns `Stream<Arguments>`.
- **EX04** `assertThat(orders).extracting(Order::id).containsExactly(1L, 2L);`
- **EX05** `assertThatThrownBy(() -> cart.add(null)).isInstanceOf(IllegalArgumentException.class).hasMessageContaining("product");`
- **EX06** Call `isAdult(18)` with no assertion: line covered. Add `assertThat(isAdult(18)).isTrue()` and `isAdult(17)` false; the `>=` to `>` mutant now fails.
- **EX07** Private methods are implementation detail; test them through public behavior, or extract the logic into its own class with a public API.
- Outcome 4 (coverage is not quality) is also covered by quiz Q09–Q10 and the lab acceptance (planted bug).
