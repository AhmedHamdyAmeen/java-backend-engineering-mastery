# JNR-028 · JPA and Hibernate — Exercises and lab

## Lab
### JNR-028-LAB1 · Entities for Shop
**Outcomes:** 1–5 · **Time:** ~4 h
1. Map `Category` and `Product` (with `Money` as an embeddable and a `status` enum) onto the existing `schema.sql`; keep `ddl-auto=none`.
2. Enable SQL logging.
3. In a transactional test run: create a product, update its price, read it again in a new transaction.
4. For each statement in the log, write one sentence on why it ran at that moment.
5. Write a safe `equals`/`hashCode` for `Product` and a test that adds it to a `HashSet` before and after saving.

**Acceptance:** the written explanation matches the SQL log statement by statement.

## Exercises (assessment: "predict the SQL")
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-028-EX01 | 1 | Add `@Entity`, `@Id`, and column mappings to a `Customer` class with a status enum. |
| JNR-028-EX02 | 1 | Turn `Address(street, city, zip)` into an embeddable used by `Customer`. |
| JNR-028-EX03 | 2 | Label each object as transient, managed, detached, or removed in a given 10-line code listing. |
| JNR-028-EX04 | 3 | Predict the SQL (statements and order) for: load a product, change the price, call a JPQL query, commit. |
| JNR-028-EX05 | 4 | Fix an entity with Lombok `@Data` by writing correct `equals`/`hashCode`. |
| JNR-028-EX06 | 5 | Turn on SQL logging with parameter values and explain one logged `insert`. |
| JNR-028-EX07 | 1, 3 | Explain why `IDENTITY` disables insert batching and what to use instead. |

## Solutions
- **EX01** `@Entity @Table(name="customer")`, `@Id @GeneratedValue private Long id;`, `@Enumerated(EnumType.STRING) private CustomerStatus status;`, protected no-arg constructor.
- **EX02** `@Embeddable record Address(...)` and `@Embedded private Address address;` in `Customer`.
- **EX03** `new` objects are transient; objects loaded or persisted inside the open transaction are managed; those from a closed context are detached; those after `remove` are removed.
- **EX04** `select ... from product where id=?`; then (auto flush before the query) `update product set price=? where id=?`; then the query `select`; commit has nothing left to flush.
- **EX05** Remove `@Data`; use `equals` on non-null id with `getClass().hashCode()`, or a stable business key such as `sku`.
- **EX06** `logging.level.org.hibernate.SQL=DEBUG` and `logging.level.org.hibernate.orm.jdbc.bind=TRACE` (verify property names for your Hibernate version).
- **EX07** With `IDENTITY` the id exists only after the insert, so Hibernate must send each insert immediately; `SEQUENCE` lets it fetch ids first and batch inserts.
