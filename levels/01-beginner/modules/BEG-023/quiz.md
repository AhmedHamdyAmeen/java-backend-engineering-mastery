# BEG-023 · Polymorphism — Quiz (predict the output)

Outcomes: O1 dynamic dispatch · O2 uniform treatment through a parent type · O3 replacing type checks.
Setup for Q01-Q06: `class A { String who() { return "A"; } }`, `class B extends A { @Override String who() { return "B"; } }`.

**Q01 (O1)** `A x = new B(); System.out.println(x.who());` prints: A. A B. B C. Compile error D. Runtime error
**Q02 (O1)** `A x = new A(); System.out.println(x.who());` prints: A. Runtime error B. B C. Compile error D. A
**Q03 (O1)** `B y = (B) new A();` results in: A. `ClassCastException` B. Compile error C. Works fine D. Prints A
**Q04 (O1)** Which is resolved at run time? A. Overloading B. Variable names C. Overriding D. Imports
**Q05 (O2)** `List<A> list = List.of(new A(), new B());` then a loop calling `who()` prints: A. A then A B. A then B C. B then B D. Compile error
**Q06 (O2)** Upcasting `A x = new B();` is: A. Automatic and safe B. Always an error C. Needs `(A)` D. Runtime-checked
**Q07 (O2)** Through a parent reference you can call: A. Any child method B. Nothing C. Only private methods D. Only methods the parent declares
**Q08 (O3)** The best fix for repeated `if (x instanceof ...)` chains is: A. More casts B. A bigger `switch` C. Overriding methods in each subclass D. Public fields
**Q09 (O3)** After the refactor, adding a new account type needs: A. A new subclass only B. Edits in every loop C. Deleting classes D. A new JVM
**Q10 (O1)** Downcasting safely requires: A. `final` B. `instanceof` check C. `static` D. Nothing

## Answers
Q01 B · Q02 D · Q03 A · Q04 C · Q05 B · Q06 A · Q07 D · Q08 C · Q09 A · Q10 B

## Practical part
The eight "predict the output" snippets are Q01-Q06 above plus the two below, exercises `BEG-023-EX01` to `EX06`, and the month-end lab. Pass: at least six of eight snippets correct and the lab acceptance met.

**Snippet 7** (same `A` and `B` as above, plus `class C extends B {}`): `A x = new C(); System.out.println(x.who());` prints: A. A B. B C. C D. Compile error. *(Answer: B. `C` inherits `B`'s override, so dynamic dispatch picks `B.who()`.)*

**Snippet 8** (same `A` and `B`): `A[] items = { new B(), new A(), new B() }; String s = ""; for (A a : items) s += a.who(); System.out.println(s);` prints: A. AAA B. BAB C. BBB D. ABA. *(Answer: B. Each element's real type decides which `who()` runs.)*
