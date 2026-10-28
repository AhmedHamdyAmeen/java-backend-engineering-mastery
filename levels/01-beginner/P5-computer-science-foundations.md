# BEG-P5 — Computer Science Foundations

**Phase goal:** the learner reasons about efficiency, knows how the core data structures work inside, and writes automated tests for their own code.

**Phase practice:** implement each data structure from scratch, then compare with the JDK implementation; all implementations covered by JUnit tests from BEG-045 onward (retrofit earlier ones).

**Phase total:** ~6.8 h video · ~26 h practice

---

### BEG-039 · Algorithms and complexity
`n: 39` · **Video:** 58 min · **Practice:** 3 h

**Prerequisites:** BEG-017

**Learning outcomes** — the learner can:
1. Express the time complexity of simple code in Big O (O(1), O(log n), O(n), O(n log n), O(n²)).
2. Distinguish time and space complexity and best, average, and worst cases.
3. Compare two solutions to the same problem by complexity and choose one.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-039-L01 | Why we measure growth, not seconds | 8 |
| BEG-039-L02 | Big O notation | 12 |
| BEG-039-L03 | Analyzing loops and nested loops | 12 |
| BEG-039-L04 | Space complexity | 8 |
| BEG-039-L05 | Best, average, worst | 10 |
| BEG-039-L06 | Demo: turning an O(n²) solution into O(n) | 8 |

**Lab** — `BEG-039-LAB1` *Analyze and improve:* state the complexity of eight snippets, then rewrite two O(n²) solutions as O(n) using a `Set` or `Map`. Acceptance: correct analysis; measured speed-up.

**Common mistakes:** counting only the outer loop; ignoring hidden loops (`list.contains`).

**Assessment:** complexity quiz (10 snippets).

**Career relevance:** capacity planning (SRC-004) and interview questions at every level.

---

### BEG-040 · Linear data structures
`n: 40` · **Video:** 68 min · **Practice:** 5 h

**Prerequisites:** BEG-031, BEG-039

**Learning outcomes** — the learner can:
1. Implement a dynamic array and explain amortized O(1) append.
2. Implement a singly linked list with insert, remove, and search.
3. Implement a stack and a queue and pick one for a given problem.
4. Compare array-based and linked structures by operation cost.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-040-L01 | Arrays in memory | 8 |
| BEG-040-L02 | Dynamic arrays and resizing | 12 |
| BEG-040-L03 | Linked lists | 15 |
| BEG-040-L04 | Stacks | 10 |
| BEG-040-L05 | Queues | 10 |
| BEG-040-L06 | Choosing: ArrayList vs LinkedList vs ArrayDeque | 5 |
| BEG-040-L07 | Demo: building MyArrayList and watching it resize | 8 |

**Lab** — `BEG-040-LAB1` *Build your own:* `MyArrayList<T>`, `MyLinkedList<T>`, and a bracket-matching checker using your stack. Acceptance: passing tests; complexity of each method documented.

**Common mistakes:** losing the list's tail on removal; resizing by +1 instead of doubling.

**Assessment:** implementation plus 4 problems.

**Career relevance:** queues reappear as message queues (MID-026).

---

### BEG-041 · Hashing
`n: 41` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-026, BEG-040

**Learning outcomes** — the learner can:
1. Explain how a hash table maps keys to buckets.
2. Describe collision handling (chaining, open addressing) and load-factor resizing.
3. Explain why a bad `hashCode` degrades `HashMap` performance and why mutable keys break it.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-041-L01 | Hash functions | 10 |
| BEG-041-L02 | Hash tables and buckets | 12 |
| BEG-041-L03 | Collisions and resizing | 12 |
| BEG-041-L04 | Inside HashMap and HashSet | 11 |
| BEG-041-L05 | Demo: MyHashMap and the constant-hashCode slowdown | 8 |

**Lab** — `BEG-041-LAB1` *MyHashMap:* chaining-based map with resizing; then demonstrate the slowdown with a constant `hashCode`. Acceptance: tests pass; timing evidence.

**Common mistakes:** mutating a key after insertion; assuming `HashMap` iteration order.

**Assessment:** implementation plus quiz.

**Career relevance:** caching (MID-037), partitioning (MID-028), sharding (SRC-007).

---

### BEG-042 · Trees
`n: 42` · **Video:** 63 min · **Practice:** 4 h

**Prerequisites:** BEG-014, BEG-040

**Learning outcomes** — the learner can:
1. Implement a binary search tree with insert, search, and in-order traversal.
2. Perform pre-, in-, post-order, and level-order traversal.
3. Explain why an unbalanced BST degrades to O(n) and what balanced trees solve (conceptually).
4. Explain a binary heap and use `PriorityQueue`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-042-L01 | Trees and terminology | 8 |
| BEG-042-L02 | Binary search trees | 15 |
| BEG-042-L03 | Traversals | 12 |
| BEG-042-L04 | Balance (concept only) | 8 |
| BEG-042-L05 | Heaps and PriorityQueue | 12 |
| BEG-042-L06 | Demo: BST insert and traversals, step by step | 8 |

**Lab** — `BEG-042-LAB1` *BST and task scheduler:* implement a BST; then build a task scheduler using `PriorityQueue`. Acceptance: tests pass; traversal outputs correct.

**Common mistakes:** missing null checks in recursion; confusing heap with BST.

**Assessment:** implementation plus traversal exercises.

**Career relevance:** B-tree indexes (MID-012), `TreeMap` choices.

---

### BEG-043 · Graph basics
`n: 43` · **Video:** 53 min · **Practice:** 3 h

**Prerequisites:** BEG-030, BEG-042

**Learning outcomes** — the learner can:
1. Represent a graph with an adjacency list.
2. Implement BFS and DFS and choose between them.
3. Find a shortest path in an unweighted graph with BFS.
4. Recognize graph problems in real systems (dependencies, networks, routes).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-043-L01 | Graphs everywhere | 8 |
| BEG-043-L02 | Representing graphs | 10 |
| BEG-043-L03 | Breadth-first search | 12 |
| BEG-043-L04 | Depth-first search | 10 |
| BEG-043-L05 | Applications: dependencies and cycles | 5 |
| BEG-043-L06 | Demo: metro route finder with BFS | 8 |

**Lab** — `BEG-043-LAB1` *Metro route finder:* load a small metro map and find the fewest-stops route between two stations. Acceptance: correct routes; unreachable stations handled.

**Common mistakes:** forgetting a visited set (infinite loops).

**Assessment:** 3 problems.

**Career relevance:** dependency mapping (SRC-009) and service graphs.

---

### BEG-044 · Algorithmic techniques
`n: 44` · **Video:** 53 min · **Practice:** 4 h

**Prerequisites:** BEG-015, BEG-039

**Learning outcomes** — the learner can:
1. Apply two pointers to sorted-array problems.
2. Apply a sliding window to subarray/substring problems.
3. Write recursive solutions and simple backtracking (subsets, permutations).
4. Recognize which technique a new problem calls for.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-044-L01 | Two pointers | 12 |
| BEG-044-L02 | Sliding window | 12 |
| BEG-044-L03 | Thinking recursively | 10 |
| BEG-044-L04 | Backtracking | 11 |
| BEG-044-L05 | Demo: solving a problem with a sliding window | 8 |

**Lab** — `BEG-044-LAB1` *Technique drills:* 8 problems (2 per technique) with complexity stated. Acceptance: 6 of 8 correct within target complexity.

**Common mistakes:** applying two pointers to unsorted data; window bounds off by one.

**Assessment:** unseen timed problem set.

**Career relevance:** Junior technical interviews.

---

### BEG-045 · Testing fundamentals
`n: 45` · **Video:** 58 min · **Practice:** 4 h

**Prerequisites:** BEG-024, BEG-029

**Learning outcomes** — the learner can:
1. Explain why automated tests exist and what a good test case contains.
2. Write JUnit 5 tests with `@Test`, assertions, and `assertThrows`.
3. Derive test cases from boundaries and equivalence classes.
4. Run tests in the IDE and read failures.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| BEG-045-L01 | Why test automatically | 8 |
| BEG-045-L02 | Anatomy of a test case | 8 |
| BEG-045-L03 | First JUnit 5 tests | 12 |
| BEG-045-L04 | Testing exceptions | 7 |
| BEG-045-L05 | Boundaries and equivalence classes | 10 |
| BEG-045-L06 | Reading test failures | 5 |
| BEG-045-L07 | Demo: test-first on the bank's withdraw method | 8 |

**Lab** — `BEG-045-LAB1` *Test what you built:* write tests for `MyArrayList`, `MyHashMap`, and the bank's `withdraw` covering boundaries and exceptions. Acceptance: ≥ 20 meaningful tests; one bug found or a planted bug caught.

**Common mistakes:** tests with no assertions; testing only the happy path; tests that depend on each other.

**Assessment:** write tests for a provided class with hidden bugs; score = bugs caught.

**Career relevance:** JNR-043 to JNR-047 and quality engineering throughout.

> **Teaching note:** Maven is introduced in BEG-054. Until then, add JUnit through IntelliJ's library prompt; BEG-054 migrates projects to Maven.
