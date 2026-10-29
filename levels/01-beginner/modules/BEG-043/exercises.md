# BEG-043 · Graph basics — Exercises and lab

## Lab
### BEG-043-LAB1 · Metro route finder
**Outcomes:** 1–4 · **Time:** ~3 h
1. Load a small metro map (a text file of "station-station" lines) into an adjacency list.
2. Implement BFS that returns the fewest-stops route between two stations.
3. Handle unknown and unreachable stations without crashing.
4. Add a DFS "can I get there at all" check and say when you would use it instead of BFS.
**Acceptance:** correct routes; unreachable stations handled.

## Exercises (assessment: 3 problems)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-043-EX01 | 1 | Write the adjacency list for edges A-B, A-C, B-D, C-D, D-E (undirected). |
| BEG-043-EX02 | 2 | Write the BFS visiting order from A for the graph in EX01 (visit neighbors in alphabetical order). |
| BEG-043-EX03 | 2 | Write the DFS visiting order from A for the same graph, same neighbor order. |
| BEG-043-EX04 | 3 | Using BFS, give the shortest path from A to E and its number of edges. |
| BEG-043-EX05 | 4 | Name the nodes and edges of: a course prerequisite plan; a social network; a map of airports and flights. Say whether each is directed. |
| BEG-043-EX06 | 2 | Explain what happens if BFS has no visited set on a graph with a cycle. |

## Solutions
- **EX01** A: [B, C]; B: [A, D]; C: [A, D]; D: [B, C, E]; E: [D].
- **EX02** A, B, C, D, E.
- **EX03** A, B, D, C, E (A -> B -> D -> C, back to D -> E).
- **EX04** A -> B -> D -> E (or via C), 3 edges.
- **EX05** Prerequisites: courses are nodes, "needs" are directed edges. Social network: people are nodes; "friend" is undirected, "follows" is directed. Airports: nodes airports, edges flights, usually directed.
- **EX06** It keeps re-adding the same nodes around the cycle and never finishes (an infinite loop or a memory error).
