# BEG-009 · Variables and data types — Exercises and lab

## Lab
### BEG-009-LAB1 · Unit converter (fixed values)
**Outcomes:** 1–5 · **Time:** ~2 h
Convert hard-coded temperatures, distances, and currencies and print the results with the correct types. Include one deliberate overflow and explain it in a comment.
**Acceptance:** correct output; the overflow is explained.

## Exercises (assessment: six exercises plus the type-selection quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-009-EX01 | 1 | Declare one variable of each type for: age, price in cents, temperature, first initial, is-student, full name. |
| BEG-009-EX02 | 2 | Explain in two sentences the difference between `int` and `String` in how they hold data. |
| BEG-009-EX03 | 3 | Rename these to Java style: `Total_Price`, `maxspeed`, a constant for 3.14159. |
| BEG-009-EX04 | 4 | Predict, then run: `7 / 2`, `7 / 2.0`, `(int) 9.99`, `(double) 7 / 2`. |
| BEG-009-EX05 | 4 | Predict the result of `Integer.MAX_VALUE + 1`, then run it and explain. |
| BEG-009-EX06 | 5 | Rewrite three declarations with `var` where the type is obvious; leave one that should not use it. |

## Solutions
- **EX01** `int age`; `int priceCents`; `double temperature`; `char initial`; `boolean isStudent`; `String fullName`.
- **EX02** `int` holds the value directly; `String` holds a reference to a text object elsewhere.
- **EX03** `totalPrice`, `maxSpeed`, `final double PI = 3.14159;`.
- **EX04** `3`, `3.5`, `9`, `3.5`.
- **EX05** `-2147483648`: the value wraps past the maximum of `int`.
- **EX06** For example `var count = 10;` and `var name = "Ana";`; avoid `var x = compute();`.
