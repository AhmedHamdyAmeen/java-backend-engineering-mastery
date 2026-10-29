# BEG-050 · SQL foundations — Exercises and lab

## Lab
### BEG-050-LAB1 · Library queries
**Outcomes:** 1–5 · **Time:** ~6 h
Answer 25 graded queries against a seeded library database: overdue loans, most-borrowed authors, members with no loans, and more.
**Acceptance:** 20 of 25 correct.

## Exercises (assessment: timed SQL test, also part of the BEG graduation gate)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-050-EX01 | 1 | Create a `publishers` table (id, name, city) and add a `website` column afterwards. |
| BEG-050-EX02 | 2 | Insert two publishers, update one city, delete the other, each with a correct `WHERE`. |
| BEG-050-EX03 | 3 | List books from after 1990, newest first, top five. |
| BEG-050-EX04 | 3 | Count books per author and keep only authors with at least two. |
| BEG-050-EX05 | 4 | List every member and their loans, including members with no loans. |
| BEG-050-EX06 | 4 | Explain in two sentences the difference between inner and left join. |
| BEG-050-EX07 | 5 | List titles of books never loaned, using a subquery. |
| BEG-050-EX08 | 2 | Explain why you run a `SELECT` before an `UPDATE` and what a missing `WHERE` does. |

## Solutions
- **EX01** `CREATE TABLE publishers (id INTEGER PRIMARY KEY, name TEXT NOT NULL, city TEXT); ALTER TABLE publishers ADD COLUMN website TEXT;`
- **EX02** `INSERT ... VALUES (...)`; `UPDATE publishers SET city = 'Oslo' WHERE id = 1;` `DELETE FROM publishers WHERE id = 2;`
- **EX03** `SELECT title FROM books WHERE published_year > 1990 ORDER BY published_year DESC LIMIT 5;`
- **EX04** `SELECT author_id, COUNT(*) FROM books GROUP BY author_id HAVING COUNT(*) >= 2;`
- **EX05** `SELECT m.name, l.id FROM members m LEFT JOIN loans l ON l.member_id = m.id;`
- **EX06** Inner join keeps only matched rows; left join keeps all left rows and fills missing right columns with `NULL`.
- **EX07** `SELECT title FROM books WHERE id NOT IN (SELECT book_id FROM loans);` (this works if `loans.book_id` has no `NULL`s).
- **EX08** The `SELECT` shows which rows will change; without `WHERE` every row is changed.
