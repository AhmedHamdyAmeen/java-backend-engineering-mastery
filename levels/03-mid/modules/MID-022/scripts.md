# MID-022 · Alternative persistence — Lecture scripts

**Video:** 52 min · **Running project:** Shop Platform (sales report and admin dashboard)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-022-L01 · When JPA is the wrong tool (8 min)
**Goal:** recognize workloads that fit JPA poorly.

**Key points**
- JPA shines for object graphs with transactional writes (aggregates with identity and state changes).
- It struggles with reporting (joins, aggregates, window functions), bulk set operations, and complex hand-tuned SQL.
- Symptoms: native queries everywhere, DTO mapping hacks, awkward entity graphs for read screens.
- You can use more than one tool in the same service, with clear boundaries.

**Show:** a table of Shop use cases: place order (JPA), monthly report (SQL), nightly price update (set-based SQL), admin search (SQL).

**Check:** Which Shop use case fits JPA best? *(Placing an order: transactional writes on an aggregate.)*

---

## MID-022-L02 · jOOQ in practice (14 min)
**Goal:** write type-safe SQL with generated classes.

**Key points**
- jOOQ generates Java classes from the database schema (tables, columns, types) through a code generator in the build.
- You write SQL as Java methods; the compiler catches renamed columns and wrong types.
- It supports modern SQL (CTEs, window functions, `ON CONFLICT`) and maps results to records or DTOs.
- Integrates with Spring transactions through `DSLContext` using the same `DataSource`.
- Generate from a migrated database (Flyway plus Testcontainers) so the code and schema agree; verify licensing for your database edition before recording (open-source edition supports PostgreSQL).

**Show**
```java
var rows = dsl.select(PRODUCT.CATEGORY_ID, DSL.sum(ORDER_ITEM.PRICE_CENTS))
              .from(ORDER_ITEM).join(PRODUCT).on(PRODUCT.ID.eq(ORDER_ITEM.PRODUCT_ID))
              .groupBy(PRODUCT.CATEGORY_ID)
              .fetch();
```

**Check:** What does the compiler catch that a SQL string would not? *(A renamed column or a type mismatch.)*

---

## MID-022-L03 · Choosing a persistence approach (8 min)
**Goal:** compare JDBC, jOOQ, and JPA and justify a choice.

**Key points**
- JDBC / `JdbcClient` / `JdbcTemplate`: full control, minimal dependencies, manual mapping and no compile-time checks.
- jOOQ: type-safe SQL, great for reports and complex queries; you manage writes and mapping yourself.
- JPA: productivity for CRUD and aggregates; the cost is hidden SQL and the learning curve.
- Decide per use case: team skill, query complexity, write shape, performance needs.
- Mixing is fine if each module has one approach and transaction management is shared.

**Show:** a decision table with columns: use case, complexity, writes/reads, choice, reason.

**Check:** Which tool for a 10-join report with window functions? *(jOOQ, or plain SQL, rather than JPA.)*

---

## MID-022-L04 · Read models and CQRS-lite (10 min)
**Goal:** serve queries from a dedicated read model inside one service.

**Key points**
- CQRS-lite: separate the write model (entities, rules) from a read model (tables or views shaped for queries), in the same service and database.
- Update the read model in the same transaction, or from domain events after commit, or by periodic refresh.
- Choose by staleness tolerance: same transaction is consistent; events are eventually consistent.
- No event sourcing and no separate database is needed for simple cases.
- Include a rebuild path: recompute the read model from the write tables.

**Show:** a diagram: `POST /orders` writes `orders` and publishes `OrderPlaced`; a listener updates `dashboard_daily(day, orders, revenue)`; `GET /admin/dashboard` reads only that table.

**Check:** Does CQRS-lite require event sourcing? *(No.)*

---

## MID-022-L05 · Demo: rewriting the sales report with jOOQ (12 min)
**Goal:** port the SQL sales report to jOOQ and compare approaches.

**Steps**
1. Show the report as plain SQL from MID-011 (CTE and window function).
2. Add the jOOQ Gradle/Maven plugin; generate classes from the Flyway-migrated database.
3. Rewrite the query using `DSL.with(...)`, `DSL.rank().over(...)`, and fetch into a record.
4. **Planned mistake:** change a column name in a migration without regenerating classes; show the build failing, then regenerate. Explain this is the safety net.
5. Compare results with the original query and note readability and refactor safety.

Prepares MID-022-LAB1.

**Check:** What happens to the jOOQ code when a column is renamed and classes regenerated? *(The compiler flags every use of the old column.)*
