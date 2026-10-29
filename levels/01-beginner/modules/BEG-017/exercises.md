# BEG-017 · Introductory algorithms — Exercises and lab

## Lab
### BEG-017-LAB1 · Race the algorithms
**Outcomes:** 1–3 · **Time:** ~2 h
1. Implement `linearSearch` and `binarySearch`.
2. Build sorted arrays of 1,000, 100,000, and 10,000,000 elements.
3. Time both searches (target missing, worst case) with `System.nanoTime()`; repeat a few times.
4. Present a results table and write a short explanation of the trend.

**Acceptance:** correct implementations; written explanation of the trend.

## Exercises (assessment: five exercises including tracing a sort by hand)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-017-EX01 | 1 | Implement `linearSearch(int[] a, int target)` returning the index or -1. |
| BEG-017-EX02 | 1 | Trace binary search for 23 in `[2, 5, 8, 12, 16, 23, 38]`; state when binary search applies. |
| BEG-017-EX03 | 2 | Trace bubble sort by hand on `[5, 1, 4, 2]`, showing the array after each pass. |
| BEG-017-EX04 | 2 | Implement selection sort and test it on an empty and a one-element array. |
| BEG-017-EX05 | 3 | Add a comparison counter to linear search and bubble sort; report counts for n = 10, 20, 40 and describe the growth. |

## Solutions
- **EX01** The loop from L02.
- **EX02** low 0, high 6, mid 3 (12 < 23) so low 4; mid 5 (23) found at index 5. It applies only when the data is sorted.
- **EX03** After pass 1: `[1, 4, 2, 5]`; pass 2: `[1, 2, 4, 5]`; pass 3: no swaps, sorted.
- **EX04** Code from L05; for empty and one-element input the loops do not run, which is correct.
- **EX05** Linear worst case: 10, 20, 40 (doubles). Bubble: 45, 190, 780 (about four times when n doubles).
- The informal growth comparison is also in the lab explanation.
