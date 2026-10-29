# BEG-041 · Hashing — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a wall of numbered mailboxes in an office.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-041-L01 · Hash functions (10 min)
**Goal:** explain what a hash function does and what makes a good one.

**Key points**
- A **hash function** turns any key (a name, a number) into an integer called the hash code.
- The same key must always give the same number.
- A good function spreads different keys widely, so they do not pile up.
- Different keys can still give the same number; that is allowed but unwanted.
- In Java, `hashCode()` provides it, and it must agree with `equals`: equal objects must have equal hash codes.

**Show**
```java
"Ana".hashCode();    // some int, the same every run
"Ana".hashCode() == "Ana".hashCode();   // true
```

**Check:** If `a.equals(b)` is true, what must be true of their hash codes? *(They must be equal.)*

---

## BEG-041-L02 · Hash tables and buckets (12 min)
**Goal:** explain how a hash table finds a key quickly.

**Key points**
- A hash table is an array of **buckets** (the mailboxes).
- To store a key: compute its hash, then pick a bucket with `index = hash % buckets` (Java makes the result non-negative).
- To find a key: compute the same hash, go straight to that bucket, and look only there.
- That skips scanning everything, so get and put are O(1) on average.
- The bucket holds the key and its value, so a table can act as a map.

**Show:** a drawing of 8 mailboxes; "Ana" hashes to 3, "Omar" to 6; looking up "Ana" opens box 3 directly.

**Check:** Why is lookup fast? *(The hash tells us which bucket to open; we do not scan the rest.)*

---

## BEG-041-L03 · Collisions and resizing (12 min)
**Goal:** explain what happens when two keys land in the same bucket, and how the table stays fast.

**Key points**
- A **collision** is two different keys mapped to one bucket.
- **Chaining**: each bucket holds a small list; add the new entry to it and compare keys with `equals` when searching.
- **Open addressing**: if the bucket is taken, probe the next free slot.
- The **load factor** is entries divided by buckets. When it passes a limit (Java's default is 0.75), the table doubles its buckets and re-places every entry.
- Few collisions mean short chains and O(1); many collisions mean long chains and slow lookups.

**Show:** bucket 3 holding a chain `Ana -> Sara`; a lookup of "Sara" finds bucket 3, then walks the chain.

**Check:** What does resizing at a load factor protect? *(It keeps chains short, so lookups stay fast.)*

---

## BEG-041-L04 · Inside HashMap and HashSet (11 min)
**Goal:** connect the theory to the JDK classes and their rules.

**Key points**
- `HashMap` is a hash table with chaining; default capacity 16, load factor 0.75, doubling on resize. Verify version details before recording.
- Since Java 8, a long chain in one bucket can become a balanced tree, limiting the damage of bad hash codes.
- `HashSet` is a `HashMap` that uses your items as keys with a dummy value.
- Your key class must override `equals` and `hashCode` together.
- **Never mutate a key** after insertion: its hash changes and the entry is lost in the wrong bucket.
- Iteration order of `HashMap` is not guaranteed; never rely on it.

**Show**
```java
Map<String, Integer> ages = new HashMap<>();
ages.put("Ana", 30);
ages.get("Ana");          // 30
```

**Check:** Why must you not change a key after putting it in a `HashMap`? *(Its hash code changes, so the lookup goes to the wrong bucket.)*

---

## BEG-041-L05 · Demo: MyHashMap and the constant-hashCode slowdown (8 min)
**Goal:** build a chained hash map, then break its speed with a bad `hashCode`. Prepares BEG-041-LAB1.

**Steps**
1. Create `MyHashMap<K,V>` with an array of buckets and a small `Node<K,V>` chain (key, value, next).
2. Write `put` and `get`: bucket index from `Math.abs(key.hashCode() % buckets.length)` (beware `Integer.MIN_VALUE`; use `(h & 0x7fffffff) % length`).
3. Add resizing when `size > 0.75 * buckets.length`: new array twice as big, re-insert all nodes.
4. **Planned mistake:** a key class whose `hashCode()` returns `1`. Insert 20,000 keys and time it; it is slow because all keys share one chain.
5. Fix: a key class with a proper `hashCode`; time again and compare.
6. Note timing numbers for the lab evidence.

**Check:** Why does a constant `hashCode` make the map slow? *(Every key goes into one bucket, so lookup scans one long chain: O(n).)*
