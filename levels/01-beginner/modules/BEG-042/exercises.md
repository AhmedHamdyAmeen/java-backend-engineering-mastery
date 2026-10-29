# BEG-042 · Trees — Exercises and lab

## Lab
### BEG-042-LAB1 · BST and task scheduler
**Outcomes:** 1–4 · **Time:** ~4 h
1. Implement a BST with `insert`, `contains`, and all four traversals returning lists.
2. Insert sorted values and show the height problem.
3. Build a task scheduler with `PriorityQueue<Task>` (priority, then name) that always runs the most urgent task next.
**Acceptance:** tests pass; traversal outputs correct.

## Exercises (assessment: implementation plus traversal exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-042-EX01 | 1 | Insert 50, 30, 70, 20, 40, 60, 80 into a BST and draw it. Is 45 found, and by which path? |
| BEG-042-EX02 | 1 | Write `contains(Node, int)` recursively, including the null case. |
| BEG-042-EX03 | 2 | For the tree from EX01, write pre-, in-, post-, and level-order outputs. |
| BEG-042-EX04 | 3 | Explain in three sentences why inserting 1, 2, 3, 4, 5 into a BST is a problem and what balanced trees do. |
| BEG-042-EX05 | 4 | Show a min-heap after adding 9, 4, 7, 1 (as an array); then what `poll()` returns twice. |
| BEG-042-EX06 | 4 | Explain two differences between a BST and a heap. |

## Solutions
- **EX01** Root 50; left 30 (20, 40); right 70 (60, 80). 45 is not found: 50, left to 30, right to 40, right of 40 is `null`.
- **EX02** `if (n == null) return false; if (v == n.value) return true; return v < n.value ? contains(n.left, v) : contains(n.right, v);`
- **EX03** Pre: 50 30 20 40 70 60 80. In: 20 30 40 50 60 70 80. Post: 20 40 30 60 80 70 50. Level: 50 30 70 20 40 60 80.
- **EX04** Sorted inserts always go right, giving a chain of height n, so search is O(n). Balanced trees rotate nodes to keep the height near log n, so operations stay O(log n).
- **EX05** One valid layout: `[1, 4, 7, 9]` (insert 9; add 4 and swap up -> 4, 9; add 7 -> 4, 9, 7; add 1 and swap up twice -> 1, 4, 7, 9). `poll()` returns 1, then 4.
- **EX06** A BST keeps left < node < right and supports sorted traversal and search in O(log n) when balanced; a heap only guarantees parent <= children, gives the minimum in O(1), and cannot be searched quickly or iterated in order.
