# JNR-027 · ORM fundamentals — Exercises and lab

## Lab
### JNR-027-LAB1 · Mismatch exercise
**Outcomes:** 1–3 · **Time:** ~1 h
1. Open the Spring JDBC `ProductRepository` from JNR-026.
2. List every piece of mapping code: SQL strings, row mappers, key handling, null handling, type conversions, joins assembled by hand.
3. For each item, predict whether an ORM would remove it, change it, or leave it.
4. For each, name one risk the ORM would add (hidden query, lazy loading, dirty checking surprise).
5. Tag each item with the mismatch it belongs to (identity, inheritance, associations, granularity).

**Acceptance:** a reasoned list with a prediction and a risk for every mapping item.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-027-EX01 | 1 | Name the four mismatches and give a one-line Shop example of each. |
| JNR-027-EX02 | 1 | Explain why `Order` with `List<OrderLine>` has no direct table equivalent. |
| JNR-027-EX03 | 2 | List three things an ORM automates and three costs it introduces. |
| JNR-027-EX04 | 2 | Explain why "we use an ORM so we do not need SQL" is wrong. |
| JNR-027-EX05 | 3 | Predict the number of selects for: `find(1)`, `find(1)`, `find(2)` in one transaction. |
| JNR-027-EX06 | 3 | Explain why changing a loaded entity without calling `save` can still update the row. |

## Solutions
- **EX01** Identity: two `Product` objects with the same id; inheritance: `DigitalProduct extends Product`; associations: `Order`-`OrderLine`; granularity: `Money` as amount and currency columns.
- **EX02** A list lives inside the object; in the database each line is a row in another table pointing back with a foreign key.
- **EX03** Automates: generated SQL, row mapping, change tracking. Costs: hidden queries, N+1 risk, learning curve and debugging effort.
- **EX04** You must design the schema, read generated SQL, write queries for reports, and diagnose slow statements.
- **EX05** Two selects; the second `find(1)` comes from the identity map.
- **EX06** The persistence context tracks managed entities and writes changes at flush (dirty checking: unit of work).
- Outcome coverage: the quiz also tests all three outcomes.
