# BEG-048 · Data fundamentals — Exercises and lab

## Lab
### BEG-048-LAB1 · Files vs database
**Outcomes:** 1–3 · **Time:** ~1 h
List the problems the Contacts CSV file would have with 1 million contacts and 100 simultaneous users.
**Acceptance:** at least five distinct problems.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-048-EX01 | 1 | Give three reasons a shop should use a database rather than one text file. |
| BEG-048-EX02 | 2 | Classify as structured, semi-structured, or unstructured: a spreadsheet, a JSON response, a voice recording. |
| BEG-048-EX03 | 2 | Write one sentence on when you might choose a nonrelational database and why "faster" alone is not a reason. |
| BEG-048-EX04 | 3 | Explain in your own words the difference between a DBMS, a database, and a schema. |
| BEG-048-EX05 | 3 | Sketch a schema (table name, columns, types) for contacts. |

## Solutions
- **EX01** Fast search, safe simultaneous use, rules (uniqueness, required fields), crash safety.
- **EX02** Structured; semi-structured; unstructured.
- **EX03** For example flexible document shapes or very large simple key lookups; speed depends on the workload, so measure.
- **EX04** DBMS is the software (PostgreSQL); the database is the stored data it manages; the schema is the structure and rules.
- **EX05** `contacts(id integer, name text, email text, phone text)`.
- Outcome coverage: all outcomes are also covered by the quiz and the lab.
