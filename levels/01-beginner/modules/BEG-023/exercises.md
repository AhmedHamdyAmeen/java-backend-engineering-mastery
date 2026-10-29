# BEG-023 · Polymorphism — Exercises and lab

## Lab
### BEG-023-LAB1 · Month-end processing
**Outcomes:** 1, 2, 3 · **Time:** ~2 h
Apply month-end rules to a mixed list of accounts (savings: interest, checking: fee) with a single loop and no type checks. Then add a third account type.
**Acceptance:** adding a new account type requires no change to the loop.

## Exercises (assessment: "predict the output" quiz on 8 snippets)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-023-EX01 | 1 | `Animal a = new Dog(); a.speak();` where `Dog` overrides `speak`. Which runs and why? |
| BEG-023-EX02 | 2 | Put a `Dog`, `Cat`, and `Cow` in a `List<Animal>` and call `speak()` on each. |
| BEG-023-EX03 | 2 | Explain why `Animal a = new Dog(); a.fetch();` does not compile when only `Dog` has `fetch()`. |
| BEG-023-EX04 | 3 | Refactor `if (shape.type.equals("CIRCLE")) ... else if (...)` area code into polymorphism. |
| BEG-023-EX05 | 1 | Predict: `Animal a = new Cat(); Dog d = (Dog) a;` What happens? |
| BEG-023-EX06 | 1, 2 | Predict the output of the eight snippets in the "predict the output" quiz (see `quiz.md` for a sample). |

## Solutions
- **EX01** `Dog.speak` runs: the method is chosen by the real object at run time.
- **EX02** `for (Animal x : animals) x.speak();` each prints its own sound.
- **EX03** The compiler checks the reference type `Animal`, which has no `fetch`. Use `instanceof Dog d` and `d.fetch()` or add it to the parent if it truly belongs.
- **EX04** Add `abstract double area()` (or a normal method) to `Shape`; `Circle` and `Square` override it; callers use `shape.area()`.
- **EX05** Compiles, then throws `ClassCastException` at run time.
- **EX06** Answers for the eight snippets are given by the instructor; apply the reference-type-checks, object-type-runs rule. Pass at least six.
