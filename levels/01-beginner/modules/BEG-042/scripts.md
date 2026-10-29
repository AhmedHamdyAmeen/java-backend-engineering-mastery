# BEG-042 · Trees — Lecture scripts

**Video:** 63 min · **Analogy used throughout:** a family tree and a company org chart.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-042-L01 · Trees and terminology (8 min)
**Goal:** name the parts of a tree.

**Key points**
- A tree is nodes connected by links, with no cycles (an org chart).
- The **root** is the top node; a **parent** has **children**; a **leaf** has none.
- The **height** is the number of links on the longest path from the root down to a leaf.
- A **subtree** is any node with everything below it; this makes trees recursive.
- A **binary tree** gives each node at most two children: left and right.

**Show:** a tree with root 8, children 3 and 10, and 3's children 1 and 6; label root, parent, leaf, height (2).

**Check:** How many children can a node of a binary tree have at most? *(Two.)*

---

## BEG-042-L02 · Binary search trees (15 min)
**Goal:** insert into and search a binary search tree (BST).

**Key points**
- BST rule: for every node, smaller values are in the left subtree and larger values in the right.
- **Search**: compare with the node; go left if smaller, right if larger; stop when equal or `null`.
- **Insert**: search for the place where the value would be and attach a new node there.
- On a reasonably balanced tree, each step discards about half the nodes: O(log n).
- Always check for `null` first in recursive code.

**Show**
```java
Node insert(Node n, int v) {
    if (n == null) return new Node(v);
    if (v < n.value) n.left = insert(n.left, v);
    else if (v > n.value) n.right = insert(n.right, v);
    return n;
}
```

**Check:** Where does 5 go in the tree 8 / 3 / 10? *(Left of 8, then right of 3.)*

---

## BEG-042-L03 · Traversals (12 min)
**Goal:** visit every node in four standard orders.

**Key points**
- **Pre-order**: node, left, right. **In-order**: left, node, right. **Post-order**: left, right, node.
- In-order on a BST gives the values in sorted order.
- **Level-order** visits row by row using a queue (breadth first).
- The first three are short recursive methods; level-order is a loop with a queue.
- Every traversal visits each node once: O(n).

**Show:** for the tree 8 / (3 / (1, 6)) / 10: in-order 1 3 6 8 10; pre-order 8 3 1 6 10; post-order 1 6 3 10 8; level-order 8 3 10 1 6.

**Check:** Which traversal prints a BST in sorted order? *(In-order.)*

---

## BEG-042-L04 · Balance (concept only) (8 min)
**Goal:** explain why balance matters, without implementing it.

**Key points**
- Insert 1, 2, 3, 4, 5 in order into a BST and you get a chain, not a tree.
- A chain has height n, so search is O(n), no better than a list.
- A **balanced** tree keeps its height near log n by rearranging (rotating) nodes on insert and delete.
- Self-balancing trees (AVL, red-black) do this automatically. Java's `TreeMap` and `TreeSet` use a red-black tree.
- Database indexes use a related structure, the B-tree.

**Show:** two drawings of the same values 1 to 5: a straight chain (height 4) and a bushy tree (height 2).

**Check:** Why can a BST become O(n)? *(Sorted inserts make a chain, so the height is n.)*

---

## BEG-042-L05 · Heaps and PriorityQueue (12 min)
**Goal:** explain a binary heap and use `PriorityQueue`.

**Key points**
- A **min-heap** is a tree where every parent is smaller than or equal to its children, so the smallest item is at the root.
- A heap is not a BST: it does not keep left smaller than right, and it is not sorted.
- Peek at the smallest: O(1). Add or remove the smallest: O(log n).
- `PriorityQueue` in Java is a min-heap by default; pass a `Comparator` to change the order.
- Uses: schedulers ("most urgent first"), top-k, shortest-path algorithms.

**Show**
```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.add(5); pq.add(1); pq.add(3);
pq.poll();   // 1
pq.poll();   // 3
```

**Check:** Does iterating a `PriorityQueue` give sorted order? *(No; only `poll()` gives items in order.)*

---

## BEG-042-L06 · Demo: BST insert and traversals, step by step (8 min)
**Goal:** build a BST by hand and in code and print all four traversals. Prepares BEG-042-LAB1.

**Steps**
1. Draw the BST after inserting 8, 3, 10, 1, 6, 14 one at a time.
2. Write `Node` and `insert` (recursive).
3. **Planned mistake:** omit the `n == null` check in `insert`; run it and show the `NullPointerException`. Fix by adding the base case first.
4. Write `inOrder`, `preOrder`, `postOrder`; print and compare with the drawing.
5. Write `levelOrder` with an `ArrayDeque` queue.
6. Insert 1 to 6 in order and print the height to show the chain problem.

**Check:** What is the in-order output after inserting 8, 3, 10, 1, 6, 14? *(1 3 6 8 10 14.)*
