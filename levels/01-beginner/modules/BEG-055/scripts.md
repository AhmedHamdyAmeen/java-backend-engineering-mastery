# BEG-055 · JDBC essentials — Lecture scripts

**Video:** 66 min · **Analogy used throughout:** a phone call to the librarian: dial (connect), ask a question (statement), hear the answer (result), hang up (close).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-055-L01 · How Java talks to a database (8 min)
**Goal:** see the pieces between Java and PostgreSQL.

**Key points**
- JDBC (Java Database Connectivity) is the standard Java API for databases.
- A driver translates JDBC calls to a specific database's protocol.
- Main types: `Connection`, `PreparedStatement`, `ResultSet`.
- Flow: connect, prepare, execute, read results, close.
- JNR-025 later builds on this with pooling and Spring.

**Show:** boxes: Java code, JDBC API, PostgreSQL driver, PostgreSQL.

**Check:** What does the driver do? *(Translates JDBC calls for one database.)*

---

## BEG-055-L02 · Connecting: driver, URL, credentials from environment variables (10 min)
**Goal:** open a connection without hard-coded secrets.

**Key points**
- Add the PostgreSQL driver as a Maven dependency (verify the current version).
- The URL looks like `jdbc:postgresql://localhost:5432/library`.
- Read user and password from environment variables with `System.getenv`.
- Never commit credentials to Git.
- `DriverManager.getConnection(url, user, password)` returns a `Connection`.

**Show**
```java
String url = System.getenv("DB_URL");
String user = System.getenv("DB_USER");
String pass = System.getenv("DB_PASSWORD");
try (Connection c = DriverManager.getConnection(url, user, pass)) {
    System.out.println("Connected: " + !c.isClosed());
}
```

**Check:** Where do credentials come from? *(Environment variables, not the source code.)*

---

## BEG-055-L03 · Querying and mapping rows to objects (12 min)
**Goal:** read rows and turn them into Java objects.

**Key points**
- Use `PreparedStatement` with `?` placeholders.
- Set values with `setString`, `setInt`, and so on; positions start at 1.
- `executeQuery()` returns a `ResultSet`; `executeUpdate()` is for insert, update, delete.
- Loop `while (rs.next())` and read columns by name.
- Close everything with try-with-resources.

**Show**
```java
String sql = "SELECT id, title FROM books WHERE title = ?";
try (PreparedStatement ps = conn.prepareStatement(sql)) {
    ps.setString(1, title);
    try (ResultSet rs = ps.executeQuery()) {
        while (rs.next()) {
            books.add(new Book(rs.getInt("id"), rs.getString("title")));
        }
    }
}
```

**Check:** What index does the first `?` have? *(1.)*

---

## BEG-055-L04 · SQL injection, live (10 min)
**Goal:** see how string concatenation lets an attacker change the query.

**Key points**
- Injection: user input is treated as SQL code.
- With concatenation, input `' OR '1'='1` makes the condition always true.
- With parameters, the input is only data, never code.
- Injection can leak or destroy data; it is a top web risk.
- Rule: never concatenate input into SQL.

**Show**
```java
// BAD
String sql = "SELECT * FROM members WHERE name = '" + name + "'";
// GOOD
String sql = "SELECT * FROM members WHERE name = ?";
```

**Check:** Why do parameters prevent injection? *(The value is sent as data, not parsed as SQL.)*

---

## BEG-055-L05 · Transactions from Java (10 min)
**Goal:** make several statements succeed or fail together.

**Key points**
- By default each statement commits on its own (auto-commit).
- `setAutoCommit(false)` starts a manual transaction.
- `commit()` saves; `rollback()` undoes.
- Roll back in a `catch` when something fails.
- Example: record a loan and reduce copies, both or neither.

**Show**
```java
conn.setAutoCommit(false);
try {
    // statement 1: insert loan
    // statement 2: update copies
    conn.commit();
} catch (SQLException e) {
    conn.rollback();
    throw e;
}
```

**Check:** What does `rollback()` do? *(Undoes the changes since the last commit.)*

---

## BEG-055-L06 · Demo: building the BookRepository with JDBC (8 min)
**Goal:** write the DAO for the lab. Prepares BEG-055-LAB1.

**Steps**
1. Define the `BookRepository` interface: `save`, `findById` (returns `Optional<Book>`), `findByTitle`, `delete`.
2. Create `JdbcBookRepository` taking a `DataSource` or connection settings.
3. Implement `save` with an `INSERT` and `PreparedStatement`.
4. **Planned mistake:** forget try-with-resources on the `ResultSet` and leak resources. Fix: wrap statement and result set.
5. Run a test against the local test database.

---

## BEG-055-L07 · Demo: SQL injection, then the PreparedStatement fix (8 min)
**Goal:** attack, then defend. Prepares BEG-055-LAB1.

**Steps**
1. Write `findByTitleUnsafe` using string concatenation.
2. Call it with `x' OR '1'='1`; every row is returned.
3. **Planned mistake:** try to "fix" it by removing quotes only; show it is still bypassable in other ways.
4. Rewrite with `PreparedStatement`; repeat the attack; it returns nothing.
5. State the rule: parameters for every value, always.
