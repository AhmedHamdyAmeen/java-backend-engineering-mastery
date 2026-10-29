# BEG-031 · Generics — Quiz

Outcomes: O1 why generics · O2 generic classes and methods · O3 bounds and wildcards.

**Q01 (O1)** Generics mainly give you: A. Faster code B. Type safety without casts C. Smaller files D. Multithreading
**Q02 (O1)** Without generics, a wrong cast fails: A. At compile time B. At runtime C. Never D. During typing
**Q03 (O1)** `List<String> l = ...; l.add(5);` results in: A. A compile error B. A runtime error C. Works fine D. A warning only
**Q04 (O2)** In `class Box<T>`, `T` is: A. A keyword B. A type placeholder C. An object D. A method
**Q05 (O2)** Which is valid? A. `Box<int>` B. `Box<Integer>` C. `Box<>` as a type D. `Box<5>`
**Q06 (O2)** In a generic method, `<T>` goes: A. After the method name B. In the body C. Before the return type D. After the parameters
**Q07 (O3)** `<T extends Comparable<T>>` lets you call: A. `compareTo` on T B. `new T()` C. `T.class` D. Nothing extra
**Q08 (O3)** `List<? extends Number>` is best described as: A. Add any Number B. Read Numbers, no adding C. Only `Integer`s D. Always empty
**Q09 (O2)** Which line does not compile for a type parameter `T`? A. `T item;` B. `List<T> list;` C. `T[] arr = null;` D. `T x = new T();`
**Q10 (O3)** Is `List<Integer>` a `List<Number>`? A. Yes always B. Only if empty C. Only with raw types D. No

## Answers
Q01 B · Q02 B · Q03 A · Q04 B · Q05 B · Q06 C · Q07 A · Q08 B · Q09 D · Q10 D

## Practical part
Four exercises `BEG-031-EX01` to `EX04` plus the lab. Pass: all four exercises correct and the repository compiles without casts or raw types.
