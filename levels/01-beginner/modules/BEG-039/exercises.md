# BEG-039 · Algorithms and complexity — Exercises and lab

## Lab
### BEG-039-LAB1 · Analyze and improve
**Outcomes:** 1–3 · **Time:** ~3 h
1. State the time complexity of eight provided snippets (constant, single loop, nested loop, halving loop, hidden `contains`, and so on) and write a one-line reason for each.
2. Rewrite two O(n²) solutions (for example duplicate detection and "find a pair with a given sum") as O(n) using a `Set` or `Map`.
3. Time old and new versions on three input sizes and record the table.
**Acceptance:** correct analysis; measured speed-up.

## Exercises (assessment: complexity quiz of 10 snippets; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-039-EX01 | 1 | Give the Big O: `a[5]`; a single loop over `n`; two nested loops over `n`; a loop with `i *= 2`; a sort with `Collections.sort`. |
| BEG-039-EX02 | 1 | Simplify to Big O: `3n + 10`, `n² + n`, `100`, `n log n + n`. |
| BEG-039-EX03 | 2 | State the time and space complexity of reversing an array into a new array, and of reversing it in place. |
| BEG-039-EX04 | 2 | For linear search in an array, describe the best, average, and worst case and the input that causes each. |
| BEG-039-EX05 | 3 | Two solutions check whether a list has two equal items: nested loops, or a `HashSet`. Compare by time and space and choose one; say when you would choose the other. |
| BEG-039-EX06 | 1 | A loop over `n` calls `list.remove(0)` on an `ArrayList` each time. What is the total complexity and why? |

## Solutions
- **EX01** O(1); O(n); O(n²); O(log n); O(n log n).
- **EX02** O(n); O(n²); O(1); O(n log n).
- **EX03** New array: O(n) time, O(n) space. In place with two indexes: O(n) time, O(1) space.
- **EX04** Best: target is first, 1 step. Worst: target last or missing, `n` steps. Average: about `n/2` steps, still O(n).
- **EX05** Nested loops: O(n²) time, O(1) space. `HashSet`: O(n) time, O(n) space. Choose the `HashSet` for large inputs; nested loops only if memory is very tight or `n` is tiny.
- **EX06** O(n²): `remove(0)` shifts all remaining items (O(n)), done `n` times.
- Outcome 3 is also covered by the lab (rewrite and measure) and the quiz.
