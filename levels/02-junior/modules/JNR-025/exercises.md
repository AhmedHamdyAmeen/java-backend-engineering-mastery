# JNR-025 · JDBC — Exercises and lab

## Lab
### JNR-025-LAB1 · Bulk import
**Outcomes:** 1–4 · **Time:** ~2 h
1. Create a `product` table (`id bigint generated always as identity`, `name text`, `price numeric(12,2)`).
2. Import 10,000 products from a provided CSV using a pooled `DataSource` and a batched `PreparedStatement`.
3. Import the same file row by row with auto-commit on; time both with the same data.
4. Print the generated keys of the first batch; map `price` to `BigDecimal`.
5. Add a `findAll(sortBy)` method whose sort column comes from an allow-list.

**Acceptance:** measured speed-up shown; no concatenated user input in any SQL.

## Exercises (assessment: fix an injectable dynamic query)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-025-EX01 | 1 | Explain in three sentences why a connection pool beats `DriverManager` per statement. |
| JNR-025-EX02 | 1 | Rewrite a method that opens `DriverManager` connections to use an injected `DataSource` with try-with-resources. |
| JNR-025-EX03 | 2 | Insert five rows with `addBatch` and print each generated id. |
| JNR-025-EX04 | 3 | Choose the Java type for: `numeric(10,2)`, `timestamptz`, `date`, and a nullable `bigint`. |
| JNR-025-EX05 | 4 | Fix `"select * from product where name = '" + name + "'"` using a placeholder. |
| JNR-025-EX06 | 4 | Fix `"... order by " + request.getParameter("sort")` with an allow-list and a default. |

## Solutions
- **EX01** Opening a connection costs network round trips, login, and setup; a pool keeps connections open and reuses them, so each statement pays almost nothing and the database is protected from too many connections.
- **EX02** `try (Connection c = dataSource.getConnection(); PreparedStatement ps = ...) { ... }`; the `DataSource` is a constructor parameter.
- **EX03** Prepare with `Statement.RETURN_GENERATED_KEYS`, `addBatch` five times, `executeBatch`, loop over `getGeneratedKeys()`.
- **EX04** `BigDecimal`; `Instant` or `OffsetDateTime`; `LocalDate`; `Long` (read with `getObject(col, Long.class)`).
- **EX05** `prepareStatement("select * from product where name = ?")` then `ps.setString(1, name)`.
- **EX06** `String col = SORTABLE.getOrDefault(sort, "name");` and concatenate only `col`.
- Outcomes 2 and 3 are also checked in the lab (batch timing, `BigDecimal` price).
