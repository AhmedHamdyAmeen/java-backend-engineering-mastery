# JNR-025 · JDBC — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** phone calls to the database (dialing is slow; a switchboard keeps lines open).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-025-L01 · From `DriverManager` to `DataSource` (8 min)
**Goal:** get database connections from a pool instead of opening one per statement.

**Key points**
- JDBC is Java's standard API to talk to SQL databases; a driver (JAR) speaks the database's protocol.
- `DriverManager.getConnection(...)` opens a brand-new connection each time: slow (network, login, setup).
- A `DataSource` hands out connections; a pool (for example HikariCP) keeps them open and reuses them.
- "Closing" a pooled connection returns it to the pool; always use try-with-resources.
- Never open one connection per statement.

**Show**
```java
try (Connection c = dataSource.getConnection();
     PreparedStatement ps = c.prepareStatement("select id, name from product where id = ?")) {
    ps.setLong(1, 42L);
    try (ResultSet rs = ps.executeQuery()) {
        if (rs.next()) System.out.println(rs.getString("name"));
    }
}
```

**Check:** What does `close()` do on a pooled connection? *(Returns it to the pool; the real connection stays open.)*

---

## JNR-025-L02 · Generated keys and batching (10 min)
**Goal:** insert many rows quickly and read the ids the database created.

**Key points**
- The database often generates the id (identity column). Ask for it with `RETURN_GENERATED_KEYS`.
- Each `executeUpdate` is one network round trip.
- A batch collects many statements (`addBatch`) and sends them together (`executeBatch`).
- Group batches (for example every 500 rows) so memory stays small.
- Turn off auto-commit and commit once per chunk for more speed.

**Show**
```java
c.setAutoCommit(false);
try (PreparedStatement ps = c.prepareStatement(
        "insert into product(name, price) values (?, ?)", Statement.RETURN_GENERATED_KEYS)) {
    for (Product p : products) {
        ps.setString(1, p.name());
        ps.setBigDecimal(2, p.price());
        ps.addBatch();
    }
    ps.executeBatch();
    try (ResultSet keys = ps.getGeneratedKeys()) { while (keys.next()) { /* keys.getLong(1) */ } }
}
c.commit();
```

**Check:** Why is a batch faster than a loop of single inserts? *(Fewer network round trips.)*

---

## JNR-025-L03 · Type mapping pitfalls (10 min)
**Goal:** map SQL column types to the right Java types.

**Key points**
- Money: `numeric(12,2)` maps to `BigDecimal`, never `double` (binary floats cannot store 0.1 exactly).
- Time: `timestamptz` maps to `Instant` or `OffsetDateTime`; `date` to `LocalDate`.
- `bigint` maps to `long`; for nullable columns use `getObject(col, Long.class)` or check `wasNull()`.
- `rs.getInt` on a NULL silently returns 0.
- Text columns map to `String`; PostgreSQL `uuid` maps to `UUID`.

**Show**
```java
BigDecimal price = rs.getBigDecimal("price");
Instant created = rs.getObject("created_at", OffsetDateTime.class).toInstant();
Long categoryId = rs.getObject("category_id", Long.class); // null stays null
```

**Check:** Which Java type for a `numeric(12,2)` price? *(`BigDecimal`.)*

---

## JNR-025-L04 · Dynamic SQL without injection (12 min)
**Goal:** build queries from user input safely.

**Key points**
- SQL injection: user text becomes part of the SQL command and changes its meaning.
- Values always go through `?` placeholders (`PreparedStatement`); the database never treats them as SQL.
- Placeholders cannot be used for column names or `ASC`/`DESC`.
- For a user-chosen sort column, use an allow-list (a fixed map from public names to real column names).
- Unknown value: reject it or fall back to a default; never paste it in.

**Show**
```java
private static final Map<String, String> SORTABLE = Map.of("name", "name", "price", "price");

String col = SORTABLE.getOrDefault(sortParam, "name");
String dir = "desc".equalsIgnoreCase(dirParam) ? "desc" : "asc";
String sql = "select id, name, price from product order by " + col + " " + dir;
```

**Check:** Can you pass a column name as a `?` parameter? *(No; use an allow-list.)*

---

## JNR-025-L05 · Demo: batch import and timing comparison (10 min)
**Goal:** measure row-by-row against batched inserts; prepares JNR-025-LAB1.

**Steps**
1. Create the `product` table with `schema.sql` in local PostgreSQL.
2. Read a 10,000-line CSV into a list of records.
3. Insert row by row with auto-commit on; time it with `System.nanoTime()`.
4. **Planned mistake:** open a new `DriverManager` connection inside the loop; show how slow it gets, then switch to a pooled `DataSource`.
5. Rewrite with `addBatch`/`executeBatch` in chunks of 500 and one commit per chunk; time again.
6. Compare the two numbers and confirm all rows arrived with `select count(*)`.
