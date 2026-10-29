# JNR-026 · Spring JDBC — Exercises and lab

## Lab
### JNR-026-LAB1 · Products on PostgreSQL
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Add the JDBC starter and driver; configure the datasource in `application.yml` with credentials from environment variables.
2. Implement `ProductRepository` (find by id, list, save, update, delete) with `JdbcClient` and named parameters, behind the existing interface.
3. Use one `RowMapper` shared by all queries.
4. Translate a duplicate SKU to a domain exception in the repository.
5. Write an integration test against a real PostgreSQL database.

**Acceptance:** no controller or service changes needed; integration test passes against a real database.

## Exercises (assessment: implement a reporting query repository method)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-026-EX01 | 1 | Write the `application.yml` datasource block without a hard-coded password. |
| JNR-026-EX02 | 2 | Write `update` and `delete` methods with named parameters and return whether a row was affected. |
| JNR-026-EX03 | 3 | Map a `product` row to a record with a `RowMapper`, then do it again with `query(Product.class)`. |
| JNR-026-EX04 | 4 | Name the exception Spring throws for a unique violation and for `.single()` with no row. |
| JNR-026-EX05 | 2, 3 | Reporting method `salesByCategory()` returning `record CategoryTotal(String category, BigDecimal total)` from a `group by` query. |
| JNR-026-EX06 | 4 | Explain why catching `DataAccessException` in every repository method is a mistake. |

## Solutions
- **EX01** `url: jdbc:postgresql://localhost:5432/shop`, `username: ${DB_USER}`, `password: ${DB_PASSWORD}`.
- **EX02** `int n = jdbc.sql("update product set price = :p where id = :id").param("p", p).param("id", id).update(); return n == 1;`
- **EX03** `(rs, i) -> new Product(rs.getLong("id"), rs.getString("name"), rs.getBigDecimal("price"))` versus `jdbc.sql(sql).query(Product.class).list()`.
- **EX04** `DuplicateKeyException` (a `DataIntegrityViolationException`); `EmptyResultDataAccessException`.
- **EX05** `select c.name as category, sum(p.price) as total from product p join category c on c.id = p.category_id group by c.name` mapped with `.query(CategoryTotal.class).list()`.
- **EX06** It hides real failures, repeats code, and leaves nobody able to decide; catch a specific subclass where you can act and let the rest reach the global handler.
