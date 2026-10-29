# BEG-049 · Relational modeling — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** a library card catalog: one card file per kind of thing, cards linked by ID numbers.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-049-L01 · Tables, rows, and columns (8 min)
**Goal:** turn a real-world thing into a table.

**Key points**
- An entity is a kind of thing: book, member, loan.
- Each entity becomes a table; each instance is a row.
- Each fact about it is a column with a type: text, integer, date, boolean.
- Name tables and columns clearly, in lowercase with underscores.
- One table, one kind of thing.

**Show**
```text
books(id, title, isbn, published_year)
```

**Check:** What is a row? *(One instance of the entity, such as one book.)*

---

## BEG-049-L02 · Primary keys (8 min)
**Goal:** identify each row uniquely.

**Key points**
- A primary key (PK) uniquely identifies a row; it cannot be empty or repeat.
- Prefer a simple ID number that never changes.
- Real data like names or emails can change or repeat, so they make poor keys.
- A generated numeric ID is common.

**Show**
```text
books: id (PK) | title | isbn
        1      | Dune  | 978...
```

**Check:** Can two rows share a primary key? *(No.)*

---

## BEG-049-L03 · Foreign keys and relationships (12 min)
**Goal:** link tables without copying data.

**Key points**
- A foreign key (FK) is a column holding another table's primary key.
- It lets one row point to another instead of repeating its data.
- One-to-many: one author has many books; the FK goes on the "many" side.
- The database can reject an FK value that points to nothing.

**Show**
```text
authors(id PK, name)
books(id PK, title, author_id FK -> authors.id)
```

**Check:** Which table holds the FK in "one author, many books"? *(`books`.)*

---

## BEG-049-L04 · Many-to-many (8 min)
**Goal:** model relationships where both sides have many.

**Key points**
- A book can have many authors; an author can write many books.
- One FK column cannot hold that, and comma-separated lists break the rules.
- Use a junction table with one row per pair.
- The junction table has two FKs; together they can be its primary key.

**Show**
```text
book_authors(book_id FK, author_id FK, PK(book_id, author_id))
```

**Check:** What do you add for many-to-many? *(A junction table.)*

---

## BEG-049-L05 · Normalization in practice (14 min)
**Goal:** clean a flat table into 3NF.

**Key points**
- Normalization removes duplication so each fact is stored once.
- 1NF: one value per cell; no lists in a column.
- 2NF: every column depends on the whole key (matters with composite keys).
- 3NF: columns depend on the key and nothing else; move other facts to their own table.
- Anomalies removed: update (change in many places), insert (cannot add without unrelated data), delete (losing facts by deleting a row).

**Show:** a flat loans sheet with member name and phone on every row, split into `members` and `loans`.

**Check:** Name one anomaly normalization removes. *(Update, insert, or delete anomaly.)*

---

## BEG-049-L06 · Demo: normalizing a library spreadsheet into tables (8 min)
**Goal:** do the full split step by step. Prepares BEG-049-LAB1.

**Steps**
1. Open the spreadsheet: loan, member, member phone, book, authors "A; B", due date.
2. Fix 1NF: split the authors list into separate rows.
3. **Planned mistake:** keep the member's phone on every loan row; show an update anomaly when one phone changes.
4. Fix: create `members`, `books`, `authors`, `book_authors`, `loans` with PKs and FKs.
5. Draw the ER diagram and check each column against 3NF.
