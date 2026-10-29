# BEG-018 · Debugging — Exercises and lab

## Lab
### BEG-018-LAB1 · Bug hunt
**Outcomes:** 1–4 · **Time:** ~2 h
You receive five small programs, each with one logic bug. For each, write a trail:
1. Reproduction steps (input, expected, actual).
2. Your hypothesis.
3. The line found with the debugger (breakpoint, stepping, watches).
4. The fix and how you verified it.

**Acceptance:** all five fixed with a written trail.

## Exercises (assessment: live debugging demonstration, also part of the BEG graduation gate)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-018-EX01 | 1 | Set a conditional breakpoint that stops only on iteration 50 of a 100-iteration loop, then step into, over, and out of a method call. |
| BEG-018-EX02 | 2 | Using watches, find where `sum` first differs from your hand-traced value in a given program. |
| BEG-018-EX03 | 3 | Read a provided stack trace: name the exception, the failing line, and the calling method. |
| BEG-018-EX04 | 4 | Write the six-step debugging process and apply it to "average prints the wrong value for `[1, 2]`". |
| BEG-018-EX05 | 3 | Match three exceptions (`NullPointerException`, `NumberFormatException`, `ArithmeticException`) to code that causes each. |

## Solutions
- **EX01** Right-click the breakpoint, enter `i == 49` (or `i == 50` depending on the loop start); use F8, F7, Shift+F8.
- **EX02** Add a watch for `sum`; compare it with your trace table on each pass; the first mismatch is the clue.
- **EX03** Read the first line for type and message, then the first line with your own class and its line number.
- **EX04** Reproduce with `[1, 2]`; isolate the average method; hypothesis integer division; test with a debugger watch; fix with `(double) sum / count`; verify with `[1, 2]` and `[2, 4, 6]`.
- **EX05** `String s = null; s.length()`; `Integer.parseInt("abc")`; `5 / 0`.
- Outcome 4 is also assessed by the live debugging demonstration and the lab written trails.
