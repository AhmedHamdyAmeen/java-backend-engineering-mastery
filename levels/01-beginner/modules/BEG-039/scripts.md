# BEG-039 · Algorithms and complexity — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** finding a name in a phone book.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-039-L01 · Why we measure growth, not seconds (8 min)
**Goal:** explain why we count steps as the input grows instead of timing one run.

**Key points**
- Seconds depend on the computer, the other programs running, and luck.
- An **algorithm** is a step-by-step recipe for solving a problem.
- What matters is how the number of steps grows when the input grows (10 items, then 10 million).
- Phone book: reading every name takes 10x longer for 10x more names; flipping to the middle again and again barely grows.
- A slow-growing algorithm wins on big data even on a slow computer.

**Show:** a table of input size (10, 1,000, 1,000,000) against steps for "read every name" and "halve the book each time" (about 10, 1,000, 1,000,000 versus about 4, 10, 20).

**Check:** Why is "it ran in 2 seconds" a weak way to compare two algorithms? *(It depends on the machine and the input size; growth is what carries over.)*

---

## BEG-039-L02 · Big O notation (12 min)
**Goal:** read and write the five common Big O classes.

**Key points**
- **Big O** describes how the steps grow with input size `n`; we drop constants and small terms (3n + 5 is O(n)).
- O(1): constant, same work for any `n` (`array[i]`).
- O(log n): halve the problem each step (binary search).
- O(n): touch each item once. O(n log n): efficient sorting. O(n²): every item against every item.
- Order from fast to slow: O(1), O(log n), O(n), O(n log n), O(n²).

**Show**
```java
int first(int[] a) { return a[0]; }                                   // O(1)
int sum(int[] a)   { int s = 0; for (int x : a) s += x; return s; }   // O(n)
```

**Check:** What is the Big O of `5n + 20`? *(O(n).)*

---

## BEG-039-L03 · Analyzing loops and nested loops (12 min)
**Goal:** find the complexity of code by looking at its loops.

**Key points**
- One loop over `n` items is O(n); two loops one after the other is still O(n).
- A loop inside a loop, both over `n`, is O(n²).
- A loop that halves (`i = i / 2`) or doubles (`i = i * 2`) its counter is O(log n).
- Look for **hidden loops**: `list.contains(x)`, `list.remove(x)`, and `String.indexOf` all scan the data.
- Count the biggest part; never count only the outer loop.

**Show**
```java
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        count++;                  // n * n = O(n^2)

for (int x : items)
    if (other.contains(x)) { }    // contains is O(n) on a List: O(n^2) overall
```

**Check:** A loop over a list of `n` items calls `list.contains` inside. Complexity? *(O(n²).)*

---

## BEG-039-L04 · Space complexity (8 min)
**Goal:** measure how much extra memory an algorithm needs.

**Key points**
- **Space complexity** is the extra memory used as `n` grows (not counting the input itself).
- A few variables: O(1). A new list as big as the input: O(n).
- Time and space often trade: a `Set` can make a search fast but costs O(n) memory.
- Recursion uses memory too: each waiting call sits on the call stack.
- Choose by what is scarce: time, memory, or both.

**Show**
```java
int max(int[] a) { int m = a[0]; for (int x : a) if (x > m) m = x; return m; } // O(1) space
Set<Integer> seen = new HashSet<>();   // filled with all n inputs: O(n) space
```

**Check:** An algorithm builds a `HashSet` of all `n` inputs. Space? *(O(n).)*

---

## BEG-039-L05 · Best, average, worst (10 min)
**Goal:** tell the three cases apart and know which one we usually quote.

**Key points**
- **Best case**: luckiest input. **Worst case**: unluckiest. **Average**: typical input.
- Phone book, reading from the first page: best case the name is first (O(1)); worst case it is last or missing (O(n)).
- We usually quote the worst case because it is a promise: it never gets slower than that.
- A case is a kind of input, and each case has its own Big O.
- The same operation can differ by case: `HashMap.get` is O(1) on average.

**Show:** linear search over `[7, 3, 9, 1]`: finding 7 takes 1 step, finding 1 takes 4, finding 5 takes 4 and fails.

**Check:** Why do we usually quote the worst case? *(It is a guarantee for any input.)*

---

## BEG-039-L06 · Demo: turning an O(n²) solution into O(n) (8 min)
**Goal:** speed up a duplicate checker by replacing nested loops with a `Set`. Prepares BEG-039-LAB1.

**Steps**
1. Write `hasDuplicate(int[] a)` with two nested loops. State its complexity: O(n²).
2. Time it for 1,000, 10,000, and 100,000 items with `System.nanoTime()`; note the growth.
3. **Planned mistake:** use `List.contains` in a single loop and claim it is O(n). Run it; it is still slow.
4. Fix: the hidden loop is the problem. Use a `HashSet`: `if (!seen.add(x)) return true;`.
5. Time again; the speed-up grows with `n`.
6. State the new cost: O(n) time, O(n) space. Name the trade.

**Check:** What did we pay for the faster time? *(Extra memory: O(n) space.)*
