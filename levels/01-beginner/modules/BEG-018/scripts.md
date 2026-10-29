# BEG-018 · Debugging — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a detective solving a case: gather clues, form a theory, test it, then close the case.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-018-L01 · A method for debugging (8 min)
**Goal:** follow a calm, repeatable process instead of guessing.

**Key points**
- A bug is a gap between what you expected and what happened.
- Process: reproduce, isolate, hypothesize, test, fix, verify.
- Reproduce: make the bug happen every time with known input.
- Isolate: shrink to the smallest code and input that still fails.
- Change one thing at a time; fix the cause, not the symptom.

**Show**
Case: `average([2, 4, 6])` prints 4.0 but `average([1, 2])` prints 1.0. Reproduce with `[1, 2]`. Hypothesis: integer division. Test: print the sum and count. Fix: divide as `double`. Verify both cases.

**Check:** Name the six steps. *(Reproduce, isolate, hypothesize, test, fix, verify.)*

---

## BEG-018-L02 · Breakpoints and stepping (12 min)
**Goal:** pause a running program and move through it line by line in IntelliJ.

**Key points**
- A breakpoint (click in the left margin) pauses the program before that line.
- Run with the Debug button, not Run.
- Step over (F8) runs the line and moves on.
- Step into (F7) goes inside the method being called; step out (Shift+F8) leaves it.
- A conditional breakpoint (right-click it) pauses only when a condition is true, such as `i == 99`.
- Verify the shortcut keys for your IntelliJ keymap before recording.

**Show:** a screenshot description: breakpoint dot on `total += price;`, debugger paused, toolbar with over/into/out, Resume button.

**Check:** What is the difference between step over and step into? *(Over runs the call as one step; into enters the method.)*

---

## BEG-018-L03 · Variables, watches, and evaluate expression (8 min)
**Goal:** look at the program's state while it is paused.

**Key points**
- The Variables panel shows current values of locals and parameters.
- A watch keeps one expression in view, such as `sum / count`.
- Evaluate Expression runs a small expression on the spot.
- Compare each value with what you expected; the first surprise is your clue.
- Do not change code while paused to "see if it works"; form a hypothesis first.

**Show:** pause inside a loop; the Variables panel shows `i = 3`, `sum = 6`; add a watch `sum / (double) count`.

**Check:** What do you do with a value that surprises you? *(Treat it as a clue and form a hypothesis about where it went wrong.)*

---

## BEG-018-L04 · Reading stack traces (10 min)
**Goal:** read an exception message and jump to the failing line.

**Key points**
- The first line says the exception type and message.
- The lines below are the call stack, newest call first.
- Find the first line that points to your own code (`MyClass.java:12`); click it.
- Read the message literally: `Index 5 out of bounds for length 5`.
- Later lines show how you got there.

**Show**
```text
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
    at Report.total(Report.java:14)
    at Main.main(Main.java:6)
```
The failing line is `Report.java:14`.

**Check:** Which line of the trace do you open first? *(The first line that points to your own code.)*

---

## BEG-018-L05 · A catalog of common runtime errors (7 min)
**Goal:** recognize the usual suspects by name.

**Key points**
- `NullPointerException`: using a reference that points to nothing.
- `ArrayIndexOutOfBoundsException` / `StringIndexOutOfBoundsException`: bad index.
- `ArithmeticException`: division by zero with integers.
- `NumberFormatException`: parsing text such as "abc" as a number.
- `StackOverflowError`: recursion with no end; `InputMismatchException`: wrong kind of `Scanner` input.

**Show:** a table of error name, typical cause, first thing to check.

**Check:** Which exception comes from `Integer.parseInt("abc")`? *(`NumberFormatException`.)*

---

## BEG-018-L06 · Demo: a full bug hunt from report to fix (8 min)
**Goal:** apply the whole method to one bug. Prepares `BEG-018-LAB1`.

**Steps**
1. Read the bug report: "the grade average is wrong when a student has a 0."
2. Reproduce with a small input and write down expected and actual.
3. Place a breakpoint at the loop; watch `sum` and `count` on each pass.
4. **Planned mistake:** change the formula at random; it fixes one case and breaks another. Undo and go back to the hypothesis.
5. The debugger shows `if (grade > 0)` skips zero; hypothesize that it should be `>= 0`, test, fix.
6. Verify the original case and two other inputs; write the case notes.

**Check:** Why undo the random change? *(It was a guess; changes should test a hypothesis.)*
