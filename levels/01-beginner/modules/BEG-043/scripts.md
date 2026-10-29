# BEG-043 · Graph basics — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a metro map with stations and lines.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-043-L01 · Graphs everywhere (8 min)
**Goal:** recognize a graph and name its parts.

**Key points**
- A **graph** is a set of **nodes** (vertices) joined by **edges** (the stations and the tracks).
- Edges can be **undirected** (two-way road) or **directed** (one-way street, "A depends on B").
- A **path** is a sequence of edges from one node to another; a **cycle** is a path that returns to its start.
- Examples: maps, social networks, web links, software dependencies, microservice calls.
- A tree is a graph with no cycles and one root.

**Show:** a small metro map with four stations and a directed "build order" graph for three libraries.

**Check:** Name two real-life graphs. *(For example roads between cities, and who follows whom.)*

---

## BEG-043-L02 · Representing graphs (10 min)
**Goal:** store a graph in code with an adjacency list.

**Key points**
- **Adjacency list**: for each node, a list of its neighbors. Best for most real graphs (few edges per node).
- **Adjacency matrix**: a grid of true/false for every pair; uses O(V²) memory, so it suits dense graphs.
- In Java: `Map<String, List<String>>`.
- For an undirected edge, add each node to the other's list.
- Use `getOrDefault` or `computeIfAbsent` so nodes with no edges still work.

**Show**
```java
Map<String, List<String>> g = new HashMap<>();
g.computeIfAbsent("A", k -> new ArrayList<>()).add("B");
g.computeIfAbsent("B", k -> new ArrayList<>()).add("A");   // undirected
```

**Check:** Which structure stores only the edges that exist? *(The adjacency list.)*

---

## BEG-043-L03 · Breadth-first search (12 min)
**Goal:** explore a graph level by level with BFS.

**Key points**
- **BFS** visits the start, then all its neighbors, then their neighbors (ripples in a pond).
- It uses a **queue**: take one from the front, add its unvisited neighbors to the back.
- Keep a **visited set**; without it, cycles cause an infinite loop.
- BFS reaches each node by the fewest edges, so it finds the shortest path in an unweighted graph.
- Cost: O(V + E), where V is the number of nodes and E the number of edges.

**Show**
```java
Queue<String> q = new ArrayDeque<>();
Set<String> visited = new HashSet<>();
q.add(start); visited.add(start);
while (!q.isEmpty()) {
    String cur = q.poll();
    for (String next : g.getOrDefault(cur, List.of()))
        if (visited.add(next)) q.add(next);
}
```

**Check:** Which structure gives BFS its level-by-level order? *(A queue.)*

---

## BEG-043-L04 · Depth-first search (10 min)
**Goal:** explore a graph deeply with DFS and choose between DFS and BFS.

**Key points**
- **DFS** goes as deep as possible along one path, then backs up (walking a maze).
- It uses recursion (the call stack) or an explicit stack, plus a visited set.
- Also O(V + E).
- Use BFS for the fewest steps; use DFS to explore everything, detect cycles, or order dependencies.
- DFS does not guarantee the shortest path.

**Show**
```java
void dfs(String node, Set<String> visited) {
    if (!visited.add(node)) return;
    for (String next : g.getOrDefault(node, List.of())) dfs(next, visited);
}
```

**Check:** You need the route with the fewest stops. BFS or DFS? *(BFS.)*

---

## BEG-043-L05 · Applications: dependencies and cycles (5 min)
**Goal:** see graph thinking in real systems.

**Key points**
- Build tools and services form a directed graph: "A needs B".
- A **cycle** in dependencies ("A needs B, B needs A") means no valid build order.
- DFS can detect a cycle: meeting a node that is still on the current path.
- Networks and routes: BFS answers "how many hops".
- This returns later in dependency mapping and service graphs.

**Show:** libraries A -> B -> C -> A; point out the cycle and say a build cannot start.

**Check:** What does a cycle in a dependency graph mean? *(There is no valid order to build or start them.)*

---

## BEG-043-L06 · Demo: metro route finder with BFS (8 min)
**Goal:** find the route with the fewest stops between two stations. Prepares BEG-043-LAB1.

**Steps**
1. Build a small metro map as an adjacency list (8 stations, two lines crossing at one station).
2. Write `findRoute(start, goal)` with a queue and a visited set.
3. **Planned mistake:** leave out the visited set; run it on a map with a loop and watch it never finish. Fix by marking nodes visited when added to the queue.
4. Store the previous station for each visited one in a `Map`, then walk back from the goal to rebuild the route.
5. Test a normal route and an unreachable station (return an empty list, not an error).
6. Print the route and the number of stops.

**Check:** How do we rebuild the route after BFS finds the goal? *(Follow the "came from" map backward and reverse it.)*
