# BEG-050 · SQL foundations — Lecture scripts

**Video:** 91 min · **Analogy used throughout:** asking the librarian precise questions about the card catalog.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-050-L01 · SQL overview: DDL vs DML (7 min)
**Goal:** know the two families of SQL statements.

**Key points**
- SQL is the language for talking to relational databases.
- DDL (Data Definition Language) changes structure: `CREATE`, `ALTER`, `DROP`.
- DML (Data Manipulation Language) changes or reads rows: `INSERT`, `UPDATE`, `DELETE`, `SELECT`.
- Statements end with a semicolon; keywords are usually written in capitals.

**Show:** two columns: DDL builds the shelves, DML moves the books.

**Check:** Is `INSERT` DDL or DML? *(DML.)*

---

## BEG-050-L02 · `CREATE` and `ALTER` (10 min)
**Goal:** create and change tables.

**Key points**
- `CREATE TABLE` names the table, its columns, and their types.
- Mark the primary key in the definition.
- `ALTER TABLE ... ADD COLUMN` adds a column later.
- `DROP TABLE` deletes the table and its data; be careful.

**Show**
```sql
CREATE TABLE authors (
  id   INTEGER PRIMARY KEY,
  name TEXT NOT NULL
);
ALTER TABLE authors ADD COLUMN country TEXT;
```

**Check:** Which statement adds a column? *(`ALTER TABLE ... ADD COLUMN`.)*

---

## BEG-050-L03 · `INSERT`, `UPDATE`, `DELETE` (10 min)
**Goal:** change rows safely.

**Key points**
- `INSERT INTO table (cols) VALUES (...)` adds a row.
- `UPDATE table SET col = value WHERE ...` changes rows.
- `DELETE FROM table WHERE ...` removes rows.
- Without `WHERE`, `UPDATE` and `DELETE` hit every row.
- Habit: run a `SELECT` with the same `WHERE` first.

**Show**
```sql
INSERT INTO authors (id, name) VALUES (1, 'Ursula Le Guin');
UPDATE authors SET country = 'USA' WHERE id = 1;
DELETE FROM authors WHERE id = 1;
```

**Check:** What happens to `DELETE FROM authors;`? *(All rows are deleted.)*

---

## BEG-050-L04 · `SELECT`, `WHERE`, `ORDER BY` (10 min)
**Goal:** read and filter rows.

**Key points**
- `SELECT cols FROM table` reads data; `*` means all columns.
- `WHERE` keeps only rows matching a condition (`=`, `<>`, `<`, `>`, `AND`, `OR`, `LIKE`, `IN`).
- `ORDER BY col [DESC]` sorts the result.
- `LIMIT n` keeps the first n rows (PostgreSQL syntax).
- `NULL` means unknown; test it with `IS NULL`, not `= NULL`.

**Show**
```sql
SELECT title, published_year
FROM books
WHERE published_year > 2000
ORDER BY title
LIMIT 10;
```

**Check:** How do you find rows with no return date? *(`WHERE returned_on IS NULL`.)*

---

## BEG-050-L05 · Aggregates, `GROUP BY`, `HAVING` (12 min)
**Goal:** summarize data.

**Key points**
- Aggregates: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.
- `GROUP BY` makes one result row per group.
- `WHERE` filters rows before grouping; `HAVING` filters groups after.
- Every selected column must be grouped or aggregated.

**Show**
```sql
SELECT author_id, COUNT(*) AS books
FROM books
GROUP BY author_id
HAVING COUNT(*) >= 3;
```

**Check:** Which clause filters on `COUNT(*)`? *(`HAVING`.)*

---

## BEG-050-L06 · Joins (15 min)
**Goal:** combine rows from related tables.

**Key points**
- A join matches rows by a condition, usually FK = PK.
- `INNER JOIN` keeps only rows with a match on both sides.
- `LEFT JOIN` keeps every left row; missing right values are `NULL`.
- Use a left join plus `WHERE right.id IS NULL` to find rows with no match.
- Give tables short aliases.

**Show**
```sql
SELECT m.name, l.loaned_on
FROM members m
LEFT JOIN loans l ON l.member_id = m.id;
```

**Check:** Which join keeps members who never borrowed? *(`LEFT JOIN` from members.)*

---

## BEG-050-L07 · Subqueries (11 min)
**Goal:** use a query inside a query when it reads better.

**Key points**
- A subquery is a `SELECT` in parentheses.
- Scalar subquery returns one value, e.g. the average.
- `IN (subquery)` tests against a list.
- Use a join if you need columns from both tables; use a subquery when you only filter.

**Show**
```sql
SELECT title FROM books
WHERE id IN (SELECT book_id FROM loans WHERE returned_on IS NULL);
```

**Check:** What does the subquery above return? *(Ids of books currently on loan.)*

---

## BEG-050-L08 · Demo: answering library questions with SQL (8 min)
**Goal:** turn questions into queries. Prepares BEG-050-LAB1.

**Steps**
1. Load the seeded library data.
2. Question: books published after 2000, sorted by title (`WHERE`, `ORDER BY`).
3. Question: loans per member (`GROUP BY`).
4. **Planned mistake:** put `COUNT(*) > 3` in `WHERE`; the error appears. Fix: move it to `HAVING`.
5. Question: overdue loans (join `loans` with `members` and filter on `due_on`).

---

## BEG-050-L09 · Demo: joins that silently drop rows (8 min)
**Goal:** see why inner join can hide data. Prepares BEG-050-LAB1.

**Steps**
1. Query members with an inner join to loans; count the result.
2. Count members alone; the numbers differ.
3. **Planned mistake:** report "all members and their loans" with an inner join; members with no loans vanish.
4. Fix: switch to `LEFT JOIN`; the missing members appear with `NULL` loan data.
5. Rule of thumb: ask "may a row have no match?" before choosing the join.
