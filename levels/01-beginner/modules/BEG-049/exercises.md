# BEG-049 · Relational modeling — Exercises and lab

## Lab
### BEG-049-LAB1 · Library schema
**Outcomes:** 1–4 · **Time:** ~3 h
Design the ER diagram for books, authors, members, and loans, with columns, types, PKs, and FKs. Have a peer review it.
**Acceptance:** 3NF; relationships correct; peer-reviewed.

## Exercises (assessment: normalize a provided spreadsheet)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-049-EX01 | 1 | Model a `members` table: choose columns and a type for each. |
| BEG-049-EX02 | 2 | Choose a primary key for `members` and say why email is a poor choice. |
| BEG-049-EX03 | 2 | Add the foreign key that links `loans` to `members` and `books`. |
| BEG-049-EX04 | 3 | Model "a book can have many authors" with a junction table. |
| BEG-049-EX05 | 3 | Fix a `books` table that has a column `tags` containing "java,sql,web". |
| BEG-049-EX06 | 4 | Normalize the provided flat spreadsheet to 3NF (list resulting tables). |
| BEG-049-EX07 | 4 | Name the update, insert, and delete anomalies in the flat sheet. |

## Solutions
- **EX01** `members(id integer, name text, email text, joined_on date)`.
- **EX02** `id`, a generated number; emails can change and may be reused.
- **EX03** `loans(id, member_id FK -> members.id, book_id FK -> books.id, loaned_on, due_on, returned_on)`.
- **EX04** `book_authors(book_id, author_id)` with a composite PK and two FKs.
- **EX05** Create `tags(id, name)` and `book_tags(book_id, tag_id)`; one tag per row.
- **EX06** Typically `members`, `books`, `authors`, `book_authors`, `loans`, each with a PK; no repeated member or book facts.
- **EX07** Update: a changed phone must be edited on every loan row. Insert: a new member cannot exist before a loan. Delete: deleting a member's only loan loses the member.
