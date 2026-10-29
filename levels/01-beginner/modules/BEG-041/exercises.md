# BEG-041 · Hashing — Exercises and lab

## Lab
### BEG-041-LAB1 · MyHashMap
**Outcomes:** 1–3 · **Time:** ~3 h
1. Implement a chaining-based `MyHashMap<K,V>` with `put`, `get`, `remove`, `size`, and load-factor resizing.
2. Test it, including replacing an existing key and a missing key.
3. Create a key class with a constant `hashCode`; time 20,000 inserts and lookups with it and with a good `hashCode`; record both timings.
**Acceptance:** tests pass; timing evidence.

## Exercises (assessment: implementation plus quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-041-EX01 | 1 | With 5 buckets and `index = hash % 5`, place keys with hashes 12, 7, 22, 3, 17 and say where the collisions are. |
| BEG-041-EX02 | 1 | Explain in three sentences how `get` finds a value without scanning the whole table. |
| BEG-041-EX03 | 2 | Compare chaining and open addressing in two sentences each. |
| BEG-041-EX04 | 2 | A table has 16 buckets and load factor 0.75. At which entry count does it resize, and to what size? |
| BEG-041-EX05 | 3 | A `Point` class overrides `equals` but not `hashCode`. Describe what goes wrong when you put it in a `HashSet`. |
| BEG-041-EX06 | 3 | A key is stored in a `HashMap`, then one of its fields changes. What happens to `get(key)`, and how do you avoid it? |

## Solutions
- **EX01** Indexes: 12 -> 2, 7 -> 2, 22 -> 2, 3 -> 3, 17 -> 2. Keys 12, 7, 22, 17 collide in bucket 2; 3 is alone in bucket 3.
- **EX02** `get` computes the key's hash, turns it into a bucket index, and opens only that bucket. It compares keys with `equals` along the short chain there. The rest of the table is never touched.
- **EX03** Chaining: each bucket holds a list of entries, and colliding keys are added to it; easy to implement. Open addressing: all entries live in the array itself, and a collision probes for the next free slot; saves node objects but needs care when removing.
- **EX04** Resize when entries exceed 12 (16 x 0.75); new capacity 32.
- **EX05** Two equal points can have different hash codes, so they land in different buckets and the set may hold duplicates or fail `contains`. Always override both methods together.
- **EX06** The hash changes, so `get` looks in a different bucket and returns `null` (the entry is still inside, unreachable). Use immutable keys such as `String`, `Integer`, or records.
