# MID-004 · Thread safety — Exercises and lab

## Lab
### MID-004-LAB1 · Stock counter
**Outcomes:** 1–4 · **Time:** ~4 h
Take an in-memory stock counter with a check-then-act race. Write a stress test that fails. Fix it three ways: (1) a lock (`synchronized` or `ReentrantLock`), (2) `AtomicInteger` with compare-and-set, (3) an immutable snapshot swapped through `AtomicReference`. Compare correctness, throughput, and code clarity.
**Acceptance:** a stress test fails before and passes after each fix.

## Exercises (assessment: five snippets with concurrency bugs)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-004-EX01 | 1 | Snippet: lazy singleton `if (inst == null) inst = new X();`. Identify the race and fix it. |
| MID-004-EX02 | 1 | Snippet: `if (!map.containsKey(k)) map.put(k, v)` on a `synchronizedMap`. Explain the bug and fix it. |
| MID-004-EX03 | 2 | Snippet: a plain `boolean stop` flag read in a loop. Explain the visibility problem and fix it. |
| MID-004-EX04 | 4 | Snippet: a `@Service` with a `List<Order>` field. Explain the risk and two redesigns. |
| MID-004-EX05 | 4 | Snippet: two methods locking `a` then `b`, and `b` then `a`. Show the deadlock and the fix. |

## Solutions
- **EX01** Two threads can both see null. Fix with a holder class, an enum, `synchronized`, or `volatile` plus double-checked locking.
- **EX02** The check and put are separate; use `ConcurrentHashMap.putIfAbsent` or `computeIfAbsent`.
- **EX03** Without a happens-before edge the loop may never see the write; make the flag `volatile` (or use interruption).
- **EX04** One shared instance across requests; make it stateless, pass data as parameters, or use a thread-safe structure or per-request object.
- **EX05** Thread 1 holds `a` waiting for `b`; thread 2 the reverse. Always lock in one order (for example by id).
- Outcome 3 (choice of tool) is covered by the lab's three fixes and Q05-Q08 (including `volatile` with `++`, which needs an atomic).
