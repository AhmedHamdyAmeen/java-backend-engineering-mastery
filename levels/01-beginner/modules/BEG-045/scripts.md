# BEG-045 · Testing fundamentals — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a safety inspector with a checklist who checks the same things every time.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-045-L01 · Why test automatically (8 min)
**Goal:** explain why we write tests as code instead of checking by hand.

**Key points**
- Checking by hand is slow, easy to forget, and done differently each time.
- An **automated test** is a small program that runs your code and checks the result for you.
- Tests run in seconds, as often as you like, and catch **regressions** (old features broken by new changes).
- They act as living documentation: they show how the code should behave.
- Tests give you the confidence to change code.

**Show:** a manual check ("run `main`, look at the output") next to a test that fails loudly when the output is wrong.

**Check:** What is a regression? *(Something that used to work and broke after a change.)*

---

## BEG-045-L02 · Anatomy of a test case (8 min)
**Goal:** name the parts of a good test case.

**Key points**
- A test case has an input, an action, and an **expected result**.
- Pattern: **Arrange** (set up), **Act** (call the code), **Assert** (check the result).
- A good test checks one behavior and has a name that says which.
- Tests must be **independent**: any order, any one alone.
- A test with no assertion proves nothing.

**Show**
```java
// Arrange
Account a = new Account(100);
// Act
a.deposit(50);
// Assert
assertEquals(150, a.getBalance());
```

**Check:** What are the three steps of a test? *(Arrange, Act, Assert.)*

---

## BEG-045-L03 · First JUnit 5 tests (12 min)
**Goal:** write and run a JUnit 5 test class.

**Key points**
- **JUnit 5** is the standard Java testing library. Add it through IntelliJ's library prompt for now; Maven comes later (BEG-054).
- Put the test in its own class; mark each test method with `@Test`.
- Use assertions from `org.junit.jupiter.api.Assertions`: `assertEquals(expected, actual)`, `assertTrue`, `assertFalse`, `assertNull`.
- Expected value goes first, actual value second.
- Run with the green arrow in the IDE; green means all passed.

**Show**
```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {
    @Test
    void addsTwoNumbers() {
        assertEquals(5, new Calculator().add(2, 3));
    }
}
```

**Check:** Which argument of `assertEquals` comes first? *(The expected value.)*

---

## BEG-045-L04 · Testing exceptions (7 min)
**Goal:** check that code fails the right way for bad input.

**Key points**
- Good code rejects bad input; the test must prove it.
- `assertThrows(ExceptionType.class, () -> code)` passes only if that exception is thrown.
- It returns the exception, so you can also check the message.
- No exception, or a different one, fails the test.
- Test one bad case per test.

**Show**
```java
@Test
void rejectsNegativeDeposit() {
    Account a = new Account(100);
    assertThrows(IllegalArgumentException.class, () -> a.deposit(-5));
}
```

**Check:** When does `assertThrows` fail? *(When no exception, or a different type, is thrown.)*

---

## BEG-045-L05 · Boundaries and equivalence classes (10 min)
**Goal:** choose test inputs that find bugs without testing everything.

**Key points**
- **Equivalence class**: a group of inputs the code treats the same. Test one from each group.
- **Boundary**: the edge between groups, where bugs hide (off-by-one).
- Example, a withdraw rule "amount must be above 0 and not above the balance": test -1, 0, 1, balance - 1, balance, balance + 1.
- Always include empty, one item, and many items for collections.
- Test the unhappy paths, not only the happy path.

**Show:** a table for `withdraw` with balance 100: input / expected (-1 error, 0 error, 1 ok, 100 ok leaves 0, 101 error).

**Check:** Why test 100 and 101 when the balance is 100? *(They sit at the boundary, where off-by-one bugs happen.)*

---

## BEG-045-L06 · Reading test failures (5 min)
**Goal:** read a failure message and find the cause.

**Key points**
- A failure shows expected, actual, the test name, and the line.
- `AssertionFailedError: expected: <150> but was: <100>` says the code gave 100.
- An exception in the code shows as an error with a stack trace; read the top lines that mention your code.
- First decide: is the code wrong or the test wrong?
- Fix, rerun, and check all the other tests are still green.

**Show:** a red result in the IDE with the expected/actual comparison and the clickable stack trace line.

**Check:** A test says `expected: <150> but was: <100>`. Which value did the code return? *(100.)*

---

## BEG-045-L07 · Demo: test-first on the bank's withdraw method (8 min)
**Goal:** write the tests before `withdraw` and let them guide the code. Prepares BEG-045-LAB1.

**Steps**
1. List the rules: amount must be positive, cannot exceed the balance, balance decreases.
2. Write three tests first: a normal withdraw, an overdraw, and a negative amount; run them and see them fail.
3. Write the simplest `withdraw` that passes the normal one.
4. **Planned mistake:** use `amount < balance` instead of `amount <= balance`; the boundary test "withdraw exactly the balance" fails. Read the failure and fix the operator.
5. Add the exceptions with `IllegalArgumentException` and rerun until green.
6. Add boundary tests for 0 and 1.

**Check:** Why write the test first? *(It forces a clear requirement and proves the test can fail.)*
