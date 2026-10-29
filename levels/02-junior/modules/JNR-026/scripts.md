# JNR-026 · Spring JDBC — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a paperwork assistant who fills in the forms (open, run, close, translate errors) while you only say what you want.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-026-L01 · DataSource configuration in Boot (8 min)
**Goal:** connect Shop to PostgreSQL with properties only.

**Key points**
- Add the `spring-boot-starter-jdbc` dependency and the PostgreSQL driver.
- Set `spring.datasource.url`, `username`, and `password` in `application.yml`; Boot builds a HikariCP pool.
- Secrets come from environment variables, not from the file in Git.
- Pool size is configurable (`spring.datasource.hikari.maximum-pool-size`); defaults are fine to start.
- Boot creates `JdbcTemplate` and `JdbcClient` beans for you.

**Show**
```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/shop
    username: ${DB_USER}
    password: ${DB_PASSWORD}
```

**Check:** Which pool does Boot use by default? *(HikariCP.)*

---

## JNR-026-L02 · `JdbcClient` and `JdbcTemplate` (12 min)
**Goal:** run queries and updates without writing connection code.

**Key points**
- `JdbcClient` is the modern fluent API (Spring 6.1 and later); `JdbcTemplate` is the older, still common one.
- Both open, close, and return connections for you.
- Use named parameters (`:name`) instead of positional `?` so queries stay readable.
- `.query(...)` reads rows; `.update(...)` runs insert, update, delete and returns the affected row count.
- A `KeyHolder` returns generated ids.

**Show**
```java
int rows = jdbc.sql("update product set price = :price where id = :id")
        .param("price", newPrice)
        .param("id", id)
        .update();

Optional<Product> p = jdbc.sql("select id, name, price from product where id = :id")
        .param("id", id)
        .query(Product.class)
        .optional();
```

**Check:** What does `update()` return? *(The number of affected rows.)*

---

## JNR-026-L03 · Mapping rows (10 min)
**Goal:** turn result rows into records.

**Key points**
- A `RowMapper<T>` converts one row to one object; Spring loops over the rows.
- You never call `rs.next()` yourself.
- `query(Product.class)` maps columns to record components or properties automatically (names must match; `created_at` matches `createdAt`).
- Write a mapper when types need conversion, for example `timestamptz` to `Instant`.
- Keep mapping inside the repository; services never see `ResultSet`.

**Show**
```java
private static final RowMapper<Product> MAPPER = (rs, i) -> new Product(
        rs.getLong("id"),
        rs.getString("name"),
        rs.getBigDecimal("price"));
```

**Check:** Who calls `rs.next()` when you use a `RowMapper`? *(Spring.)*

---

## JNR-026-L04 · Exception translation (10 min)
**Goal:** understand why you get `DataAccessException` instead of `SQLException`.

**Key points**
- `SQLException` is checked and database-specific (error codes, SQL states).
- Spring catches it and rethrows an unchecked `DataAccessException` subclass, for example `DuplicateKeyException`, `DataIntegrityViolationException`, `EmptyResultDataAccessException`.
- This keeps services independent of the database and of JDBC.
- Catch a specific subclass at one place that can act (for example turn a duplicate into 409); do not catch `DataAccessException` everywhere.
- Unhandled ones go to the global exception handler.

**Show**
```java
try {
    jdbc.sql("insert into product(sku, name) values (:sku, :name)")
        .param("sku", sku).param("name", name).update();
} catch (DuplicateKeyException e) {
    throw new SkuAlreadyExistsException(sku);
}
```

**Check:** Is `DataAccessException` checked or unchecked? *(Unchecked.)*

---

## JNR-026-L05 · Demo: replacing the in-memory repository with Spring JDBC (10 min)
**Goal:** swap the Shop repository implementation without touching controllers or services; prepares JNR-026-LAB1.

**Steps**
1. Show the existing `ProductRepository` interface and the in-memory implementation.
2. Apply `schema.sql` manually in local PostgreSQL and add the datasource properties.
3. Create `JdbcProductRepository implements ProductRepository` using `JdbcClient` and a shared mapper.
4. **Planned mistake:** forget the `@Repository`/bean switch so two implementations exist; show the startup error and remove the in-memory bean.
5. Run the existing API tests; they pass unchanged.
6. Add one integration test against a real PostgreSQL database.
