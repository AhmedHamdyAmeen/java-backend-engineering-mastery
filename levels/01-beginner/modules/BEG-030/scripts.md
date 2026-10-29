# BEG-030 · Collections — Lecture scripts

**Video:** 81 min · **Analogy used throughout:** different kinds of containers: a numbered shelf, a bag of unique tokens, a phone book, a ticket queue.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-030-L01 · Beyond arrays: the Collections Framework (8 min)
**Goal:** see why we need more than arrays.

**Key points**
- An array has a fixed size. Adding, removing, and searching are awkward.
- The Collections Framework gives ready-made containers that grow and shrink.
- Four main kinds: `List` (ordered, duplicates allowed), `Set` (no duplicates), `Map` (key to value), `Queue` (waiting line).
- They live in `java.util`.
- The `<String>` in `List<String>` says what the container holds. Generics are explained in BEG-031.

**Show:** a picture of four containers with example contents.

**Check:** Which kind of collection does not allow duplicates? *(`Set`.)*

---

## BEG-030-L02 · Lists (12 min)
**Goal:** use `ArrayList` and know when `LinkedList` differs.

**Key points**
- A `List` keeps insertion order and allows duplicates. Positions start at 0.
- Declare by interface, create by class: `List<String> names = new ArrayList<>();`.
- Core methods: `add`, `get(i)`, `set`, `remove`, `size`, `contains`, `isEmpty`.
- `ArrayList` is backed by an array: fast `get(i)`, slower insert in the middle.
- `LinkedList` is a chain of nodes: fast at the ends, slow `get(i)`. Use `ArrayList` unless you have a reason.
- `contains` scans the whole list, so it is slow on big lists.

**Show**
```java
List<String> names = new ArrayList<>();
names.add("Ana"); names.add("Omar");
System.out.println(names.get(1)); // Omar
```

**Check:** Which list is the default choice? *(`ArrayList`.)*

---

## BEG-030-L03 · Sets (10 min)
**Goal:** use sets to keep unique values.

**Key points**
- A `Set` ignores a second copy of the same value; `add` returns `false`.
- `HashSet`: fastest, no order promised.
- `LinkedHashSet`: keeps insertion order.
- `TreeSet`: keeps values sorted.
- Fast "is it in there?" checks with `contains`.

**Show**
```java
Set<String> tags = new HashSet<>();
tags.add("java"); tags.add("java");
System.out.println(tags.size()); // 1
```

**Check:** Which set keeps values sorted? *(`TreeSet`.)*

---

## BEG-030-L04 · Maps (15 min)
**Goal:** store and look up values by key.

**Key points**
- A `Map<K, V>` holds key-value pairs. Keys are unique; values may repeat.
- `put`, `get`, `containsKey`, `remove`, `size`, `getOrDefault`.
- `HashMap`: fast, no order. `LinkedHashMap`: insertion order. `TreeMap`: sorted by key.
- `get` returns `null` when the key is missing.
- Loop with `entrySet()`; use `merge` or `getOrDefault` for counting.

**Show**
```java
Map<String, Integer> stock = new HashMap<>();
stock.put("pen", 10);
stock.merge("pen", 5, Integer::sum); // 15
for (Map.Entry<String, Integer> e : stock.entrySet()) {
    System.out.println(e.getKey() + "=" + e.getValue());
}
```

**Check:** What does `get` return for a missing key? *(`null`.)*

---

## BEG-030-L05 · Queues and deques (8 min)
**Goal:** model a waiting line.

**Key points**
- A `Queue` is first in, first out (FIFO): `offer` to add, `poll` to take from the front, `peek` to look.
- `poll` and `peek` return `null` when empty.
- `ArrayDeque` is a good general queue.
- A `Deque` works at both ends, so it also works as a stack: `push`, `pop`.
- `PriorityQueue` hands out the smallest element first.

**Show**
```java
Queue<String> line = new ArrayDeque<>();
line.offer("Ana"); line.offer("Omar");
System.out.println(line.poll()); // Ana
```

**Check:** In a queue, who leaves first? *(The one who arrived first.)*

---

## BEG-030-L06 · Choosing a collection: decision chart (7 min)
**Goal:** pick a collection from the requirement.

**Key points**
- Key to value lookup? `Map`.
- Unique values only? `Set`.
- Ordered, duplicates, index access? `List`.
- Process in arrival order? `Queue`/`Deque`.
- Then pick ordering: none (`Hash*`), insertion (`Linked*`), sorted (`Tree*`).
- Declare variables by interface type, such as `List<String> x = new ArrayList<>();`, so the implementation can change later.

**Show:** a flowchart that follows these questions.

**Check:** You need to find a customer by id quickly. Which collection? *(A `Map`.)*

---

## BEG-030-L07 · Iteration and `ConcurrentModificationException` (5 min)
**Goal:** remove items while looping safely.

**Key points**
- A for-each loop reads each element in turn.
- Removing from a list inside a for-each throws `ConcurrentModificationException`.
- Safe options: an `Iterator` with `it.remove()`, or `list.removeIf(...)`.
- `removeIf` is the simplest.

**Show**
```java
List<Integer> nums = new ArrayList<>(List.of(1, 2, 3, 4));
nums.removeIf(n -> n % 2 == 0); // [1, 3]
```

**Check:** What is the simplest safe way to remove matching elements? *(`removeIf`.)*

---

## BEG-030-L08 · Demo: word frequency with Map (8 min)
**Goal:** count words with a `Map`. Prepares `BEG-030-LAB1`.

**Steps**
1. Split a sentence on spaces into words, lowercase them.
2. Create `Map<String, Integer> counts = new HashMap<>();`.
3. For each word use `counts.merge(word, 1, Integer::sum)`.
4. **Planned mistake:** use `counts.get(word) + 1` on a new word; it throws `NullPointerException`. Fix with `merge` or `getOrDefault`.
5. Print entries; switch to `TreeMap` to see sorted output.

---

## BEG-030-L09 · Demo: the wrong collection, measured (8 min)
**Goal:** see why the choice matters.

**Steps**
1. Fill an `ArrayList` and a `HashSet` with 100,000 numbers.
2. Time 10,000 `contains` calls on each using `System.nanoTime()`.
3. **Planned mistake:** conclude from one noisy run; repeat a few times and compare.
4. Observe: the list is far slower because it scans every element.
5. Conclusion: use a `Set` or `Map` for lookups.
