# BEG-039 · Algorithms and complexity — Quiz (complexity)

Outcomes: O1 express Big O · O2 time vs space, best/average/worst · O3 compare solutions.

**Q01 (O1)** `int x = arr[10];` is: A. O(n) B. O(log n) C. O(n²) D. O(1)
**Q02 (O1)** A single `for` loop from 0 to `n` doing constant work is: A. O(1) B. O(n) C. O(n²) D. O(log n)
**Q03 (O1)** Two nested loops, each over `n`: A. O(n) B. O(2n) C. O(n²) D. O(log n)
**Q04 (O1)** `for (int i = 1; i < n; i *= 2)` is: A. O(n) B. O(n²) C. O(1) D. O(log n)
**Q05 (O1)** `3n² + 5n + 9` simplifies to: A. O(n) B. O(n²) C. O(3n²) D. O(n³)
**Q06 (O1)** A loop over a `List` of `n` items calling `list.contains(x)` inside is: A. O(n) B. O(n²) C. O(log n) D. O(1)
**Q07 (O2)** Extra memory that grows with the input is called: A. Time complexity B. Space complexity C. Best case D. A constant
**Q08 (O2)** Linear search's best case is: A. O(n) B. O(n²) C. O(1) D. O(log n)
**Q09 (O2)** Why quote the worst case? A. It is the most common B. It is a guarantee for every input C. It is the easiest to write D. It is always O(n)
**Q10 (O3)** Finding duplicates in a big list: which is faster for large `n`? A. Nested loops, O(n²) B. A `HashSet`, O(n) C. They are always equal D. Cannot be compared

## Answers
Q01 D · Q02 B · Q03 C · Q04 D · Q05 B · Q06 B · Q07 B · Q08 C · Q09 B · Q10 B

## Practical part
Six exercises `BEG-039-EX01` to `EX06` plus the lab. The assessment is the 10-snippet complexity quiz (the ten questions above plus the lab snippets): pass at 8 of 10, and a lab with correct analysis and a measured speed-up.
