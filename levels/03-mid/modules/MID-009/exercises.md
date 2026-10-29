# MID-009 · Advanced generics and reflection — Exercises and lab

## Lab
### MID-009-LAB1 · Audit annotation
**Outcomes:** 3–4 (with 1–2 in exercises) · **Time:** ~2.5 h
Create an `@Audited` annotation and a proxy-based interceptor that logs calls to annotated methods (method name, arguments, duration). Apply it to a Shop service interface. Demonstrate the self-invocation limitation.
**Acceptance:** works through an interface; self-invocation limitation demonstrated.

## Exercises (assessment: exercises plus a proxy-behavior quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-009-EX01 | 1 | Show that `new ArrayList<String>().getClass() == new ArrayList<Integer>().getClass()`; explain, then use a raw list to cause heap pollution and observe where the exception appears. |
| MID-009-EX02 | 1 | Write `<T> T create(Class<T>)` as the replacement for `new T()`. |
| MID-009-EX03 | 2 | Write `addAll(Collection<? extends T> src, Collection<? super T> dst)`; explain PECS with `Integer`, `Number`, `Object`. |
| MID-009-EX04 | 3 | Use reflection to list all methods annotated with a custom `@Audited` on a class. |
| MID-009-EX05 | 4 | Explain why `@Transactional` on `b()` does not work when called from `a()` in the same class, and give two fixes. |
| MID-009-EX06 | 3 | Time 1,000,000 direct vs reflective calls; report the difference and one way to reduce it. |

## Solutions
- **EX01** Both classes are `ArrayList` (erased). Adding an `Integer` through a raw reference compiles with a warning; `ClassCastException` appears later when a `String` is read.
- **EX02** `return type.getDeclaredConstructor().newInstance();`
- **EX03** `Collection<Integer>` can be copied into `Collection<Number>` or `Collection<Object>`: source extends, destination super.
- **EX04** `Arrays.stream(c.getDeclaredMethods()).filter(m -> m.isAnnotationPresent(Audited.class))` with `RUNTIME` retention.
- **EX05** The call is on `this`, bypassing the Spring proxy. Move `b()` to another bean, or inject the proxy (self-injection with care) or restructure.
- **EX06** Reflection is slower, mostly warm-up-dependent; cache `Method` objects or use `MethodHandle`/direct calls.
