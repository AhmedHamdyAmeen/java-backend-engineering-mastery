# BEG-021 · Encapsulation — Exercises and lab

## Lab
### BEG-021-LAB1 · Bank Accounts v2
**Outcomes:** 1, 2, 3, 4 · **Time:** ~2 h
Make the fields of `Account` private. Enforce invariants (balance never negative, amounts positive) in the constructor and `withdraw`. Replace `setBalance` with behavior methods. Add an immutable `Money` class (final fields, no setters).
**Acceptance:** no way to reach an invalid state from outside the class.

## Exercises (assessment: code review exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-021-EX01 | 1 | Which of `private`, package-private, `protected`, `public` would you use for: a helper method, a field, a service method called from other packages, a method meant for subclasses? |
| BEG-021-EX02 | 2 | Add the rule "age is between 0 and 150" to a `Person` class so it cannot be broken. |
| BEG-021-EX03 | 3 | Rewrite `if (c.getItems() > 0) c.setItems(c.getItems() - 1);` as a behavior method. |
| BEG-021-EX04 | 4 | Make `Money` fully immutable and add `plus`. |
| BEG-021-EX05 | 4 | Fix a `Team` class that returns its internal `List<String> members` directly. |
| BEG-021-EX06 | 1, 2, 3, 4 | Code review: in a provided class, list every encapsulation violation and how to fix it. |

## Solutions
- **EX01** private; private; public; protected.
- **EX02** Private field; check in the constructor and the setter (if any) and throw `IllegalArgumentException` when out of range.
- **EX03** `public void removeItem() { if (items == 0) throw new IllegalStateException(); items--; }` then `c.removeItem();`.
- **EX04** `public final class Money { private final long cents; ... public Money plus(Money o) { return new Money(cents + o.cents); } }`.
- **EX05** Return `List.copyOf(members)` (or an unmodifiable view), and copy any incoming list in the constructor.
- **EX06** Typical findings: public fields, a setter that skips validation, reflex getters/setters, returned mutable collection, missing constructor validation. Graded against the review checklist.
