# BEG-037 · Optional — Exercises and lab

## Lab
### BEG-037-LAB1 · Safe lookups
**Outcomes:** 1–3 · **Time:** ~1 h
Change `findById` in the generic repository (BEG-031) to return `Optional` and update all callers.
**Acceptance:** no `.get()` without a check.

## Exercises (assessment: three exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-037-EX01 | 1 | Write `Optional<String> firstLongWord(List<String> words, int min)` that returns the first word with at least `min` letters. |
| BEG-037-EX02 | 2 | Given `Optional<String> name`, print it upper-cased or "guest", and write a second version that throws `IllegalStateException("name missing")`. |
| BEG-037-EX03 | 3 | Fix these: a class with an `Optional<String>` field, a method with an `Optional<Integer>` parameter, a method returning `Optional<List<Order>>`. |

## Solutions
- **EX01** `for (String w : words) if (w.length() >= min) return Optional.of(w); return Optional.empty();` (or a stream with `filter(...).findFirst()`).
- **EX02** `name.map(String::toUpperCase).orElse("guest")`; `name.orElseThrow(() -> new IllegalStateException("name missing"))`.
- **EX03** Make the field a plain `String` (possibly null, documented) or keep it as a normal value; take a plain `Integer`/`int` or use overloads; return `List<Order>` and an empty list when nothing is found.
- Outcome 1 is also covered by the lab and quiz Q01–Q03.
