# BEG-055 · JDBC essentials — Exercises and lab

## Lab
### BEG-055-LAB1 · Library DAO
**Outcomes:** 1–5 · **Time:** ~3 h
Write a `BookRepository` interface with a JDBC implementation (`save`, `findById` returning `Optional`, `findByTitle`, `delete`) and integration tests against a local test database.
**Acceptance:** no string-concatenated SQL; resources closed; tests pass.

## Exercises (assessment: implement a new repository method with a test; explain why parameters prevent injection)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-055-EX01 | 1 | Add the PostgreSQL driver with Maven and connect using `DB_URL`, `DB_USER`, `DB_PASSWORD` environment variables. |
| BEG-055-EX02 | 2 | Write `findAll()` returning a `List<Book>` mapped from a `ResultSet`. |
| BEG-055-EX03 | 2 | Write `findById(int)` returning `Optional<Book>`. |
| BEG-055-EX04 | 3 | Rewrite a method that closes resources manually using try-with-resources. |
| BEG-055-EX05 | 4 | Demonstrate injection against a concatenated query, then fix it with parameters. |
| BEG-055-EX06 | 5 | Write a method that inserts a loan and reduces `copies` in one transaction with rollback on error. |
| BEG-055-EX07 | 1 | Check that no password appears in the code or the Git history of your project. |
| BEG-055-EX08 | 2 | Implement a new method `findByTitleContaining(String)` using `LIKE ?` and write an integration test for it. (A lookup by author needs a join through `book_authors`; try it only as a stretch task.) |

## Solutions
- **EX01** Dependency `org.postgresql:postgresql` (verify version); `DriverManager.getConnection(System.getenv("DB_URL"), ...)`.
- **EX02** Loop `while (rs.next())`, add `new Book(rs.getInt("id"), rs.getString("title"))` to a list.
- **EX03** `if (rs.next()) return Optional.of(map(rs)); return Optional.empty();`
- **EX04** `try (Connection c = ...; PreparedStatement ps = c.prepareStatement(sql); ResultSet rs = ps.executeQuery()) { ... }`
- **EX05** Input `x' OR '1'='1` returns all rows with concatenation; with `?` it returns none because the value is data.
- **EX06** `setAutoCommit(false)`; two `executeUpdate` calls; `commit()`; `catch` calls `rollback()` and rethrows.
- **EX07** Credentials come from environment variables; `git log -p` and a search for the password show no match.
- **EX08** `SELECT ... WHERE title LIKE ?` with the parameter `"%" + text + "%"` (bound through `setString`, never concatenated); the test inserts two books, queries, and asserts the result. Stretch: join `books`, `book_authors`, and `authors` to filter by author name.
