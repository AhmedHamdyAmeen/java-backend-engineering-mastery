# BEG-040 · Linear data structures — Quiz

Outcomes: O1 dynamic array · O2 linked list · O3 stack and queue · O4 compare structures.

**Q01 (O1)** Array access `a[i]` costs: A. O(n) B. O(log n) C. O(n²) D. O(1)
**Q02 (O1)** A dynamic array that is full usually: A. Throws an error B. Allocates a bigger array and copies C. Deletes the oldest item D. Does nothing
**Q03 (O1)** Growing by doubling makes append: A. Amortized O(1) B. Always O(n) C. O(n²) D. O(log n)
**Q04 (O1)** Growing by +1 each time makes `n` appends cost about: A. O(n) B. O(n²) C. O(log n) D. O(1)
**Q05 (O2)** A singly linked list node holds: A. Only a value B. A value and a reference to the next node C. An index D. Two arrays
**Q06 (O2)** Searching a linked list by value is: A. O(1) B. O(log n) C. O(n) D. O(n²)
**Q07 (O2)** The last node's `next` is: A. The head B. `null` C. Itself D. Zero
**Q08 (O3)** A stack is: A. FIFO B. Random access C. Sorted D. LIFO
**Q09 (O3)** Which fits "tasks processed in arrival order"? A. Stack B. Queue C. Tree D. Set
**Q10 (O4)** Which JDK class is the usual choice for a stack or queue? A. `Stack` B. `Vector` C. `ArrayDeque` D. `int[]`

## Answers
Q01 D · Q02 B · Q03 A · Q04 B · Q05 B · Q06 C · Q07 B · Q08 D · Q09 B · Q10 C

## Practical part
Implementation of the lab (`MyArrayList`, `MyLinkedList`, stack, queue, bracket checker) plus 4 problems (`BEG-040-EX01`, `EX04`, `EX05`, `EX06`). Pass: tests pass, complexity documented, and at least 3 of the 4 problems correct. Exercises `EX02` and `EX03` are also part of the module.
