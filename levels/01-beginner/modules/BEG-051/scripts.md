# BEG-051 · PostgreSQL basics — Lecture scripts

**Video:** 53 min · **Analogy used throughout:** a library building with rooms (databases), shelves (schemas), staff keys (users), and rules on the door (constraints).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-051-L01 · Installing PostgreSQL (10 min)
**Goal:** get a local PostgreSQL running.

**Key points**
- PostgreSQL is an open-source relational DBMS and our main database.
- Install it natively or run it in a container; verify the current version and installer steps before recording.
- The installer asks for a password for the `postgres` superuser; remember it.
- The server listens on port 5432 by default.
- Check it works by connecting.

**Show:** the installer steps and a first `psql --version`.

**Check:** Which default port does PostgreSQL use? *(5432.)*

---

## BEG-051-L02 · `psql` and a GUI client (10 min)
**Goal:** connect with two tools.

**Key points**
- `psql` is the command-line client.
- pgAdmin or DBeaver are graphical clients that show tables and run queries.
- Useful `psql` commands: `\l` lists databases, `\dt` lists tables, `\q` quits.
- Use the GUI to browse; use `psql` and SQL scripts to repeat work.

**Show**
```bash
psql -h localhost -U postgres
```
```text
\l
\dt
```

**Check:** Which command lists tables in `psql`? *(`\dt`.)*

---

## BEG-051-L03 · Databases, schemas, and users (8 min)
**Goal:** organize and secure access.

**Key points**
- One server holds many databases; each database has schemas (default `public`).
- Create a separate user (role) per application with only the rights it needs.
- Do not work as the `postgres` superuser for daily work.
- Grant the app user rights on its own database only.

**Show**
```sql
CREATE USER library_app WITH PASSWORD 'change-me';
CREATE DATABASE library OWNER library_app;
```

**Check:** Why not use `postgres` for the app? *(Too much power; a mistake or a leak affects everything.)*

---

## BEG-051-L04 · Constraints that protect data (10 min)
**Goal:** let the database reject bad data.

**Key points**
- `NOT NULL`: a value is required.
- `UNIQUE`: no duplicates in the column.
- `CHECK`: a rule such as `copies >= 0`.
- `FOREIGN KEY ... REFERENCES`: the value must exist in the other table.
- Constraints in the database protect data even when application code has a bug.

**Show**
```sql
CREATE TABLE books (
  id     SERIAL PRIMARY KEY,
  isbn   TEXT NOT NULL UNIQUE,
  copies INTEGER NOT NULL CHECK (copies >= 0)
);
```

**Check:** Which constraint stops duplicate emails? *(`UNIQUE`.)*

---

## BEG-051-L05 · First look at transactions (7 min)
**Goal:** group statements so they succeed or fail together.

**Key points**
- A transaction is a group of statements treated as one unit.
- `BEGIN` starts, `COMMIT` saves, `ROLLBACK` undoes everything since `BEGIN`.
- Example: moving a book between members; both changes or neither.
- Details (isolation, locks) come in later levels.

**Show**
```sql
BEGIN;
UPDATE books SET copies = copies - 1 WHERE id = 1;
ROLLBACK;
```

**Check:** What does `ROLLBACK` do? *(Undoes all changes since `BEGIN`.)*

---

## BEG-051-L06 · Demo: creating the Library database with constraints (8 min)
**Goal:** build the schema as a re-runnable script. Prepares BEG-051-LAB1.

**Steps**
1. Create the `library` database and `library_app` user.
2. Write `schema.sql` with tables from BEG-049, adding `NOT NULL`, `UNIQUE`, `CHECK`, and FKs.
3. Add `DROP TABLE IF EXISTS ... ` at the top so the script can run again.
4. **Planned mistake:** insert a loan for a member that does not exist; the FK rejects it. Show the error message.
5. Demonstrate `BEGIN`, an `UPDATE`, then `ROLLBACK`.
