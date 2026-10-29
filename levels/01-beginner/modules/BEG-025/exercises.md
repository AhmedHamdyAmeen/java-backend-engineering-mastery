# BEG-025 · Relationships — Exercises and lab

## Lab
### BEG-025-LAB1 · Bank Accounts v4
**Outcomes:** 1, 2, 3 · **Time:** ~1.5 h
Draw the UML diagram first: `Customer` owns many `Account`s; each `Account` has many `Transaction`s (composition). Then implement it. Name each relationship type in a note.
**Acceptance:** diagram matches code.

## Exercises (assessment: diagram-from-description exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-025-EX01 | 1 | Classify: (a) Order has OrderLines, (b) Team has Players, (c) Printer used by a method parameter, (d) Student attends Course. |
| BEG-025-EX02 | 1 | Give Java code that shows aggregation and code that shows composition. |
| BEG-025-EX03 | 2 | Diagram from description: "A library has many books. A member can borrow many books; a book is borrowed by at most one member at a time. Each loan has a date." |
| BEG-025-EX04 | 3 | Implement `Customer` with a `List<Account>` and `openAccount` / `accounts()` that does not expose the list. |
| BEG-025-EX05 | 2, 3 | Spot the problem: `Customer` and `Account` each hold the other, but `Account` is never given its customer. Fix it. |

## Solutions
- **EX01** (a) composition; (b) aggregation; (c) dependency; (d) association. Aggregation versus association can be debated; justification matters.
- **EX02** Aggregation: a `Team` receives existing `Player` objects in `add(Player p)`. Composition: an `Order` creates its `OrderLine` objects internally and never shares the list.
- **EX03** Boxes: Library, Book, Member, Loan. `Library 1 ◇— * Book`; `Member 1 — * Loan`; `Book 1 — 0..* Loan` (only one open at a time); Loan holds the date. Judged on correct multiplicities.
- **EX04** `public List<Account> accounts() { return List.copyOf(accounts); }` and `openAccount` creates and adds.
- **EX05** Set both sides in one method (`openAccount` creates the account with `this` as owner), or remove the back reference if no one needs it.
- Outcomes 2 and 3 are also covered by the lab.
