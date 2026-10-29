# BEG-040 · Linear data structures — Exercises and lab

## Lab
### BEG-040-LAB1 · Build your own
**Outcomes:** 1–4 · **Time:** ~5 h
1. Implement `MyArrayList<T>` (`add`, `get`, `remove(int)`, `size`) with doubling growth.
2. Implement `MyLinkedList<T>` (`addFirst`, `addLast`, `insert`, `remove`, `contains`).
3. Implement a stack and a queue (any base) and write a bracket-matching checker with your stack.
4. Write the Big O of each method in a comment above it.
**Acceptance:** passing tests (plain `main` checks are fine until BEG-045); complexity of each method documented.

## Exercises (assessment: implementation plus 4 problems)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-040-EX01 | 1 | A dynamic array has capacity 4 and doubles when full. Count the copies done while adding 17 items, starting empty. |
| BEG-040-EX02 | 1 | Explain in three sentences why append is amortized O(1) and not worst-case O(1). |
| BEG-040-EX03 | 2 | Draw the nodes before and after removing the middle item of `A -> B -> C`; write the one line that rewires. |
| BEG-040-EX04 | 3 | Use a stack to check whether `"([)]"` and `"{[()]}"` are balanced. |
| BEG-040-EX05 | 3 | Choose stack or queue: undo history; print jobs; browser back button; customers at a counter. |
| BEG-040-EX06 | 4 | Fill in the cost (O(1) or O(n)) for `ArrayList` and a singly linked list: get by index, add at end, add at front, remove at front. |

## Solutions
- **EX01** Resizes happen when adding items 5, 9, and 17 (to capacities 8, 16, 32): 3 copies, moving 4 + 8 + 16 = 28 items in total.
- **EX02** Most appends write one slot. Occasionally one append copies all items (O(n)). The total over `n` appends is about 2n, so on average each is O(1), but a single append can be O(n).
- **EX03** Before: A -> B -> C. After: A -> C. `a.next = b.next;` (with `a` the node before `b`).
- **EX04** `"([)]"` is not balanced (`)` meets `[` on top); `"{[()]}"` is balanced and the stack ends empty.
- **EX05** Stack; queue; stack; queue.
- **EX06** `ArrayList`: O(1), O(1) amortized, O(n), O(n). Singly linked list: O(n), O(n) without a tail reference (O(1) with one), O(1), O(1).
