# BEG-035 · Functional basics — Exercises and lab

## Lab
### BEG-035-LAB1 · Filters
**Outcomes:** 1–3 · **Time:** ~1.5 h
Rewrite anonymous `Comparator` classes and custom filter loops using lambdas and method references. Keep a before/after copy.
**Acceptance:** same behavior, less code.

## Exercises (assessment: four exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-035-EX01 | 1 | Convert an anonymous `Runnable` that prints "hello" into a lambda; explain which interface it implements. |
| BEG-035-EX02 | 2 | Write one lambda for each: `Predicate<Integer>` (even), `Function<String,Integer>` (length), `Consumer<String>` (print upper-case), `Supplier<String>` ("ready"), `BiFunction<Integer,Integer,Integer>` (max). |
| BEG-035-EX03 | 3 | Rewrite as method references: `s -> s.toUpperCase()`, `s -> System.out.println(s)`, `() -> new ArrayList<String>()`. |
| BEG-035-EX04 | 1 | Write `filter(List<Integer>, Predicate<Integer>)` returning a new list; use it for positives and for numbers over 100. |

## Solutions
- **EX01** `Runnable r = () -> System.out.println("hello");` It implements `Runnable`, whose single method is `run`.
- **EX02** `n -> n % 2 == 0`; `s -> s.length()`; `s -> System.out.println(s.toUpperCase())`; `() -> "ready"`; `(a, b) -> Math.max(a, b)`.
- **EX03** `String::toUpperCase`; `System.out::println`; `ArrayList::new` (as `Supplier<List<String>>`).
- **EX04** Loop, `if (p.test(x)) result.add(x);`. Calls: `filter(list, n -> n > 0)`, `filter(list, n -> n > 100)`.
- Mistakes (long lambdas, captured variables) are covered in L02 and demo L05.
