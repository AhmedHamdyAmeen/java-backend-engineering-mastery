# BEG-014 · Methods — Exercises and lab

## Lab
### BEG-014-LAB1 · Command-line calculator (mini-project 2 of 3)
**Outcomes:** 1–5 · **Time:** ~3 h
1. Build a menu-driven calculator: add, subtract, multiply, divide, power, factorial, quit.
2. Write each operation as its own method that returns a result and does not print.
3. Make `power` iterative and `factorial` recursive.
4. Handle division by zero and negative factorial input.
5. Keep reading input and printing in separate methods from the math.

**Acceptance:** no duplicated logic; division by zero handled; recursion has a base case.

## Exercises (assessment: six exercises plus the calculator)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-014-EX01 | 1 | Extract the repeated "area of a rectangle" code from a given program into `area(w, h)`. |
| BEG-014-EX02 | 2 | Predict the output: a method does `x = x * 2` on a parameter; the caller prints its own variable afterwards. Explain. |
| BEG-014-EX03 | 3 | Write overloaded `print(int)`, `print(String)`, `print(int, int)`. Which is called for `print("a")`? |
| BEG-014-EX04 | 4 | Draw the call stack at the deepest point of `a()` calling `b()` calling `c()`. |
| BEG-014-EX05 | 5 | Write a recursive `sumOfDigits(int n)`. |
| BEG-014-EX06 | 5 | Write recursive `factorial(n)` and say what happens without the base case. |

## Solutions
- **EX01** `static double area(double w, double h) { return w * h; }`, called wherever the code was repeated.
- **EX02** The caller's variable is unchanged; Java passes a copy of the value. (For an object reference the copy points to the same object.)
- **EX03** `print("a")` matches the `String` version; Java picks the signature matching the argument types.
- **EX04** Bottom to top: `main`, `a`, `b`, `c` (top, running).
- **EX05** `if (n < 10) return n; return n % 10 + sumOfDigits(n / 10);` Example: 123 gives 6.
- **EX06** `if (n <= 1) return 1; return n * factorial(n - 1);` Without the base case it recurses forever and ends in `StackOverflowError`.
- Outcome 1's "clear parameters and return type" and the pass-by-value of references are also checked in the quiz and the calculator.
