# BEG-014 · Methods — Quiz

Outcomes: O1 extract methods · O2 pass-by-value · O3 overloading · O4 call stack · O5 recursion.

**Q01 (O1)** A method that returns nothing has return type: A. `null` B. `void` C. `empty` D. `int`
**Q02 (O1)** A good method usually: A. Does one clear job B. Computes and prints everything C. Has no name D. Is very long
**Q03 (O2)** A method changes its `int` parameter. The caller's variable: A. Changes too B. Stays the same C. Becomes 0 D. Causes an error
**Q04 (O2)** Java passes arguments: A. By reference only B. By value (a copy) C. By name D. By pointer arithmetic
**Q05 (O3)** Overloaded methods must differ in: A. Return type only B. Parameter list C. Method body D. Access modifier only
**Q06 (O3)** `max(2.5, 1.0)` with `max(int,int)` and `max(double,double)` calls: A. The int one B. The double one C. Neither D. Both
**Q07 (O4)** The call stack holds: A. Source files B. One frame per active method call C. Only `main` D. All variables forever
**Q08 (O4)** When a method returns, its frame is: A. Kept B. Removed C. Copied D. Printed
**Q09 (O5)** A recursive method needs: A. A base case B. A loop C. No parameters D. A `static` field
**Q10 (O5)** Recursion without a base case ends in: A. `NullPointerException` B. `StackOverflowError` C. A compile error D. A normal result

## Answers
Q01 B · Q02 A · Q03 B · Q04 B · Q05 B · Q06 B · Q07 B · Q08 B · Q09 A · Q10 B

## Practical part
Six exercises `BEG-014-EX01` to `EX06` plus the command-line calculator. Pass: at least five exercises correct and a calculator with no duplicated logic, handled division by zero, and a recursive factorial with a base case.
