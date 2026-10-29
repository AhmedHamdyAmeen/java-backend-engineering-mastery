# BEG-012 · Conditions — Exercises and lab

## Lab
### BEG-012-LAB1 · Shipping cost calculator
**Outcomes:** 1–4 · **Time:** ~2 h
1. Write the rules on paper: cost by weight band, extra cost by zone, discount for members.
2. Code the calculator with hard-coded inputs first, then read them with `Scanner`.
3. Flatten any nesting deeper than two levels.
4. Build a test table and work out every expected result by hand before running the code.

**Acceptance:** a table of at least 10 test inputs with expected and actual results, including every weight boundary.

## Exercises (assessment: six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-012-EX01 | 1 | Print "negative", "zero", or "positive" for an int. |
| BEG-012-EX02 | 1 | Map a score to grades A-F with an `else if` chain; test 90, 89, 60, 59. |
| BEG-012-EX03 | 2 | Convert a month number (1-12) to days using a classic `switch` with grouped cases. |
| BEG-012-EX04 | 2 | Rewrite EX03 as a switch expression. Which version do you prefer, and why? |
| BEG-012-EX05 | 3 | Flatten `if (a) { if (b) { if (c) { run(); } } }` once with `&&` and once with early exits. |
| BEG-012-EX06 | 4 | Find the problem in `if (x > 5) {...} else if (x > 10) {...}` and in a chain that tests `x >= 0` then `x > 100`. |

## Solutions
- **EX01** `if (n < 0) ... else if (n == 0) ... else ...`.
- **EX02** Order from highest: `>= 90`, `>= 80`, and so on. 90 gives A, 89 gives B, 60 gives D, 59 gives F.
- **EX03** `case 4: case 6: case 9: case 11: days = 30; break;` and so on; February is 28 (or 29), `default` for the rest.
- **EX04** `int days = switch (m) { case 4, 6, 9, 11 -> 30; case 2 -> 28; default -> 31; };` Preference is open; the arrow form is shorter and has no fall-through.
- **EX05** `if (a && b && c) run();` or `if (!a) return; if (!b) return; if (!c) return; run();`.
- **EX06** `x > 10` can never be reached: any x above 10 is already caught by `x > 5` (unreachable branch). In the second chain every x above 100 also satisfies `x >= 0`, so the second test is never reached for the values it was meant for.
- Outcome 4 is also covered by quiz Q09 and Q10 and by the lab test table.
