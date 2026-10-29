# BEG-028 · OOP design practice — Exercises and lab

## Lab
### BEG-028-LAB1 · Parking garage
**Outcomes:** 1, 2, 3, 4 · **Time:** ~6 h
Model and implement a garage with levels, spot sizes, vehicles, tickets, and fees. Produce a UML diagram, working code, and a half-page design rationale covering key decisions and trade-offs. Complete a peer review of another learner's design (and receive one).
**Acceptance:** UML + code + a half-page design rationale; peer review completed.

## Exercises (assessment: design review using the rubric in `assessment/framework.md`, design dimension)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-028-EX01 | 1 | From the text "A cinema has screens; each screen shows movies at times; customers buy tickets for a showing", list classes, relationships, and one invariant. |
| BEG-028-EX02 | 2 | Decide which class should own: `isSoldOut()`, `price()`, `canFit(vehicle)`. Justify each. |
| BEG-028-EX03 | 3 | Given a `ShopManager` with 12 methods (pricing, stock, email, file saving), propose a split. |
| BEG-028-EX04 | 4 | Write a five-line rationale for your cinema design including one rejected alternative. |
| BEG-028-EX05 | 1, 2 | Spot the premature inheritance: a `Vehicle` hierarchy with `Car`, `Truck`, `ElectricTruck`, `OldTruck` where the subclasses differ only by one number. Propose a simpler model. |

## Solutions
- **EX01** Classes: `Cinema`, `Screen`, `Movie`, `Showing`, `Customer`, `Ticket`. `Cinema 1—* Screen`, `Screen 1—* Showing`, `Showing *—1 Movie`, `Ticket *—1 Showing`. Invariant: a showing cannot sell more tickets than its seats.
- **EX02** `Showing.isSoldOut()` (knows seats sold); `Showing`/a `PricePolicy` for `price()`; `Spot.canFit(vehicle)` (knows its size). Rule: the class with the data does the work.
- **EX03** For example `PriceCalculator`, `StockLevel`/`Inventory`, `EmailNotifier`, `ShopRepository`, leaving `Shop` as a thin coordinator.
- **EX04** Should name classes, a main decision (e.g., fee as a separate policy for easy change), and a rejected option with its trade-off.
- **EX05** One `Vehicle` class with a size/`VehicleType` field (or a small enum). Inheritance is not needed when only data differs.
- The lab is graded with the design dimension of the rubric in `assessment/framework.md`.
