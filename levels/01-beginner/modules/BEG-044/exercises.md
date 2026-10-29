# BEG-044 · Algorithmic techniques — Exercises and lab

## Lab
### BEG-044-LAB1 · Technique drills
**Outcomes:** 1–4 · **Time:** ~4 h
Solve 8 problems, 2 per technique: two pointers (pair sum in a sorted array; reverse in place), sliding window (best sum of `k` consecutive items; longest substring without repeats), recursion (sum of digits; power), and backtracking (subsets; permutations). State the time complexity of each solution in a comment.
**Acceptance:** 6 of 8 correct within target complexity.

## Exercises (assessment: unseen timed problem set; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-044-EX01 | 1 | Given sorted `[1, 3, 4, 6, 9, 11]` and target 10, trace the two pointers until the pair is found. |
| BEG-044-EX02 | 1 | Remove duplicates from a sorted array in place with two pointers; return the new length. |
| BEG-044-EX03 | 2 | For `[2, 1, 5, 1, 3, 2]` and `k = 3`, find the maximum sum of 3 consecutive items with a sliding window. |
| BEG-044-EX04 | 3 | Write `sumDigits(int n)` recursively; name the base case. |
| BEG-044-EX05 | 3 | List all subsets of `[1, 2, 3]` and say how many permutations it has. |
| BEG-044-EX06 | 4 | Pick a technique for each: (a) longest run of 1s with at most one 0 flipped; (b) find two numbers that sum to a target in a sorted array; (c) all orderings of 4 letters; (d) count the files in nested folders. |

## Solutions
- **EX01** l=0, r=5: 1+11=12, too big, r-- ; 1+9=10, found (1 and 9).
- **EX02** `int w = 1; for (int r = 1; r < a.length; r++) if (a[r] != a[w-1]) a[w++] = a[r]; return w;` (assuming a non-empty array).
- **EX03** Window sums: 8, 7, 9, 6. Maximum 9 (items 5, 1, 3).
- **EX04** `if (n < 10) return n; return n % 10 + sumDigits(n / 10);` Base case: a single digit (n < 10).
- **EX05** `[]`, `[1]`, `[2]`, `[3]`, `[1,2]`, `[1,3]`, `[2,3]`, `[1,2,3]` (8 subsets); 3! = 6 permutations.
- **EX06** (a) sliding window; (b) two pointers; (c) backtracking; (d) recursion.
