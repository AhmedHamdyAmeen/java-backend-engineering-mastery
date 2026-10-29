# BEG-027 · Packages and organization — Exercises and lab

## Lab
### BEG-027-LAB1 · Bank Accounts v5
**Outcomes:** 1, 2, 3 · **Time:** ~1.5 h
Reorganize Bank Accounts into feature packages (account, customer, notification) with a minimal public surface. Write two sentences justifying feature over layer packaging.
**Acceptance:** only intended classes are `public`.

## Exercises (assessment: refactoring exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-027-EX01 | 1 | Give the folder path and `package` line for class `Invoice` in package `com.acme.billing`. |
| BEG-027-EX02 | 1 | Fix the clash: your code needs both `java.util.Date` and `java.sql.Date`. |
| BEG-027-EX03 | 2 | A class `RateTable` is used only by `Account`. Which modifier should it have and why? |
| BEG-027-EX04 | 3 | Group these into packages by feature: `OrderController`, `OrderService`, `OrderRepository`, `UserController`, `UserService`. |
| BEG-027-EX05 | 1, 2, 3 | Refactoring exercise: take a provided project in the default package and reorganize it with a small public surface. |

## Solutions
- **EX01** `com/acme/billing/Invoice.java` with `package com.acme.billing;`.
- **EX02** Import one (`import java.util.Date;`) and write `java.sql.Date` in full where needed.
- **EX03** Package-private (no modifier): only its package needs it, and hiding it keeps the public surface small.
- **EX04** `order/` (the three Order classes) and `user/` (`UserController`, `UserService`). Justification: related code together, helpers can be package-private.
- **EX05** Graded on: correct `package` lines and folders, compiles and runs, helpers package-private, no use of the default package.
