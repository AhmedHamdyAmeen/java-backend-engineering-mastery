# JNR-003 · Code quality — Exercises and lab

## Lab
### JNR-003-LAB1 · Clean the checkout
**Outcomes:** 1–4 · **Time:** ~2.5 h
Refactor a provided 300-line `CheckoutService` that already has tests. Rename, extract methods and classes, remove duplication, and replace primitives with small types.
**Acceptance:** tests stay green throughout; each commit is one named refactoring (for example "Extract calculateTax"); no behavior change.

## Exercises (assessment: smell-spotting review of an unseen class with proposed refactorings, plus six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-003-EX01 | 1 | Rename `int d(int a, int b)`, `boolean f`, and `class DataManager` so they show intent. Invent a context first. |
| JNR-003-EX02 | 1 | Rewrite a name that uses `get`, `fetch`, and `retrieve` for the same idea so it uses one word. |
| JNR-003-EX03 | 2 | A class `Order` sends emails, saves to a database, and calculates tax. Describe its cohesion and coupling problems. |
| JNR-003-EX04 | 2 | Reduce coupling: change `OrderService` from `new SmtpMailer()` to depending on an interface. |
| JNR-003-EX05 | 3 | Give an example where removing duplication (DRY) makes code harder to read (KISS). Say what you would do. |
| JNR-003-EX06 | 4 | Match each smell to its refactoring: long method, feature envy, primitive obsession, duplicated logic, large class. |
| JNR-003-EX07 | 4 | Do an Extract Method with the IDE on a given block, run the tests, and name the commit. |

## Solutions
- **EX01** Example: `int totalQuantity(int cartA, int cartB)`, `boolean isPaid`, `class PriceCalculator`.
- **EX02** Choose one verb, for example `find`, and use it everywhere.
- **EX03** Low cohesion (three unrelated jobs); high coupling to mail, database, and tax code. Split into three classes.
- **EX04** `private final Mailer mailer;` set in the constructor; `Mailer` is an interface with `SmtpMailer` implementing it.
- **EX05** Two methods that look alike are merged with a boolean flag and branches. Leave the duplication until the third case or the real shared idea is clear.
- **EX06** Long method -> Extract Method; feature envy -> Move Method; primitive obsession -> introduce a record; duplicated logic -> Extract Method; large class -> Extract Class.
- **EX07** Select the block, Extract Method, name it by intent, run the tests; commit "Extract calculateShipping".
- Outcome 4 is also covered by the assessment review and quiz Q07–Q10.
