# BEG-037 · Optional — Quiz

Outcomes: O1 returning Optional · O2 transforming and unwrapping · O3 where not to use it.

**Q01 (O1)** `Optional<T>` is best used as: A. A field type B. A method parameter C. A return type when a result may be missing D. A collection replacement
**Q02 (O1)** Which creates an empty Optional? A. `Optional.empty()` B. `Optional.of(null)` C. `new Optional()` D. `null`
**Q03 (O1)** `Optional.of(null)` will: A. Return empty B. Throw `NullPointerException` C. Return `null` D. Compile-fail
**Q04 (O2)** `opt.orElse("x")` returns: A. Always "x" B. The value, or "x" if empty C. An `Optional` D. Nothing
**Q05 (O2)** Which computes its default only when needed? A. `orElse` B. `get` C. `orElseGet` D. `isPresent`
**Q06 (O2)** To throw your own exception when empty: A. `orElseThrow(...)` B. `orElse(null)` C. `get()` D. `filter(...)`
**Q07 (O2)** `opt.map(String::length)` returns: A. `int` B. `String` C. `void` D. `Optional<Integer>`
**Q08 (O3)** Calling `get()` on an empty Optional: A. Returns null B. Returns "" C. Throws `NoSuchElementException` D. Returns 0
**Q09 (O3)** A method that finds no orders should return: A. `Optional<List<Order>>` B. An empty `List` C. `null` D. `Optional.empty()` of a list
**Q10 (O3)** Which is an anti-pattern? A. Optional return value B. `map(...).orElse(...)` C. `orElseThrow` D. An `Optional` field in a class

## Answers
Q01 C · Q02 A · Q03 B · Q04 B · Q05 C · Q06 A · Q07 D · Q08 C · Q09 B · Q10 D

## Practical part
Three exercises `BEG-037-EX01` to `EX03` plus the lab. Pass: all three exercises correct and the lab has no unchecked `.get()`.
