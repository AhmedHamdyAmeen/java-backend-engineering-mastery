# BEG-026 · Java object model — Exercises and lab

## Lab
### BEG-026-LAB1 · Broken set
**Outcomes:** 2, 3, 4 · **Time:** ~1.5 h
Put `Money` objects into a `HashSet` (treat it as a black box) with no overrides, with only `equals`, and with both `equals` and `hashCode`. Record the set size each time and explain the duplicates.
**Acceptance:** correct implementation and explanation.

## Exercises (assessment: contract quiz plus implementation exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-026-EX01 | 1 | List five methods every object inherits from `Object`, and say which three are most often overridden. |
| BEG-026-EX02 | 2 | Predict `==` and `equals` for: two literals `"a"`, `new String("a")` vs a literal, two `new Account(...)` with the same data and no overrides. |
| BEG-026-EX03 | 2 | Fix: `if (command == "quit")`. |
| BEG-026-EX04 | 3 | Implement `equals` and `hashCode` for `Customer(id, name)` where `id` identifies the customer. |
| BEG-026-EX05 | 3 | Explain why a mutable field in `hashCode` can make an object "disappear" from a `HashSet`. |
| BEG-026-EX06 | 4 | Write a `toString` for `Account` that shows number and balance but not secrets. |

## Solutions
- **EX01** `toString`, `equals`, `hashCode`, `getClass`, `wait`/`notify` (or `clone`). Most overridden: `toString`, `equals`, `hashCode`.
- **EX02** `"a" == "a"` true (shared literal), `equals` true; `new String("a") == "a"` false, `equals` true; two accounts: `==` false, `equals` false.
- **EX03** `"quit".equals(command)` (also safe against `null`).
- **EX04** Compare `id` only: `equals` checks `o instanceof Customer c && id == c.id`; `hashCode` returns `Long.hashCode(id)` or `Objects.hash(id)`.
- **EX05** The object was stored under a bucket from its old hash; after the field changes, lookups use the new hash and look in another bucket.
- **EX06** `return "Account[" + number + ", balance=" + balance + "]";`
- Outcome 3 is also covered by the lab and the quiz.
