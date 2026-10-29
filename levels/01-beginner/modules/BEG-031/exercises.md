# BEG-031 · Generics — Exercises and lab

## Lab
### BEG-031-LAB1 · Generic repository
**Outcomes:** 1–3 · **Time:** ~2 h
Write `InMemoryRepository<T, ID>` with `save`, `findById`, `findAll`, `delete`. Use it for two different types (for example `Contact` and `Event`). Show one line that fails to compile when the wrong type is saved.
**Acceptance:** no casts; compile-time type safety demonstrated.

## Exercises (assessment: four exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-031-EX01 | 1 | Explain in two sentences what goes wrong with a raw `List` holding mixed types, and how `List<String>` fixes it. |
| BEG-031-EX02 | 2 | Write `Pair<A, B>` with a constructor and getters; create `Pair<String, Integer>`. |
| BEG-031-EX03 | 2, 3 | Write `static <T extends Comparable<T>> T max(List<T> list)`. |
| BEG-031-EX04 | 3 | Write `static double sum(List<? extends Number> nums)` and call it with `List<Integer>` and `List<Double>`. |

## Solutions
- **EX01** A raw list accepts anything, so a bad element is found only when a cast fails at runtime. `List<String>` makes the compiler reject non-strings and removes the cast.
- **EX02** `class Pair<A,B>{ private final A first; private final B second; Pair(A a,B b){first=a;second=b;} A getFirst(){return first;} B getSecond(){return second;} }`
- **EX03** Loop keeping `best`; replace it when `item.compareTo(best) > 0`. Return `best`.
- **EX04** `double total = 0; for (Number n : nums) total += n.doubleValue(); return total;`
- The common mistakes (raw types, `new T()`) are covered in demo L06; the lab covers outcomes 1–2 as well.
