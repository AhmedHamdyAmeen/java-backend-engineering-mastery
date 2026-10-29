# BEG-040 · Linear data structures — Lecture scripts

**Video:** 68 min · **Analogy used throughout:** a row of lockers, a stack of plates, and a queue at a shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-040-L01 · Arrays in memory (8 min)
**Goal:** explain why array access by index is instant.

**Key points**
- An array is a row of equal-sized boxes side by side in memory (the lockers).
- The computer finds item `i` by arithmetic: start address plus `i` times the item size. That is O(1).
- The size is fixed when you create the array.
- Inserting in the middle means shifting everything after it: O(n).
- Searching an unsorted array means checking each item: O(n).

**Show:** a drawing of 5 lockers numbered 0 to 4, with an arrow jumping straight to locker 3.

**Check:** Why is `a[3]` O(1)? *(The position is computed; nothing is scanned.)*

---

## BEG-040-L02 · Dynamic arrays and resizing (12 min)
**Goal:** explain how a list grows and why append is amortized O(1).

**Key points**
- A dynamic array (like `ArrayList`) keeps a plain array plus a `size` counter.
- When the array is full, make a new array about twice as big and copy the items over.
- Copying costs O(n) but happens rarely. Spread over many appends, each append is **amortized** O(1) ("on average, over many operations").
- Growing by +1 each time would copy on every append, so the total becomes O(n²).
- Capacity is the array's length; size is how many items are really stored.

**Show**
```java
if (size == data.length) {
    data = java.util.Arrays.copyOf(data, data.length * 2);
}
data[size++] = item;
```

**Check:** Why double instead of adding one slot? *(Doubling copies rarely; +1 copies on every append.)*

---

## BEG-040-L03 · Linked lists (15 min)
**Goal:** build a singly linked list and know its costs.

**Key points**
- A linked list is a chain of **nodes**; each holds a value and a reference to the next node (a treasure hunt of clues).
- Keep a `head` reference; the last node's `next` is `null`.
- Insert at the head: O(1). Search by value: O(n). No jumping to index `i`.
- To remove a node, point the previous node's `next` past it. Do not lose the head or the tail while rewiring.
- Nodes are scattered in memory and cost extra for the references.

**Show**
```java
class Node<T> { T value; Node<T> next; Node(T v) { value = v; } }
void addFirst(T v) { Node<T> n = new Node<>(v); n.next = head; head = n; }
```

**Check:** What is the cost of `get(i)` on a linked list? *(O(n): you walk from the head.)*

---

## BEG-040-L04 · Stacks (10 min)
**Goal:** use a stack: last in, first out.

**Key points**
- A **stack** is like a stack of plates: you add and remove only at the top.
- Operations: `push` (add), `pop` (remove top), `peek` (look at top). All O(1).
- **LIFO**: last in, first out.
- Uses: undo, the call stack, matching brackets, backtracking.
- In Java use `ArrayDeque` as a stack (`push`, `pop`, `peek`); avoid the old `Stack` class.

**Show:** checking `"{[()]}"`: push each opener; on a closer, pop and compare; at the end the stack must be empty.

**Check:** After `push(1)`, `push(2)`, `pop()`, what does `peek()` return? *(1.)*

---

## BEG-040-L05 · Queues (10 min)
**Goal:** use a queue: first in, first out.

**Key points**
- A **queue** is a line at a shop: join at the back, leave from the front.
- **FIFO**: first in, first out.
- Operations: `offer` (enqueue), `poll` (dequeue), `peek`. All O(1) with a good implementation.
- Uses: print jobs, task processing, breadth-first search, message queues.
- A queue on a plain array wastes time shifting items; use a linked list or a circular array.

**Show**
```java
Queue<String> q = new ArrayDeque<>();
q.offer("Ana");
q.offer("Omar");
String next = q.poll();   // "Ana"
```

**Check:** Which serves the oldest item first, a stack or a queue? *(A queue.)*

---

## BEG-040-L06 · Choosing: ArrayList vs LinkedList vs ArrayDeque (5 min)
**Goal:** pick the right JDK structure for a problem.

**Key points**
- `ArrayList`: fast `get(i)`, fast append, slow insert/remove in the middle. The default choice.
- `LinkedList`: fast insert/remove at the ends or at a known node, slow `get(i)`; in practice rarely faster than the others.
- `ArrayDeque`: fast at both ends. Best for stacks and queues.
- Measure before claiming one is faster; arrays are friendly to the CPU cache.
- Decide by the operation you do most.

**Show:** a table: operation / `ArrayList` / `LinkedList` / `ArrayDeque` (get by index, add at end, add at front, remove from middle).

**Check:** Which would you use for a queue of tasks? *(`ArrayDeque`.)*

---

## BEG-040-L07 · Demo: building MyArrayList and watching it resize (8 min)
**Goal:** write a small dynamic array and print each resize. Prepares BEG-040-LAB1.

**Steps**
1. Create `MyArrayList<T>` with `Object[] data`, `int size`, initial capacity 2.
2. Write `add(T item)` and `get(int index)` (reject bad indexes).
3. **Planned mistake:** grow by +1 in `add`; print "resized" and count copies for 20 adds (about 18).
4. Fix: double the capacity; run again and see only a few resizes (to 4, 8, 16, 32).
5. Add `size()` and `remove(int index)` that shifts items left; null out the freed slot.
6. Note the cost of each method; this goes into the lab documentation.

**Check:** How many resizes happen for 20 adds with doubling from capacity 2? *(Four: to 4, 8, 16, and 32.)*
