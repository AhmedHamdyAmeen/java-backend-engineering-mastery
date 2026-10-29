# BEG-011 · Input and output — Exercises and lab

## Lab
### BEG-011-LAB1 · Receipt printer
**Outcomes:** 1–4 · **Time:** ~3 h
Read item names, quantities, and prices. Print an aligned receipt with line totals, subtotal, and tax. Reject invalid quantities (not a whole number, or less than 1) by asking again.

Example output:
```
Item        Qty    Price     Total
Pen           2     1.50      3.00
Notebook      1     4.25      4.25
Subtotal                      7.25
Tax (15%)                     1.09
Total                         8.34
```
**Acceptance:** columns aligned; invalid input re-prompted.

## Exercises (assessment: five)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-011-EX01 | 1 | Ask for a name and an age; print `Ana is 30 years old.` |
| BEG-011-EX02 | 1 | Ask for age and then full name, and make both work correctly (the trap). |
| BEG-011-EX03 | 2 | Read a decimal number as text and double it with `Double.parseDouble`. |
| BEG-011-EX04 | 2 | Keep asking for a whole number until the user enters one between 1 and 10. |
| BEG-011-EX05 | 3 | Print three products and prices in aligned columns with two decimals. |

## Solutions
- **EX01** `in.nextLine()` for name, `in.nextInt()` for age, then `printf("%s is %d years old.%n", name, age)`.
- **EX02** Add `in.nextLine();` after `nextInt()` before reading the name.
- **EX03** `double d = Double.parseDouble(in.nextLine()); System.out.println(d * 2);`
- **EX04** Loop with `hasNextInt()`, discard bad input with `in.next()`, and check `n >= 1 && n <= 10`.
- **EX05** `printf("%-12s %8.2f%n", name, price)`.

**Outcome 4** is checked by the quiz (Q09, Q10) and by lab criterion "invalid input re-prompted".
