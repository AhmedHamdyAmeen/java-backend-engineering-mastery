# MID-008 · Performance profiling — Exercises and lab

## Lab
### MID-008-LAB1 · Profile Shop
**Outcomes:** 1–5 · **Time:** ~4 h
The instructor plants a CPU hot spot and a lock contention in Shop. Using recordings, thread dumps, and (if needed) a heap dump, find both without reading the source first, fix them, and show before/after evidence under the same load.
**Acceptance:** written investigation log.

## Exercises (assessment: investigation of an unseen recording)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-008-EX01 | 1 | Record Shop for 2 minutes with JFR; list the five most useful pages or views and one finding from each. |
| MID-008-EX02 | 2 | From a provided flame graph, name the hottest method, its caller, and a hypothesis. |
| MID-008-EX03 | 3 | From three provided thread dumps, identify the contended lock, its owner, and the blocked threads. |
| MID-008-EX04 | 4 | From a provided heap dump, name the largest retainer and explain why it stays live. |
| MID-008-EX05 | 5 | Write a four-line investigation log entry for a fix: symptom, evidence, change, before/after. |
| MID-008-EX06 | 5 | List three ways a measurement can mislead (cold start, debug mode, single run) and how to avoid each. |

## Solutions
- **EX01** For example: Automated Analysis, Method Profiling, Memory/GC, Lock Instances, Threads; each gives a lead (hot method, allocation rate, pause, contended monitor, parked pool).
- **EX02** The widest top-level frame; its parent frame is the caller; hypothesis, for example, repeated regex or formatting per call.
- **EX03** Find the monitor address shown as "waiting to lock"; the owner is the thread with "locked" on the same address; list the blocked threads.
- **EX04** Dominator tree top entry, with the path to GC roots (typically a static or singleton field).
- **EX05** A complete entry has a measured symptom (p95 numbers), the evidence artifact, a single change, and re-measured numbers under the same load.
- **EX06** Cold start: warm up first. Debug mode: profile production-like settings. Single run: repeat and compare distributions.
