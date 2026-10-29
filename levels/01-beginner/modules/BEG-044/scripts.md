# BEG-044 · Algorithmic techniques — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a pair of walkers on a path, a sliding picture frame, and nested Russian dolls.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-044-L01 · Two pointers (12 min)
**Goal:** solve sorted-array problems with two indexes instead of nested loops.

**Key points**
- Two pointers are two indexes (two walkers) that move through the array, often from both ends.
- It works when the data is **sorted**: moving a pointer has a predictable effect on the result.
- Example: find two numbers that add up to a target. Too small: move the left pointer right. Too big: move the right pointer left.
- Each pointer moves one way only, so the cost is O(n) instead of O(n²).
- On unsorted data it fails; sort first (O(n log n)) or use a `Set`.

**Show**
```java
int l = 0, r = a.length - 1;
while (l < r) {
    int sum = a[l] + a[r];
    if (sum == target) return true;
    if (sum < target) l++; else r--;
}
return false;
```

**Check:** Why does this need a sorted array? *(The sum only moves in a known direction when each pointer step makes it larger or smaller.)*

---

## BEG-044-L02 · Sliding window (12 min)
**Goal:** solve subarray and substring problems with a window that grows and shrinks.

**Key points**
- A **window** is a range `[left, right]` (the picture frame) that slides across the data.
- Move `right` to add an item; move `left` to drop one. Update the answer incrementally; do not recompute from scratch.
- Fixed-size window: for example the best sum of any 3 consecutive items.
- Variable-size window: for example the longest substring without repeated characters.
- Each index moves forward at most `n` times, so it is O(n). Watch the off-by-one at the window edges.

**Show**
```java
int sum = 0, best = Integer.MIN_VALUE;
for (int i = 0; i < a.length; i++) {
    sum += a[i];
    if (i >= k) sum -= a[i - k];
    if (i >= k - 1) best = Math.max(best, sum);
}
```

**Check:** Why is a sliding window O(n) and not O(n × k)? *(Each step adds one item and removes one; nothing is re-added.)*

---

## BEG-044-L03 · Thinking recursively (10 min)
**Goal:** write a recursive method with a base case and a smaller step.

**Key points**
- **Recursion**: a method that calls itself on a smaller version of the problem (Russian dolls).
- Every recursive method needs a **base case** (stop) and a **recursive case** (move toward the base case).
- Trust the smaller call: assume it works and combine its result.
- Each call waits on the call stack; too deep gives `StackOverflowError`.
- Some problems are naturally recursive: factorial, trees, folders in folders.

**Show**
```java
int factorial(int n) {
    if (n <= 1) return 1;          // base case
    return n * factorial(n - 1);   // smaller problem
}
```

**Check:** What happens with no base case? *(The calls never stop and the stack overflows.)*

---

## BEG-044-L04 · Backtracking (11 min)
**Goal:** generate all subsets or permutations by choosing, exploring, and undoing.

**Key points**
- **Backtracking** tries a choice, goes deeper recursively, then undoes the choice and tries the next.
- Pattern: choose, explore, un-choose.
- Subsets of `n` items: 2ⁿ results. Permutations: n! results. Expect these to grow very fast.
- Stop early when a partial answer cannot work (pruning).
- Copy the current list when you save a result; otherwise later changes alter it.

**Show**
```java
void subsets(int[] a, int i, List<Integer> cur, List<List<Integer>> out) {
    if (i == a.length) { out.add(new ArrayList<>(cur)); return; }
    subsets(a, i + 1, cur, out);              // skip a[i]
    cur.add(a[i]);
    subsets(a, i + 1, cur, out);              // take a[i]
    cur.remove(cur.size() - 1);               // undo
}
```

**Check:** How many subsets does a 3-item set have? *(8.)*

---

## BEG-044-L05 · Demo: solving a problem with a sliding window (8 min)
**Goal:** find the longest substring with no repeated characters. Prepares BEG-044-LAB1.

**Steps**
1. State the problem and the brute-force idea: check every substring, O(n³) or O(n²) with care.
2. Choose a window `[left, right]` and a `Set<Character>` of what is in it.
3. Move `right`; while the new character is already in the set, remove `s.charAt(left)` and move `left`.
4. **Planned mistake:** compute the length as `right - left` instead of `right - left + 1`; run on `"abc"` and see 2 instead of 3. Fix the off-by-one.
5. Test `""`, `"aaaa"`, `"abcabcbb"` (answer 3).
6. State the cost: O(n) time, O(k) space for the character set.

**Check:** Why is `right - left + 1` the length? *(Both ends are included, so a window with `left == right` holds one item.)*
