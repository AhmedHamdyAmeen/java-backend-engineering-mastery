# BEG-032 · Sorting and comparison — Quiz

Outcomes: O1 Comparable · O2 Comparator · O3 sorting and sorted collections.

**Q01 (O1)** `Comparable<T>` requires which method? A. `compare` B. `sort` C. `equals` D. `compareTo`
**Q02 (O1)** `compareTo` returns a positive number when: A. This comes after the other B. They are equal C. This comes first D. It is null
**Q03 (O1)** A safe way to compare two `int`s: A. `a - b` B. `Integer.compare(a, b)` C. `a == b` D. `a.equals(b)`
**Q04 (O2)** `Comparator.comparing(Player::getName)` sorts by: A. Score B. Insertion order C. Name D. Hash code
**Q05 (O2)** To reverse a comparator: A. `.reverse()` B. `.flip()` C. `.negate()` D. `.reversed()`
**Q06 (O2)** Use a `Comparator` rather than `Comparable` when: A. You need several different orders B. You want fewer lines C. You use a `HashMap` D. Never
**Q07 (O3)** `thenComparing` is used to: A. Remove duplicates B. Break ties with another key C. Sort twice D. Reverse
**Q08 (O3)** Two elements with `compare` result 0 in a `TreeSet`: A. Both are kept B. An error is thrown C. Only one is kept D. They swap places
**Q09 (O1)** Why is `return a - b;` risky? A. It is slower B. It can overflow C. It does not compile D. It sorts backwards
**Q10 (O3)** `list.sort(null)` or `Collections.sort(list)` uses: A. Hash order B. A random order C. Insertion order D. The natural order (`Comparable`)

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 D

## Practical part
Three exercises `BEG-032-EX01` to `EX03` plus the lab. Pass: all three exercises correct and tied scores ordered by name in the lab.
