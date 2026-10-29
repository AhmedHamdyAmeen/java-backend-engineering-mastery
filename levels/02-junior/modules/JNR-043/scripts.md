# JNR-043 · Unit testing — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a quality inspector who checks one part on the bench before it goes into the machine.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-043-L01 · What a unit is (7 min)
**Goal:** decide what to test in a unit test and what to leave out.

**Key points**
- A unit is a small piece of behavior: usually one class or one method with its logic.
- A unit test runs in milliseconds, with no database, network, or files.
- Test the public behavior (inputs and outputs), not private methods. If a private method seems to need a test, the logic probably belongs in its own class.
- A good test fails for one reason only, and its name says which.
- Verify the current JUnit Jupiter version before recording.

**Show**
```java
class PriceCalculatorTest {
    @Test
    void appliesTenPercentDiscount() {
        var calc = new PriceCalculator();
        assertEquals(new BigDecimal("90.00"), calc.discounted(new BigDecimal("100.00"), 10));
    }
}
```

**Check:** Should a unit test talk to PostgreSQL? *(No; that is an integration test.)*

---

## JNR-043-L02 · Lifecycle and structure (10 min)
**Goal:** use the JUnit Jupiter lifecycle annotations to keep tests tidy.

**Key points**
- `@BeforeEach` runs before every test; `@AfterEach` runs after every test. JUnit makes a fresh test-class instance per test, so tests do not share fields.
- `@BeforeAll` / `@AfterAll` run once per class and are static by default.
- `@DisplayName` gives a readable name in reports.
- `@Nested` groups tests by situation (for example "when the cart is empty").
- `@Disabled` skips a test, but always with a reason.

**Show**
```java
@DisplayName("Cart")
class CartTest {
    Cart cart;
    @BeforeEach void setUp() { cart = new Cart(); }

    @Nested @DisplayName("when empty")
    class WhenEmpty {
        @Test void totalIsZero() { assertEquals(BigDecimal.ZERO, cart.total()); }
    }
}
```

**Check:** How many times does `@BeforeEach` run for a class with four tests? *(Four.)*

---

## JNR-043-L03 · Parameterized tests (12 min)
**Goal:** run one test body against many inputs.

**Key points**
- `@ParameterizedTest` replaces copy-pasted tests that differ only in data.
- `@ValueSource` for a list of single values.
- `@CsvSource` for several columns per row (input and expected result).
- `@MethodSource` for complex objects built in a static method.
- Use `{0}`-style placeholders in the `name` attribute so failures say which row broke.

**Show**
```java
@ParameterizedTest(name = "{0}% off {1} = {2}")
@CsvSource({"10,100.00,90.00", "0,100.00,100.00", "50,80.00,40.00"})
void discountTable(int pct, BigDecimal price, BigDecimal expected) {
    assertEquals(0, expected.compareTo(calc.discounted(price, pct)));
}
```

**Check:** Which source fits a table of input/expected pairs? *(`@CsvSource`.)*

---

## JNR-043-L04 · AssertJ (12 min)
**Goal:** write assertions that read like sentences and give clear failures.

**Key points**
- AssertJ starts with `assertThat(actual)` and chains checks.
- Collections: `containsExactly`, `contains`, `hasSize`, `extracting`.
- Exceptions: `assertThatThrownBy(...)` or `assertThatExceptionOfType(...)`, then check type and message.
- Numbers and decimals: `isEqualByComparingTo` for `BigDecimal`.
- Failure messages show actual versus expected, so you debug faster.

**Show**
```java
assertThat(orders).extracting(Order::status).containsExactly(NEW, PAID);
assertThatThrownBy(() -> cart.add(null))
    .isInstanceOf(IllegalArgumentException.class)
    .hasMessageContaining("product");
```

**Check:** Which AssertJ method checks that code throws? *(`assertThatThrownBy`.)*

---

## JNR-043-L05 · Coverage and its limits (9 min)
**Goal:** read a coverage report and not be fooled by it.

**Key points**
- Coverage tools (for example JaCoCo) show which lines and branches ran during tests.
- Low coverage shows untested code; high coverage does not show tested behavior.
- A test with no assertions gives coverage and no protection.
- Mutation testing changes your code on purpose; if tests still pass, the mutant "survived" and the test is weak.
- Use coverage to find gaps, not as a target to hit.

**Show:** a method `isAdult(age)` with a test that calls it and asserts nothing: 100% line coverage, zero protection. Then a mutation (`>=` to `>`) survives.

**Check:** Can 100% coverage coexist with a bug? *(Yes; running a line is not checking its result.)*

---

## JNR-043-L06 · Demo: turning copy-pasted tests into a parameterized table (10 min)
**Goal:** refactor repeated tests into one table. Prepares `JNR-043-LAB1`.

**Steps**
1. Show ten near-identical tests for Shop discount and tax rules.
2. Create one `@ParameterizedTest` with `@CsvSource`; move the data into rows.
3. Add a readable `name` template and run; each row reports separately.
4. Add edge rows (zero, maximum discount, rounding).
5. **Planned mistake:** compare `BigDecimal` with `assertEquals` and `100.0` vs `100.00` fails; fix with `isEqualByComparingTo`.
6. Plant a bug in the calculator and show a row failing.
