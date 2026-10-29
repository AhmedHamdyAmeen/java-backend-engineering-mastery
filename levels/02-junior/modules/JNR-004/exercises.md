# JNR-004 · SOLID principles — Exercises and lab

## Lab
### JNR-004-LAB1 · Pluggable pricing
**Outcomes:** 1–4 · **Time:** ~2 h
Refactor Shop Core so tax rules and payment providers are injected through interfaces. Add a new tax rule without modifying existing classes. Write a fake payment provider for tests.
**Acceptance:** core has no dependency on concrete providers; a new tax rule is added by adding a class only; tests run without a network.

## Exercises (assessment: design quiz with code snippets plus the lab; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-004-EX01 | 1 | State each SOLID letter in one sentence each. |
| JNR-004-EX02 | 1 | A `ReportService` queries a database, formats a PDF, and emails it. Which principle does it break? |
| JNR-004-EX03 | 2 | Refactor `if (type.equals("PERCENT")) ... else if (type.equals("FIXED")) ...` so a new type needs no edit to existing code. |
| JNR-004-EX04 | 1 | A `ReadOnlyList extends MyList` throws `UnsupportedOperationException` in `add`. Which principle is broken and how do you fix it? |
| JNR-004-EX05 | 3 | Make `CheckoutService` depend on a `PaymentProvider` interface and test it with a fake. |
| JNR-004-EX06 | 4 | Give an example where an interface with a single implementation is needless. Say what you would do instead. |

## Solutions
- **EX01** S: one reason to change. O: extend without editing. L: subtypes work wherever the parent does. I: small, focused interfaces. D: depend on interfaces, not concrete classes.
- **EX02** SRP. Split into `ReportQuery`, `PdfFormatter`, `ReportMailer`.
- **EX03** Introduce `interface Discount { Money apply(Money p); }` with a class per type; a new type is a new class (OCP).
- **EX04** LSP. Do not inherit; separate `ReadableList` and `MutableList` interfaces (ISP helps too).
- **EX05** `CheckoutService(PaymentProvider p)`; test with `class FakePayments implements PaymentProvider { ... }` returning a fixed receipt.
- **EX06** A `PriceFormatter` interface with only one class and no test need. Use the class directly; extract an interface when a second implementation or test double is needed.
- The assessment design quiz covers outcome 1 and 4 further; outcomes 2–3 are covered by the lab.
