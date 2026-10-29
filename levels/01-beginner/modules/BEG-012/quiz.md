# BEG-012 · Conditions — Quiz

Outcomes: O1 if chains · O2 choosing if/switch · O3 simplifying · O4 unreachable/overlap.

**Q01 (O1)** The condition inside `if (...)` must be: A. An int B. A String C. A boolean D. A char
**Q02 (O1)** In an `else if` chain, Java runs: A. Every true branch B. Only the first true branch C. Only the last true branch D. A random one
**Q03 (O1)** For `if (n >= 10)`, which values are the boundary to test? A. 9 and 10 B. 0 C. 100 D. -10
**Q04 (O2)** Which fits a `switch` best? A. Score ranges B. One day number with seven fixed choices C. Two doubles compared D. A complex `&&` test
**Q05 (O2)** A missing `break` in a classic switch causes: A. A compile error B. Fall-through into the next case C. The switch to stop D. Nothing
**Q06 (O2)** In `case 6, 7 -> "Weekend"` the arrow form: A. Falls through B. Needs `break` C. Does not fall through D. Is only for Strings
**Q07 (O3)** `if (a) { if (b) { run(); } }` equals: A. `if (a || b)` B. `if (a && b)` C. `if (a == b)` D. `if (!a && b)`
**Q08 (O3)** An early exit helps because it: A. Makes the program faster B. Removes a level of nesting C. Skips compile checks D. Avoids variables
**Q09 (O4)** In `if (x > 5) {...} else if (x > 10) {...}` the second branch is: A. Always run B. Never reached C. Reached for x = 7 D. A syntax error
**Q10 (O4)** Two branches that can both be true for the same value are: A. Overlapping B. Unreachable C. Final D. Constant

## Answers
Q01 C · Q02 B · Q03 A · Q04 B · Q05 B · Q06 C · Q07 B · Q08 B · Q09 B · Q10 A

## Practical part
Six exercises `BEG-012-EX01` to `EX06` plus the shipping lab with its test table. Pass: at least five exercises correct and the test table covering all boundaries.
