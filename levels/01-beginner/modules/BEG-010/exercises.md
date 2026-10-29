# BEG-010 · Operators — Exercises and lab

## Lab
### BEG-010-LAB1 · Expression predictor
**Outcomes:** 1–4 · **Time:** ~3 h
Predict the output of the 20 expressions below on paper, then run them in code. Record each prediction before running and explain each mismatch.

1. `7 / 2` 2. `7 % 2` 3. `-7 / 2` 4. `7 / 2.0` 5. `10 % 3 + 1` 6. `2 + 3 * 4` 7. `(2 + 3) * 4` 8. `5 > 3` 9. `5 == 5.0` 10. `!(3 > 5)`
11. `true && false` 12. `true || false && false` 13. `int x = 5; x += 3;` (x) 14. `int x = 5; x *= 2 + 1;` (x) 15. `int i = 3; i++;` (i)
16. `int i = 3; int j = i++;` (i, j) 17. `int i = 3; int j = ++i;` (i, j) 18. `int d = 0; d != 0 && 10 / d > 1` 19. `1 + 2 + "3"` 20. `"1" + 2 + 3`

**Acceptance:** predictions recorded before running; each mismatch explained.

## Exercises (assessment: six)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-010-EX01 | 1 | Write an expression that is true when `n` is even. |
| BEG-010-EX02 | 1 | Write an expression for "year is a leap year": divisible by 4 and (not by 100 or divisible by 400). |
| BEG-010-EX03 | 2 | Compute the average of the ints 7 and 8 as a decimal; first get it wrong, then fix it. |
| BEG-010-EX04 | 2 | Convert 135 minutes into hours and remaining minutes using `/` and `%`. |
| BEG-010-EX05 | 3 | Predict the final values of `a` and `b`: `int a = 2; int b = a++ + ++a;` |
| BEG-010-EX06 | 4 | Rewrite `10 / d > 1 && d != 0` so it can never divide by zero. |

## Solutions
- **Lab:** 1: 3 · 2: 1 · 3: -3 · 4: 3.5 · 5: 2 · 6: 14 · 7: 20 · 8: true · 9: true · 10: true · 11: false · 12: true · 13: 8 · 14: 15 · 15: 4 · 16: i=4, j=3 · 17: i=4, j=4 · 18: false (no crash) · 19: `33` · 20: `123`.
- **EX01** `n % 2 == 0`.
- **EX02** `(y % 4 == 0) && (y % 100 != 0 || y % 400 == 0)`.
- **EX03** `(7 + 8) / 2` gives 7; fix: `(7 + 8) / 2.0` gives 7.5.
- **EX04** `135 / 60` is 2 hours; `135 % 60` is 15 minutes.
- **EX05** `a++` yields 2 (a becomes 3); `++a` makes a 4 and yields 4; `b` is 6, `a` is 4.
- **EX06** `d != 0 && 10 / d > 1`.
