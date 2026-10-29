# BEG-051 · PostgreSQL basics — Exercises and lab

## Lab
### BEG-051-LAB1 · Library database live
**Outcomes:** 1–4 · **Time:** ~3 h
Create the Library schema from BEG-049 as a SQL script with constraints and seed data. Try to insert invalid rows and record the errors. Demonstrate a rollback.
**Acceptance:** script re-runnable from scratch.

## Exercises (assessment: practical check of the script)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-051-EX01 | 1 | Install PostgreSQL, connect with `psql`, and run `SELECT version();`. |
| BEG-051-EX02 | 1 | Connect with pgAdmin or DBeaver and browse the tables of a database. |
| BEG-051-EX03 | 2 | Create a user `library_app`, a database `library` owned by it, and connect as that user. |
| BEG-051-EX04 | 3 | Add `NOT NULL`, `UNIQUE`, and `CHECK` constraints to `books`; write one failing insert for each. |
| BEG-051-EX05 | 3 | Add a foreign key from `loans` to `members` and show the error for a missing member. |
| BEG-051-EX06 | 4 | Run an `UPDATE` inside `BEGIN`, check the result, then `ROLLBACK` and check again. |
| BEG-051-EX07 | 2 | Explain why an application should not connect as `postgres`. |

## Solutions
- **EX01** `psql -U postgres`, then `SELECT version();`.
- **EX02** Register a server on `localhost:5432`, open Schemas > public > Tables.
- **EX03** `CREATE USER library_app WITH PASSWORD '...'; CREATE DATABASE library OWNER library_app;` then `psql -U library_app -d library`.
- **EX04** Null title -> `NOT NULL` error; repeated ISBN -> unique violation; `copies = -1` -> check violation.
- **EX05** `member_id INTEGER NOT NULL REFERENCES members(id)`; inserting `member_id = 999` fails with a foreign key violation.
- **EX06** Before rollback the changed value shows; after rollback it is back to the original.
- **EX07** The superuser can change or drop everything; least privilege limits damage from bugs or leaks.
