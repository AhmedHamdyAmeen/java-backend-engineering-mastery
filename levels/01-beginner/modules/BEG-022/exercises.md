# BEG-022 · Inheritance — Exercises and lab

## Lab
### BEG-022-LAB1 · Bank Accounts v3
**Outcomes:** 1, 2, 3 · **Time:** ~2 h
Create `SavingsAccount` (interest) and `CheckingAccount` (overdraft) extending `Account`, using `super(...)` and `@Override`. Then refactor a provided bad inheritance hierarchy into composition and write a short explanation of why.
**Acceptance:** overrides correct; refactor explained.

## Exercises (assessment: 4 exercises plus a written "is-a or has-a?" quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-022-EX01 | 1 | Create `Animal` (name, `speak()`) and `Dog extends Animal` that overrides `speak()` and calls `super(name)`. |
| BEG-022-EX02 | 2 | List what a `Dog` object gets from `Animal` and what it does not (private fields, constructors). |
| BEG-022-EX03 | 3 | Write "is-a or has-a?" for: Car/Engine, Cat/Animal, Library/Book, Square/Rectangle. |
| BEG-022-EX04 | 3 | Rewrite `class Logger extends FileWriter` as composition and explain the benefit. |

## Solutions
- **EX01**
  ```java
  class Animal { protected final String name; Animal(String name) { this.name = name; } String speak() { return "..."; } }
  class Dog extends Animal { Dog(String n) { super(n); } @Override String speak() { return "Woof"; } }
  ```
- **EX02** Gets: non-private fields and methods (private ones exist inside the object but are not accessible). Does not get: constructors; private members are not accessible.
- **EX03** has-a; is-a; has-a; Square/Rectangle: has-a is the safer answer (a square inheriting `setWidth`/`setHeight` breaks rectangle behavior, so "is-a" in maths does not mean "extends" in code).
- **EX04** `class Logger { private final FileWriter out; ... void log(String m) { out.write(m); } }`. Callers see only `log`, and the writer can be swapped.
- The written "is-a or has-a?" quiz is `quiz.md`; the Account hierarchy and override outcomes are also covered by the lab.
