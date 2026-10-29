# BEG-036 · Stream API — Quiz

Outcomes: O1 intermediate operations · O2 terminal operations · O3 grouping and collectors · O4 streams vs loops.

**Q01 (O1)** Which keeps only matching items? A. `map` B. `sorted` C. `filter` D. `limit`
**Q02 (O1)** Which transforms each item into another value? A. `filter` B. `map` C. `distinct` D. `count`
**Q03 (O1)** `flatMap` is used to: A. Flatten nested collections into one stream B. Sort C. Count D. Reverse
**Q04 (O2)** A pipeline with no terminal operation: A. Runs everything B. Fails to compile C. Throws at runtime D. Does nothing
**Q05 (O2)** `findFirst()` returns: A. The item B. `null` if empty C. An `Optional` D. A list
**Q06 (O2)** Which combines all items into one value? A. `reduce` B. `filter` C. `distinct` D. `skip`
**Q07 (O3)** `Collectors.groupingBy(Person::getCity)` returns: A. A `List` B. A `Set` C. A single number D. A `Map` from city to list of people
**Q08 (O3)** To count items per group, use as downstream: A. `Collectors.joining()` B. `Collectors.counting()` C. `Collectors.toSet()` D. `distinct()`
**Q09 (O1)** Using a stream a second time after a terminal operation: A. Works B. Returns an empty list C. Throws `IllegalStateException` D. Restarts it
**Q10 (O4)** A loop is usually clearer when: A. You need a one-line filter B. You group data C. You want fewer lines always D. You need many steps, state changes, or early exit

## Answers
Q01 C · Q02 B · Q03 A · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Six exercises `BEG-036-EX01` to `EX06` plus the lab. Pass: at least five exercises correct, EX06 justified, and all lab results correct.
