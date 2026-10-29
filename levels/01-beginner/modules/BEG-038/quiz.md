# BEG-038 · Java memory basics — Quiz (diagram quiz)

Outcomes: O1 stack and heap · O2 references and aliasing · O3 garbage collection.

**Q01 (O1)** Local variables of a running method live in: A. The heap B. A stack frame C. A file D. The class
**Q02 (O1)** Objects created with `new` live: A. In the stack frame B. In a constant C. On the heap D. In the compiler
**Q03 (O1)** When a method returns, its stack frame: A. Stays forever B. Moves to the heap C. Is saved to disk D. Is removed
**Q04 (O2)** `int a = 5; int b = a; b = 9;` then `a` is: A. 9 B. 14 C. 0 D. 5
**Q05 (O2)** `List<String> a = new ArrayList<>(); List<String> b = a; b.add("x");` then `a.size()` is: A. 0 B. 1 C. 2 D. Error
**Q06 (O2)** `b = a` for object variables copies: A. The object B. The reference C. Both D. Nothing
**Q07 (O2)** `==` on two object variables compares: A. Content B. Length C. Names D. References
**Q08 (O3)** An object is eligible for GC when: A. It is old B. It is large C. It is unreachable D. `null` is printed
**Q09 (O3)** `System.gc()`: A. Frees memory immediately B. Is only a hint C. Is required D. Deletes variables
**Q10 (O1)** Infinite recursion causes: A. `OutOfMemoryError` B. `NullPointerException` C. `ArithmeticException` D. `StackOverflowError`

## Answers
Q01 B · Q02 C · Q03 D · Q04 D · Q05 B · Q06 B · Q07 D · Q08 C · Q09 B · Q10 D

## Practical part
Five exercises `BEG-038-EX01` to `EX05` plus the lab diagrams. Pass: at least four exercises correct and all four lab diagrams matching the debugger.
