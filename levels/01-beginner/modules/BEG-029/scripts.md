# BEG-029 · Exceptions — Lecture scripts

**Video:** 71 min · **Analogy used throughout:** a fire alarm and an emergency plan.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-029-L01 · What goes wrong at runtime (8 min)
**Goal:** see that programs fail while running, and that Java reports it with an exception.

**Key points**
- Some errors are found by the compiler. Others only appear when the program runs: bad input, missing file, dividing by zero.
- When this happens Java creates an exception object and "raises the alarm".
- If nobody handles it, the program stops and prints a stack trace.
- A stack trace lists the exception type, the message, and the chain of calls that led there. Read it from the top.

**Show**
```java
int[] nums = new int[3];
System.out.println(nums[5]); // ArrayIndexOutOfBoundsException
```

**Check:** What does Java print when an exception is not handled? *(A stack trace, and the program stops.)*

---

## BEG-029-L02 · The exception hierarchy (10 min)
**Goal:** tell checked, unchecked, and errors apart.

**Key points**
- `Throwable` is the top. Below it: `Error` and `Exception`.
- `Error` (such as `OutOfMemoryError`) means the JVM is in trouble. Do not catch it.
- `RuntimeException` and its children are unchecked: bugs like `NullPointerException`, `IllegalArgumentException`. The compiler does not force you to handle them.
- Other `Exception`s are checked: `IOException`. The compiler forces you to catch or declare them.
- Rule of thumb: checked for problems the caller can recover from; unchecked for programming mistakes.

**Show:** a tree: `Throwable` → `Error` / `Exception` → `RuntimeException`.

**Check:** Is `NullPointerException` checked? *(No, it is unchecked.)*

---

## BEG-029-L03 · `try`, `catch`, `finally` (10 min)
**Goal:** handle an exception without crashing.

**Key points**
- Put risky code in `try`; the plan goes in `catch`.
- Catch the narrowest useful type, not a bare `Exception`.
- Several catch blocks are checked top to bottom; put specific types first.
- Multi-catch: `catch (A | B e)` when the handling is the same.
- `finally` always runs, whether or not something failed.

**Show**
```java
try {
    int n = Integer.parseInt(text);
} catch (NumberFormatException e) {
    System.out.println("Not a number: " + text);
} finally {
    System.out.println("Done");
}
```

**Check:** When does `finally` run? *(Always, with or without an exception.)*

---

## BEG-029-L04 · Throwing and declaring (8 min)
**Goal:** raise your own exceptions and declare checked ones.

**Key points**
- `throw new IllegalArgumentException("age must be >= 0, was " + age);` raises one.
- A good message says what was wrong and which value caused it.
- A method that may throw a checked exception declares it: `void read() throws IOException`.
- The caller must then catch it or declare it too.
- Do not use exceptions for normal flow, such as ending a loop.

**Show**
```java
void setAge(int age) {
    if (age < 0) throw new IllegalArgumentException("age must be >= 0, was " + age);
    this.age = age;
}
```

**Check:** What does `throws` do? *(Warns callers the method may raise that checked exception.)*

---

## BEG-029-L05 · Custom exceptions (9 min)
**Goal:** write an exception for a business rule.

**Key points**
- Extend `Exception` (checked) or `RuntimeException` (unchecked).
- Name it after the problem and end with `Exception`.
- Give it a message constructor, and a constructor that takes a `cause`.
- Passing the cause keeps the original error; losing it hides the real problem.

**Show**
```java
class InsufficientFundsException extends Exception {
    InsufficientFundsException(String message) { super(message); }
    InsufficientFundsException(String message, Throwable cause) { super(message, cause); }
}
```

**Check:** Why pass the cause? *(So the original error is not lost.)*

---

## BEG-029-L06 · try-with-resources (10 min)
**Goal:** close resources automatically.

**Key points**
- Files and connections must be closed, or they leak.
- Put the resource in the `try (...)` parentheses; Java closes it for you, even on failure.
- It works with anything that implements `AutoCloseable`.
- Several resources close in reverse order.
- It replaces the old, long `finally` + `close()` code.

**Show**
```java
try (BufferedReader r = Files.newBufferedReader(path)) {
    System.out.println(r.readLine());
} catch (IOException e) {
    System.out.println("Could not read: " + e.getMessage());
}
```

**Check:** What interface makes a class usable in try-with-resources? *(`AutoCloseable`.)*

---

## BEG-029-L07 · Demo: InsufficientFundsException end to end (8 min)
**Goal:** define, throw, and handle a custom exception. Prepares `BEG-029-LAB1`.

**Steps**
1. Create `InsufficientFundsException` extending `Exception`.
2. In `Account.withdraw`, throw it when the amount is more than the balance, with a helpful message.
3. Declare `throws InsufficientFundsException` on `withdraw`.
4. **Planned mistake:** call `withdraw` in `main` without handling; the compiler complains. Fix with try/catch.
5. Print the message to the user and keep the balance unchanged.

---

## BEG-029-L08 · Demo: finding a swallowed exception (8 min)
**Goal:** spot and fix an empty catch. Prepares the "swallowed exception" review.

**Steps**
1. Run a program that "does nothing" when a file is missing.
2. Find `catch (Exception e) {}` in the code.
3. **Planned mistake:** add only `e.printStackTrace()` and move on; discuss why a real message and handling is better.
4. Catch the narrow type, give the user a clear message, keep the cause if rethrowing.
5. Rerun and see the problem reported.
