# BEG-041 · Hashing — Quiz

Outcomes: O1 hash tables and buckets · O2 collisions and resizing · O3 bad hash codes and mutable keys.

**Q01 (O1)** A hash function turns a key into: A. An integer B. A sorted list C. A String only D. A bucket full of keys
**Q02 (O1)** If `a.equals(b)` is true, their `hashCode()` values must be: A. Different B. Equal C. Zero D. Unrelated
**Q03 (O1)** In a hash table, the bucket for a key is chosen from: A. Insertion order B. The key's hash code C. The value D. Alphabetical order
**Q04 (O1)** Average cost of `HashMap.get`: A. O(n) B. O(log n) C. O(1) D. O(n²)
**Q05 (O2)** Two different keys in the same bucket is called a: A. Resize B. Collision C. Overflow D. Duplicate
**Q06 (O2)** Chaining handles collisions by: A. Overwriting the old entry B. Deleting the old entry C. Refusing the new key D. Keeping a list of entries in the bucket
**Q07 (O2)** Load factor is: A. Entries divided by buckets B. Buckets divided by entries C. The longest chain D. The key size
**Q08 (O2)** When the load factor limit is passed, the table: A. Stops accepting keys B. Doubles its buckets and re-places entries C. Sorts itself D. Throws an exception
**Q09 (O3)** A `hashCode` that always returns the same number makes lookups about: A. O(1) B. O(log n) C. O(n) D. Faster
**Q10 (O3)** Changing a key after putting it in a `HashMap` can cause: A. A faster map B. An automatic resize C. A compile error D. The entry to be impossible to find

## Answers
Q01 A · Q02 B · Q03 B · Q04 C · Q05 B · Q06 D · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Implementation of `MyHashMap` (lab `BEG-041-LAB1`) with timing evidence, plus this quiz and exercises `BEG-041-EX01` to `EX06`. Pass: tests pass, timing shows the constant-hash slowdown, and at least 8 of 10 quiz answers correct.
