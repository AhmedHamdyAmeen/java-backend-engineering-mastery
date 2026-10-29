# BEG-038 · Java memory basics — Exercises and lab

## Lab
### BEG-038-LAB1 · Draw it
**Outcomes:** 1–3 · **Time:** ~1 h
Draw memory diagrams (stack frames, local variables, heap objects) for four short programs: primitive copy, object aliasing, a method that mutates a parameter, and an object that becomes unreachable. Confirm each with the debugger.
**Acceptance:** diagrams match observed values.

## Exercises (assessment: diagram quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-038-EX01 | 1 | Draw the stack and heap for `int x = 5; int y = x; y = 6; StringBuilder sb = new StringBuilder("a");` and state `x`. |
| BEG-038-EX02 | 2 | Given `StringBuilder a = new StringBuilder("hi"); StringBuilder b = a; b.append("!");` predict `a`, and explain. |
| BEG-038-EX03 | 2 | A method `void add(List<String> l) { l.add("z"); }` is called with a list. Does the caller's list change? Explain. |
| BEG-038-EX04 | 3 | Mark the moment the object becomes eligible for GC: `Person p = new Person(); p = new Person();`. |
| BEG-038-EX05 | 3 | Explain in two sentences why `System.gc()` does not guarantee anything. |

## Solutions
- **EX01** `x` is 5; `y` is 6 (copied by value). `sb` in the frame points to a heap `StringBuilder`.
- **EX02** `a` is "hi!": `b` is another reference to the same object.
- **EX03** Yes. The method receives a copy of the reference, pointing to the same list.
- **EX04** After the second assignment, the first `Person` has no references and is eligible.
- **EX05** It only suggests a collection; the JVM decides when and whether it runs, and garbage is collected automatically when unreachable.
- The four-program diagram work in the lab and the diagram quiz (`quiz.md`) cover outcome 1 as well.
