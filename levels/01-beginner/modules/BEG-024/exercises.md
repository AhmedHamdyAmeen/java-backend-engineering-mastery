# BEG-024 · Abstract classes and interfaces — Exercises and lab

## Lab
### BEG-024-LAB1 · Notification channels
**Outcomes:** 1, 3 · **Time:** ~2 h
Create a `Notifier` interface with Email, SMS, and Console implementations. The bank sends statements through any `Notifier`. Add one test or `main` that runs the same statement through all three.
**Acceptance:** the bank class depends only on the interface.

## Exercises (assessment: 4 exercises plus a design question)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-024-EX01 | 1 | Declare `Shape` with `double area()` and implement it in `Circle` and `Rectangle`. |
| BEG-024-EX02 | 2 | Write an abstract `Employee` with name, a constructor, and `abstract double pay()`; implement `Salaried` and `Hourly`. |
| BEG-024-EX03 | 4 | Add a `default String describe()` to `Shape` that returns `"Area: " + area()`. Name one risk of default methods. |
| BEG-024-EX04 | 3 | Interface or abstract class? (a) `Flyable` for birds and planes, (b) a base `Vehicle` with shared `speed` and `fuel` fields. |
| BEG-024-EX05 | 3 | Design question: a report system must export to PDF, CSV, and later more formats. Sketch the types and justify interface vs abstract class. |

## Solutions
- **EX01** `interface Shape { double area(); }`; `Circle` returns `Math.PI * r * r`; `Rectangle` returns `w * h`.
- **EX02** `abstract class Employee { protected final String name; Employee(String n) { name = n; } abstract double pay(); }` with two subclasses overriding `pay`.
- **EX03** `default String describe() { return "Area: " + area(); }`. Risk: conflicts when two interfaces define the same default, and logic hidden in interfaces.
- **EX04** (a) interface (unrelated types share a capability); (b) abstract class (shared state).
- **EX05** `interface ReportExporter { void export(Report r); }` with `PdfExporter`, `CsvExporter`; add an abstract helper only if they share real code. New formats are new classes.
- Outcome 1 is also covered by the lab.
