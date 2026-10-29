# BEG-017 · Introductory algorithms — Lecture scripts

**Video:** 63 min · **Analogy used throughout:** finding a name in a phone book, and lining up books on a shelf by height.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-017-L01 · What an algorithm is (6 min)
**Goal:** define an algorithm and why we compare them.

**Key points**
- An algorithm is a clear list of steps that solves a problem.
- A recipe is an algorithm; so is the plan from BEG-016.
- Many algorithms solve the same problem in different ways.
- We compare them by correctness first, then by how many steps they take.
- Searching and sorting are the classic first examples.

**Show:** two ways to find "Mona" in a class list: read from the top, or open the middle of a sorted list and halve the search.

**Check:** What is the first thing an algorithm must be? *(Correct.)*

---

## BEG-017-L02 · Linear search (8 min)
**Goal:** find a value by checking each element in order.

**Key points**
- Start at index 0 and compare each element to the target.
- Return the index when found; return -1 if the loop ends.
- It works on any array, sorted or not.
- Worst case: the target is last or missing, so n checks.
- Simple and good for small data.

**Show**
```java
static int linearSearch(int[] a, int target) {
    for (int i = 0; i < a.length; i++) {
        if (a[i] == target) return i;
    }
    return -1;
}
```

**Check:** How many comparisons in the worst case for 1,000 items? *(1,000.)*

---

## BEG-017-L03 · Binary search (12 min)
**Goal:** find a value in a sorted array by halving the range.

**Key points**
- It works only on sorted data.
- Check the middle: found, or discard the half that cannot contain it.
- Keep `low` and `high`; repeat while `low <= high`.
- Each step halves the range: 1,000 items need about 10 steps.
- Compute the middle as `low + (high - low) / 2`; `(low + high) / 2` can overflow for huge arrays.

**Show**
```java
int low = 0, high = a.length - 1;
while (low <= high) {
    int mid = low + (high - low) / 2;
    if (a[mid] == target) return mid;
    if (a[mid] < target) low = mid + 1;
    else high = mid - 1;
}
return -1;
```

**Check:** Why does binary search need sorted data? *(Otherwise discarding half is not safe.)*

---

## BEG-017-L04 · Bubble sort (10 min)
**Goal:** sort by swapping neighbors that are out of order.

**Key points**
- Compare neighbors; swap if the left is bigger.
- One pass pushes the largest value to the end (a bubble rising).
- Repeat passes until nothing swaps.
- Two nested loops: about n × n comparisons.
- Easy to understand, slow for large data.

**Show**
```java
for (int pass = 0; pass < a.length - 1; pass++) {
    for (int i = 0; i < a.length - 1 - pass; i++) {
        if (a[i] > a[i + 1]) { int t = a[i]; a[i] = a[i + 1]; a[i + 1] = t; }
    }
}
```
Trace `[4, 2, 3]`: swap to `[2, 4, 3]`, then `[2, 3, 4]`.

**Check:** After the first pass, where is the largest value? *(At the end.)*

---

## BEG-017-L05 · Selection sort (10 min)
**Goal:** sort by repeatedly selecting the smallest remaining value.

**Key points**
- Find the smallest value in the unsorted part.
- Swap it into the next position of the sorted part.
- Repeat, shrinking the unsorted part by one.
- At most n - 1 swaps; still about n × n comparisons.
- Like picking the shortest book and placing it first on the shelf.

**Show**
```java
for (int i = 0; i < a.length - 1; i++) {
    int min = i;
    for (int j = i + 1; j < a.length; j++) {
        if (a[j] < a[min]) min = j;
    }
    int t = a[i]; a[i] = a[min]; a[min] = t;
}
```

**Check:** What does selection sort pick on each pass? *(The smallest remaining value.)*

---

## BEG-017-L06 · Counting steps: a first look at efficiency (9 min)
**Goal:** compare algorithms by counting operations.

**Key points**
- Add a counter and increase it at each comparison.
- Linear search grows in step with n: double the data, double the work.
- Binary search grows very slowly: double the data, one more step.
- Bubble and selection grow with n × n: double the data, about four times the work.
- This is an informal preview; BEG-039 formalizes it (Big-O).

**Show**
| n | linear (worst) | binary (worst) | bubble (compares) |
| --- | --- | --- | --- |
| 8 | 8 | 4 | 28 |
| 1,000 | 1,000 | 10 | ~500,000 |

**Check:** If n doubles, what happens to linear search work? *(It about doubles.)*

---

## BEG-017-L07 · Demo: racing linear and binary search (8 min)
**Goal:** measure both searches on growing arrays. Prepares `BEG-017-LAB1`.

**Steps**
1. Build a sorted array of n numbers: `a[i] = i * 2`.
2. Time a search for a missing value with `System.nanoTime()`.
3. Run for 1,000, 100,000, and 10,000,000 elements; print a table.
4. **Planned mistake:** run binary search on an unsorted array; it misses a value that is present. Sort first and rerun.
5. Explain the trend; note that timings vary between runs and machines.

**Check:** Why can binary search give a wrong answer on unsorted data? *(It discards a half that may hold the target.)*
