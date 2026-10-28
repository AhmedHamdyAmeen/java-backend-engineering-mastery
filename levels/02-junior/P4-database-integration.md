# JNR-P4 — Database Integration

**Phase goal:** the learner persists data correctly with PostgreSQL from Spring — choosing between JDBC and JPA, controlling transactions, evolving the schema with migrations, and avoiding the classic ORM performance traps.

**Running project:** *Shop API* replaces its in-memory repositories with PostgreSQL. A local PostgreSQL install is used until Docker Compose arrives in JNR-050.

**Phase total:** ~10.6 h video · ~26.5 h practice

> **Teaching note:** schema migrations (JNR-033) come late in the roadmap's order. Until then, labs apply the provided `schema.sql` manually; never use Hibernate's `ddl-auto=update` outside throwaway experiments. JNR-033 converts everything to versioned migrations.

---

### JNR-025 · JDBC
`n: 79` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-055

**Learning outcomes** — the learner can:
1. Obtain connections from a `DataSource` (connection pool) instead of `DriverManager`.
2. Execute batch inserts and retrieve generated keys.
3. Map SQL types to Java types correctly (`numeric` ↔ `BigDecimal`, `timestamptz` ↔ `Instant`/`OffsetDateTime`).
4. Prevent SQL injection in dynamic queries (e.g., user-chosen sort columns via allow-lists).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-025-L01 | From `DriverManager` to `DataSource` | 8 |
| JNR-025-L02 | Generated keys and batching | 10 |
| JNR-025-L03 | Type mapping pitfalls | 10 |
| JNR-025-L04 | Dynamic SQL without injection | 12 |
| JNR-025-L05 | Demo: batch import and timing comparison | 10 |

**Lab** — `JNR-025-LAB1` *Bulk import:* import 10,000 products from CSV with batched inserts; compare timing with row-by-row inserts. Acceptance: measured speed-up; no concatenated user input.

**Common mistakes:** `double` for prices; concatenating `ORDER BY` columns; one connection per statement.

**Assessment:** fix an injectable dynamic query.

**Career relevance:** understanding what every higher-level abstraction does underneath.

---

### JNR-026 · Spring JDBC
`n: 80` · **Video:** 50 min · **Practice:** 2.5 h

**Prerequisites:** JNR-011, JNR-025

**Learning outcomes** — the learner can:
1. Configure a `DataSource` through Spring Boot properties.
2. Query and update with `JdbcClient`/`JdbcTemplate` and named parameters.
3. Map rows to records with `RowMapper` or automatic mapping.
4. Explain how Spring translates `SQLException`s into its `DataAccessException` hierarchy.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-026-L01 | DataSource configuration in Boot | 8 |
| JNR-026-L02 | `JdbcClient` and `JdbcTemplate` | 12 |
| JNR-026-L03 | Mapping rows | 10 |
| JNR-026-L04 | Exception translation | 10 |
| JNR-026-L05 | Demo: replacing the in-memory repository with Spring JDBC | 10 |

**Lab** — `JNR-026-LAB1` *Products on PostgreSQL:* implement `ProductRepository` with Spring JDBC behind the existing interface. Acceptance: no controller or service changes needed; integration test against a real database.

**Common mistakes:** leaking `ResultSet` handling into services; catching `DataAccessException` everywhere.

**Assessment:** implement a reporting query repository method.

**Career relevance:** JDBC remains the right choice for reporting and bulk work (MID-022).

---

### JNR-027 · ORM fundamentals
`n: 81` · **Video:** 45 min · **Practice:** 1 h

**Prerequisites:** JNR-026

**Learning outcomes** — the learner can:
1. Explain the object-relational impedance mismatch (identity, inheritance, associations, granularity).
2. Describe what an ORM automates and what it costs.
3. Explain the persistence context as an identity map and unit of work.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-027-L01 | Objects vs tables | 10 |
| JNR-027-L02 | What an ORM does | 10 |
| JNR-027-L03 | The persistence context | 15 |
| JNR-027-L04 | Demo: watching the persistence context with SQL logging | 10 |

**Lab** — `JNR-027-LAB1` *Mismatch exercise:* list every piece of mapping code in the Spring JDBC repository and predict which an ORM would remove and which risks it would add. Acceptance: reasoned list.

**Common mistakes:** believing an ORM removes the need to know SQL.

**Assessment:** quiz.

**Career relevance:** basis for diagnosing ORM issues (JNR-032, MID-021).

---

### JNR-028 · JPA and Hibernate
`n: 82` · **Video:** 84 min · **Practice:** 4 h

**Prerequisites:** JNR-027

**Learning outcomes** — the learner can:
1. Map entities with `@Entity`, `@Id`, generated identifiers, columns, enums, and embedded value objects.
2. Describe entity states (transient, managed, detached, removed) and transitions.
3. Explain dirty checking and flush timing, and predict when SQL is issued.
4. Implement `equals`/`hashCode` safely for entities.
5. Enable SQL logging and read the generated statements.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-028-L01 | Mapping an entity | 12 |
| JNR-028-L02 | Identifiers and generation strategies | 10 |
| JNR-028-L03 | Embeddables and value objects | 8 |
| JNR-028-L04 | Entity lifecycle | 12 |
| JNR-028-L05 | Dirty checking and flushing | 10 |
| JNR-028-L06 | Entity equality | 8 |
| JNR-028-L07 | Demo: mapping Shop entities and predicting the SQL | 12 |
| JNR-028-L08 | Demo: entity states in the debugger | 12 |

**Lab** — `JNR-028-LAB1` *Entities for Shop:* map `Product`, `Category`, and `Money` (embeddable); log SQL and explain each statement during a create-update-read sequence. Acceptance: explanation matches the log.

**Common mistakes:** entities as API DTOs; `GenerationType.IDENTITY` without understanding batching impact; Lombok `@Data` on entities.

**Assessment:** "predict the SQL" exercise.

**Career relevance:** the default persistence stack for Spring services.

---

### JNR-029 · Spring Data JPA
`n: 83` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-028

**Learning outcomes** — the learner can:
1. Define repositories extending `JpaRepository` and explain the generated implementation.
2. Write derived queries and recognize when a name becomes unreadable.
3. Write JPQL and native queries with `@Query` and parameters.
4. Return projections (interface or record) for read-only views and use `Pageable`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-029-L01 | Repository interfaces | 10 |
| JNR-029-L02 | Derived queries | 10 |
| JNR-029-L03 | JPQL with `@Query` | 10 |
| JNR-029-L04 | Native queries | 8 |
| JNR-029-L05 | Projections and paging | 12 |
| JNR-029-L06 | Demo: migrating the catalog to Spring Data JPA | 12 |
| JNR-029-L07 | Demo: projections for paged listings | 12 |

**Lab** — `JNR-029-LAB1` *Catalog on JPA:* move products and categories to Spring Data JPA, with paged search by name, category, and price range using a projection for listings. Acceptance: API contract unchanged; tests pass.

**Common mistakes:** 60-character derived method names; native queries by default; returning entities to controllers.

**Assessment:** implement three queries from requirements.

**Career relevance:** daily work; advanced Hibernate in MID-021.

---

### JNR-030 · Entity relationships
`n: 84` · **Video:** 79 min · **Practice:** 4 h

**Prerequisites:** BEG-049, JNR-029

**Learning outcomes** — the learner can:
1. Map one-to-one, one-to-many, many-to-one, and many-to-many relationships.
2. Identify the owning side and keep bidirectional associations in sync with helper methods.
3. Choose cascade types and orphan removal for aggregates, and explain the risks.
4. Replace a many-to-many with an explicit join entity when the link has data.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-030-L01 | Many-to-one: the default relationship | 10 |
| JNR-030-L02 | One-to-many and the owning side | 12 |
| JNR-030-L03 | One-to-one | 7 |
| JNR-030-L04 | Many-to-many and join entities | 10 |
| JNR-030-L05 | Cascades and orphan removal | 10 |
| JNR-030-L06 | Unidirectional by default | 6 |
| JNR-030-L07 | Demo: mapping Order and OrderLine as an aggregate | 12 |
| JNR-030-L08 | Demo: cascade and orphan-removal surprises | 12 |

**Lab** — `JNR-030-LAB1` *Orders:* `Order` with `OrderLine`s (cascade + orphan removal), many-to-one to `Customer`, and line references to `Product`. Acceptance: removing a line from the collection deletes it; no cascade from order to product.

**Common mistakes:** `CascadeType.ALL` everywhere; bidirectional mappings that are never synchronized; `@ManyToMany` with extra columns.

**Assessment:** map a provided ER diagram.

**Career relevance:** aggregates in DDD (MID-060).

---

### JNR-031 · Transactions
`n: 85` · **Video:** 79 min · **Practice:** 3 h

**Prerequisites:** BEG-051, JNR-029

**Learning outcomes** — the learner can:
1. Explain ACID with concrete failure scenarios.
2. Place `@Transactional` at the service layer around a business operation.
3. Explain default rollback rules (unchecked vs checked) and configure them.
4. Explain the proxy mechanism and diagnose self-invocation failures.
5. Use read-only transactions and keep transactions short (no remote calls inside).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-031-L01 | ACID by example | 10 |
| JNR-031-L02 | Transaction boundaries | 10 |
| JNR-031-L03 | `@Transactional` and proxies | 12 |
| JNR-031-L04 | Rollback rules | 8 |
| JNR-031-L05 | Propagation basics | 8 |
| JNR-031-L06 | Long transactions and remote calls | 7 |
| JNR-031-L07 | Demo: making checkout atomic | 12 |
| JNR-031-L08 | Demo: finding the self-invocation bug | 12 |

**Lab** — `JNR-031-LAB1` *Place order:* placing an order reserves stock and creates the order atomically; a failure mid-way leaves no partial data. Includes the canonical money-transfer exercise with a planted self-invocation bug to fix. Acceptance: failure tests prove atomicity.

**Common mistakes:** `@Transactional` on private methods or controllers; calling a payment API inside a transaction; swallowing exceptions so nothing rolls back.

**Assessment:** fix a broken transaction implementation and explain why it failed.

**Career relevance:** junior implementation; isolation and locking in MID-015/016.

---

### JNR-032 · ORM pitfalls
`n: 86` · **Video:** 74 min · **Practice:** 3 h

**Prerequisites:** JNR-030

**Learning outcomes** — the learner can:
1. Detect N+1 queries from SQL logs or a query counter in tests.
2. Fix N+1 with fetch joins, entity graphs, or projections.
3. Explain lazy vs eager loading and why `LazyInitializationException` happens.
4. Explain why fetch-joining collections with pagination is dangerous and apply a safe alternative.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-032-L01 | The N+1 problem | 12 |
| JNR-032-L02 | Fetch joins and entity graphs | 12 |
| JNR-032-L03 | Lazy loading and its exception | 10 |
| JNR-032-L04 | Pagination with collections | 8 |
| JNR-032-L05 | Open Session in View: why to turn it off | 8 |
| JNR-032-L06 | Demo: catching N+1 with a query-count test | 12 |
| JNR-032-L07 | Demo: fixing lazy loading without Open Session in View | 12 |

**Lab** — `JNR-032-LAB1` *Fix the order list:* a provided order-history endpoint issues 101 queries for 100 orders; reduce it to at most 2 with a test asserting the query count. Acceptance: test fails before, passes after.

**Common mistakes:** switching everything to `EAGER`; leaving Open Session in View enabled.

**Assessment:** diagnose a slow endpoint from logs.

**Career relevance:** common production issue; MID-021 goes deeper.

---

### JNR-033 · Schema migrations
`n: 87` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-051, JNR-028

**Learning outcomes** — the learner can:
1. Version the schema with Flyway migrations that run on startup.
2. Write forward-only migrations and explain why applied migrations are never edited.
3. Separate reference/seed data from test data.
4. Validate entity mappings against the migrated schema (`ddl-auto=validate`).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-033-L01 | Why the schema needs version control | 8 |
| JNR-033-L02 | Flyway basics | 12 |
| JNR-033-L03 | Writing safe migrations | 10 |
| JNR-033-L04 | Seed data | 5 |
| JNR-033-L05 | Liquibase in brief | 5 |
| JNR-033-L06 | Demo: baselining Shop with Flyway and adding V2 | 10 |

**Lab** — `JNR-033-LAB1` *Migrate Shop:* convert the schema to Flyway (`V1__baseline.sql`), then add a `sku` column with a backfill in `V2`. Acceptance: fresh database and existing database both reach the same state.

**Common mistakes:** editing an applied migration; `ddl-auto=update` in production.

**Assessment:** write a migration for a new requirement.

**Career relevance:** zero-downtime migrations (MID-020).

---

### JNR-034 · Database constraints
`n: 88` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** JNR-033

**Learning outcomes** — the learner can:
1. Enforce invariants in the database with unique, foreign-key, not-null, and check constraints.
2. Translate constraint violations into meaningful API errors (e.g., 409 for duplicates).
3. Explain why application-level checks alone fail under concurrency.
4. Create indexes for foreign keys and common lookups, and verify use with `EXPLAIN`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-034-L01 | The database as the last line of defense | 8 |
| JNR-034-L02 | Unique and check constraints | 10 |
| JNR-034-L03 | Constraint violations to API errors | 8 |
| JNR-034-L04 | Indexes: a first look | 14 |
| JNR-034-L05 | Demo: racing two requests against a unique constraint | 10 |

**Lab** — `JNR-034-LAB1` *Race the duplicate:* two concurrent requests create the same SKU; show the application check failing and the unique constraint saving you, mapped to 409. Acceptance: concurrent test reliably produces one success and one 409.

**Common mistakes:** "check then insert" without a constraint; indexing every column.

**Assessment:** add constraints and indexes to a schema from requirements.

**Career relevance:** index internals (MID-012) and data integrity (SRC-014).
