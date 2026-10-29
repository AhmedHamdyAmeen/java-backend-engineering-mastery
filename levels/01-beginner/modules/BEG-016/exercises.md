# BEG-016 · Problem-solving — Exercises and lab

## Lab
### BEG-016-LAB1 · Plan before code
**Outcomes:** 1–4 · **Time:** ~3 h
For each of three unseen problems (supplied by the instructor, for example: second largest value, palindrome check, count vowels):
1. Restate the problem and list inputs, outputs, constraints.
2. Write pseudocode or a flowchart.
3. List edge cases with expected results.
4. Hand-trace one example with a variable table.
5. Only then write the Java code and submit the plan with it.

**Acceptance:** plan and code match; all listed edge cases handled.

## Exercises (assessment: one unseen problem solved with a plan, graded on the plan as much as the code)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-016-EX01 | 1 | Restate "give each customer a loyalty discount" and list inputs, outputs, and three questions to ask. |
| BEG-016-EX02 | 2 | Decompose "print a report of the highest-scoring student" into 5 steps. |
| BEG-016-EX03 | 2 | Write pseudocode for "is a number prime?" and draw its flowchart. |
| BEG-016-EX04 | 3 | Trace `int x = 10; int c = 0; while (x > 1) { x = x / 2; c++; }` with a variable table. |
| BEG-016-EX05 | 4 | List at least six edge cases for "average of an array of grades". |

## Solutions
- **EX01** Inputs: customer data, purchase history. Output: discount percent. Questions: what makes a customer loyal? maximum discount? can discounts stack?
- **EX02** 1 read the scores; 2 start the best at the first student; 3 compare each other student; 4 update the best; 5 print the name and score.
- **EX03** If n < 2 not prime; for d from 2 up to the square root of n, if n % d == 0 then not prime; otherwise prime. The flowchart has one decision diamond for each test.
- **EX04** Rows: x 10, c 0 → x 5, c 1 → x 2, c 2 → x 1, c 3; the loop ends. Final c is 3.
- **EX05** Empty array; one grade; all equal; zero grades; negative or above 100 (invalid); very large array; decimals.
- Lab acceptance and the graded unseen problem cover the full routine (outcomes 1-4 together).
