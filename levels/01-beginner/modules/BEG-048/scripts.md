# BEG-048 · Data fundamentals — Lecture scripts

**Video:** 38 min · **Analogy used throughout:** a paper notebook versus a well-run library with a librarian.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-048-L01 · Why databases (8 min)
**Goal:** explain why apps do not just store data in files.

**Key points**
- Programs forget everything when they stop; data must be saved.
- Files work for small, single-user data.
- A database adds searching, safety, and rules for many users at once.
- It protects data when the computer crashes mid-write.
- Many users can read and write at the same time without breaking each other's work.

**Show:** a notebook that two people write in at once, next to a librarian handling requests one by one.

**Check:** Name one thing a database adds over a plain file. *(Fast search, safe concurrent access, rules, crash safety.)*

---

## BEG-048-L02 · Structured vs unstructured data (7 min)
**Goal:** tell data shapes apart.

**Key points**
- Structured data has fixed fields: name, email, age.
- Semi-structured data has fields but they can vary, like JSON.
- Unstructured data has no fixed shape: photos, videos, free text.
- Databases are best at structured data; big files usually go to file storage.

**Show:** a contact as a table row, as JSON, and a photo.

**Check:** Is a photo structured? *(No, unstructured.)*

---

## BEG-048-L03 · Relational vs nonrelational (8 min)
**Goal:** compare the two big families at a high level.

**Key points**
- Relational: tables with rows and columns, linked by keys, queried with SQL.
- Nonrelational (NoSQL): other shapes such as documents, key-value pairs, or graphs.
- Relational databases enforce a strict structure and strong consistency.
- Nonrelational ones can be more flexible or scale differently.
- "NoSQL is faster" is not true in general; it depends on the job.

**Show:** the same contact as a row in a table and as a JSON document.

**Check:** Is NoSQL always faster? *(No; it depends on the workload.)*

---

## BEG-048-L04 · DBMS and schemas (7 min)
**Goal:** name the parts of a database system.

**Key points**
- A DBMS (database management system) is the software that stores and serves data. PostgreSQL is one.
- A database is the data it manages.
- A schema describes the structure: tables, columns, types, rules.
- A schema is the blueprint; the rows are the contents.

**Show:** a table definition as the blueprint, and three rows as data.

**Check:** What is a schema? *(The structure and rules of the data: tables, columns, types.)*

---

## BEG-048-L05 · Demo: why the contacts CSV breaks at scale (8 min)
**Goal:** see file problems first-hand. Prepares BEG-048-LAB1.

**Steps**
1. Open the Contacts CSV from the earlier project; search for one email by reading the whole file.
2. Generate 1 million rows and time the search again.
3. Edit the same file from two programs at once; the last save wins.
4. **Planned mistake:** a name containing a comma shifts all columns. Fix: quote the field, then note that a database column type would avoid this.
5. List the problems found: slow search, lost updates, no uniqueness check, no crash safety, no access control.
