# BEG-029 · Exceptions — Exercises and lab

## Lab
### BEG-029-LAB1 · Bank with rules
**Outcomes:** 1–5 · **Time:** ~2 h
Build an `Account` with `deposit` and `withdraw`. Overdrawing throws `InsufficientFundsException`. A console loop reads amounts as text and retries when `NumberFormatException` occurs. Read one small file using try-with-resources.
**Acceptance:** no empty catch blocks; messages helpful to the user.

## Exercises (assessment: five exercises plus a "fix the swallowed exception" review)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-029-EX01 | 1 | Classify as checked, unchecked, or error: `IOException`, `NullPointerException`, `OutOfMemoryError`, `IllegalArgumentException`. |
| BEG-029-EX02 | 2 | Write code that parses a string to `int` and prints a friendly message on failure, plus a `finally` that prints "done". |
| BEG-029-EX03 | 2 | Rewrite two identical catch blocks for `NumberFormatException` and `ArithmeticException` as one multi-catch. |
| BEG-029-EX04 | 3, 4 | Write `OutOfStockException` (with a cause constructor) and a method that throws it with a message naming the item and quantity. |
| BEG-029-EX05 | 5 | Rewrite a `BufferedReader` read with manual `finally { close(); }` as try-with-resources. |
| BEG-029-EX06 | 2 | Review: fix `try { load(); } catch (Exception e) {}` so the error is not swallowed. |

## Solutions
- **EX01** Checked, unchecked, error, unchecked.
- **EX02** `try { int n = Integer.parseInt(s); } catch (NumberFormatException e) { System.out.println("'" + s + "' is not a whole number."); } finally { System.out.println("done"); }`
- **EX03** `catch (NumberFormatException | ArithmeticException e) { ... }`.
- **EX04** `class OutOfStockException extends Exception { OutOfStockException(String m){super(m);} OutOfStockException(String m, Throwable c){super(m,c);} }` then `throw new OutOfStockException("Only 2 of 'pen' left, requested 5");`
- **EX05** `try (BufferedReader r = Files.newBufferedReader(p)) { ... } catch (IOException e) { ... }`.
- **EX06** Catch the narrow type (for example `IOException`), print a clear message, and either recover or rethrow `new IllegalStateException("Could not load data", e)`.
- Outcome 1 is also covered by quiz Q01–Q03; outcome 3 is also covered by the lab.
