# BEG-013 · Loops — Exercises and lab

## Lab
### BEG-013-LAB1 · Number guessing game (mini-project 1 of 3)
**Outcomes:** 1–4 · **Time:** ~3 h
1. Pick a random target between 1 and 100.
2. Allow a limited number of attempts (for example 7); give higher/lower hints.
3. Reject input that is not a number or is out of range without losing an attempt.
4. Report the number of attempts used at the end.
5. Ask "play again?" and replay without restarting the program.
6. Step through one game in the debugger.

**Acceptance:** handles invalid input, reports attempts, replay works.

## Exercises (assessment: seven exercises plus the guessing game)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-013-EX01 | 1 | For each task pick `for`, `while`, or `do-while` and justify: print 1-10; read until "quit"; a menu shown at least once. |
| BEG-013-EX02 | 2 | Print the sum of 1 to 100 with a `for` loop. |
| BEG-013-EX03 | 2 | This loop never ends. Fix it: `int i = 0; while (i < 10) { System.out.println(i); }` |
| BEG-013-EX04 | 2 | Print the numbers 10 down to 1 with no off-by-one error. |
| BEG-013-EX05 | 3 | Print 1-20, skipping multiples of 3 and stopping at the first number above 15. |
| BEG-013-EX06 | 4 | Print a 5-row triangle of stars. |
| BEG-013-EX07 | 4 | Print the multiplication table 1-9 and state how many times the body runs. |

## Solutions
- **EX01** `for` (known count); `while` (unknown count, may run zero times); `do-while` (at least once).
- **EX02** `int sum = 0; for (int i = 1; i <= 100; i++) sum += i;` result 5050.
- **EX03** Add `i++;` inside the body.
- **EX04** `for (int i = 10; i >= 1; i--)`.
- **EX05** `for (int i = 1; i <= 20; i++) { if (i > 15) break; if (i % 3 == 0) continue; System.out.println(i); }`
- **EX06** `for (int r = 1; r <= 5; r++) { for (int c = 1; c <= r; c++) System.out.print("*"); System.out.println(); }`
- **EX07** Nested loops 1..9 by 1..9; the body runs 81 times.
- The guessing game and quiz also cover outcomes 2 and 3 further.
