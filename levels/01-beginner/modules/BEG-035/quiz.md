# BEG-035 · Functional basics — Quiz

Outcomes: O1 lambdas and functional interfaces · O2 standard interfaces · O3 method references.

**Q01 (O1)** A functional interface has: A. No methods B. Exactly one abstract method C. Only static methods D. Two abstract methods
**Q02 (O1)** `(a, b) -> a + b` is a: A. Lambda expression B. Class C. Package D. Loop
**Q03 (O1)** A lambda can use a local variable from outside if it is: A. Static B. Public C. Effectively final D. Volatile
**Q04 (O2)** Takes a value, returns `boolean`: A. `Function` B. `Predicate` C. `Consumer` D. `Supplier`
**Q05 (O2)** Takes nothing, returns a value: A. `Consumer` B. `Predicate` C. `BiFunction` D. `Supplier`
**Q06 (O2)** Takes a value, returns nothing: A. `Consumer` B. `Supplier` C. `Predicate` D. `Function`
**Q07 (O2)** Method name of `Function`: A. `get` B. `test` C. `accept` D. `apply`
**Q08 (O3)** `String::length` is equal to: A. `s -> s.length()` B. `() -> length()` C. `s -> length` D. `String.length()`
**Q09 (O3)** `System.out::println` is a reference to: A. A static method B. A constructor C. A method of a specific object D. A field
**Q10 (O1)** If a lambda body needs ten lines, you should: A. Keep it B. Move it to a named method C. Use a longer name D. Remove the braces

## Answers
Q01 B · Q02 A · Q03 C · Q04 B · Q05 D · Q06 A · Q07 D · Q08 A · Q09 C · Q10 B

## Practical part
Four exercises `BEG-035-EX01` to `EX04` plus the lab. Pass: all four exercises correct and the lab behaving the same as before with less code.
