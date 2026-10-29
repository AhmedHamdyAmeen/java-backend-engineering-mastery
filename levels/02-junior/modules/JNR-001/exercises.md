# JNR-001 · Modern Java — Exercises and lab

## Lab
### JNR-001-LAB1 · Shop Core v1
**Outcomes:** 2–4 · **Time:** ~2.5 h
Model `Product`, `Money`, and `CartLine` as records with validation in compact constructors. Model `Discount` as a sealed hierarchy (percentage, fixed amount, buy-X-get-Y) and price a cart line with an exhaustive `switch`.
**Acceptance:** no setters anywhere; adding a new discount type causes a compile error until the switch handles it; no `default` branch.

## Exercises (assessment: refactor a legacy POJO-heavy module and justify each change, plus seven exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-001-EX01 | 1 | Explain in three sentences the six-month cadence, what LTS means, and which version you would choose for a new production service and why. |
| JNR-001-EX02 | 2 | Rewrite a `Customer` class (name, email, getters, setters, equals, hashCode, toString) as a record. Reject a blank name. |
| JNR-001-EX03 | 2 | A record has a `List<String> tags` component. Show how a caller can break it and fix it. |
| JNR-001-EX04 | 3 | Declare a sealed interface `PaymentMethod` with `Card`, `Cash`, `Voucher`. Write a switch returning a fee for each. |
| JNR-001-EX05 | 3 | Add `Transfer` to `PaymentMethod` without touching the switch. What happens? Why is `default` harmful here? |
| JNR-001-EX06 | 4 | Rewrite a chain of `if (o instanceof X) { X x = (X) o; ... }` with pattern matching, and a concatenated JSON string with a text block. |
| JNR-001-EX07 | 4 | Use a record pattern to print `Money(cents, currency)` from an `Object` using `instanceof`. |

## Solutions
- **EX01** Releases every six months (March, September); LTS gets years of support; pick the current LTS, because it is patched for a long time (verify the version).
- **EX02** `record Customer(String name, String email) { Customer { if (name == null || name.isBlank()) throw new IllegalArgumentException("name"); } }`.
- **EX03** The caller keeps the original list and changes it. Fix: `tags = List.copyOf(tags);` in the compact constructor.
- **EX04** `sealed interface PaymentMethod permits Card, Cash, Voucher {}` (records); `switch (m) { case Card c -> ...; case Cash c -> ...; case Voucher v -> ...; }`.
- **EX05** The code fails to compile: the switch is not exhaustive. With `default`, it would compile and silently use the wrong fee.
- **EX06** `if (o instanceof Product p) { ... p.name() ... }`; a text block with three quotes and no escaped quotes.
- **EX07** `if (o instanceof Money(long cents, String currency)) { System.out.println(cents + " " + currency); }`.
- Outcome 1 is also covered by quiz Q01–Q03; the lab covers outcomes 2–4.
