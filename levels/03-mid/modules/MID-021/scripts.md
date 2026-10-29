# MID-021 · Advanced Hibernate — Lecture scripts

**Video:** 58 min · **Running project:** Shop Platform (nightly price-update job and order queries)
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-021-L01 · Fetch plans per use case (10 min)
**Goal:** load exactly the data each use case needs.

**Key points**
- Associations should be `LAZY` by default; decide the fetch per use case, not on the mapping.
- `JOIN FETCH` or an entity graph loads an association in one query; avoids N+1.
- Fetching two collections at once creates a cartesian product; fetch one collection and batch the others (`@BatchSize` or `default_batch_fetch_size`).
- For read-only screens, a DTO projection selects only needed columns and skips the persistence context.
- Pagination with a fetched collection is done in memory by Hibernate (warning `HHH000104`); paginate ids first.

**Show**
```java
@EntityGraph(attributePaths = "items")
Optional<Order> findWithItemsById(Long id);

@Query("select new com.shop.OrderSummary(o.id, o.total, c.name) from Order o join o.customer c")
List<OrderSummary> summaries();
```

**Check:** Why a DTO projection for a list screen? *(It loads only the needed columns and creates no managed entities.)*

---

## MID-021-L02 · Batching inserts and updates (10 min)
**Goal:** send many statements to the database in few round trips.

**Key points**
- Set `hibernate.jdbc.batch_size` (for example 50) and `order_inserts`/`order_updates` to group statements.
- `GenerationType.IDENTITY` forces Hibernate to insert each row immediately to get the id, which disables insert batching.
- Use a sequence (`GenerationType.SEQUENCE` with `allocationSize` matching the sequence increment) to batch inserts.
- With the PostgreSQL driver, `reWriteBatchedInserts=true` merges inserts further (verify driver option before recording).
- Flush and clear the persistence context every batch to keep memory flat.

**Show**
```yaml
spring.jpa.properties.hibernate.jdbc.batch_size: 50
spring.jpa.properties.hibernate.order_updates: true
```

**Check:** Why does `IDENTITY` stop insert batching? *(Hibernate must execute each insert at once to learn the generated id.)*

---

## MID-021-L03 · Second-level and query caches (12 min)
**Goal:** decide whether a cache is worth it.

**Key points**
- First-level cache: the persistence context, per transaction; always on.
- Second-level cache: shared across sessions through a provider (Ehcache, Infinispan, Caffeine via JCache); needs `@Cache` per entity.
- Good candidates: read-mostly reference data (countries, categories). Bad: frequently changed or large mutable entities.
- Query cache stores result ids and is invalidated on any write to the tables involved; rarely a win.
- Multi-instance deployments need a distributed or invalidating provider; often a dedicated cache (Redis, later modules) is simpler.
- A cache hides bugs and adds staleness; measure hit ratio before keeping it.

**Show:** a decision table: entity, read/write ratio, staleness allowed, cache yes/no.

**Check:** Which entity suits a second-level cache: product stock or country list? *(Country list; stock changes constantly.)*

---

## MID-021-L04 · Entity states revisited: merge vs persist (8 min)
**Goal:** handle detached entities correctly.

**Key points**
- States: transient (new), managed (in the persistence context), detached (loaded earlier, session closed), removed.
- `persist` makes a new entity managed; `merge` copies the state of a detached entity onto a managed copy and returns that copy.
- Use the returned object from `merge`; the argument stays detached.
- Spring Data `save` calls `persist` for new entities and `merge` otherwise; `merge` of an unknown id may do an extra `SELECT`.
- Prefer loading the entity inside the transaction and changing it (dirty checking) over merging DTO-built entities.

**Show**
```java
Product managed = em.merge(detached);   // use 'managed', not 'detached'
```

**Check:** What does `merge` return? *(The managed copy; the passed object stays detached.)*

---

## MID-021-L05 · Hibernate statistics (6 min)
**Goal:** measure statements and cache use in tests.

**Key points**
- `hibernate.generate_statistics=true` exposes counts of statements, entity loads, flushes, and cache hits.
- Assert statement counts in tests to catch N+1 regressions.
- Log SQL with `org.hibernate.SQL` at debug level rather than `show-sql` in production.
- Libraries such as datasource-proxy can also count statements (verify choice before recording).

**Show**
```java
Statistics stats = sessionFactory.getStatistics();
stats.clear();
service.loadOrders();
assertThat(stats.getPrepareStatementCount()).isLessThanOrEqualTo(2);
```

**Check:** Why assert statement counts in tests? *(To catch N+1 queries before production.)*

---

## MID-021-L06 · Demo: 10× faster bulk updates with batching (12 min)
**Goal:** speed up the nightly price update without leaving JPA.

**Steps**
1. Baseline: load 100 000 products, change the price, `saveAll`; record statement count and time with statistics.
2. Enable `batch_size=50` and `order_updates`; measure again.
3. Page through the data and `flush()` + `clear()` every 50 rows to keep memory stable.
4. **Planned mistake:** batching is set but entities use `IDENTITY` and the job inserts; inserts stay unbatched. Fix: switch to a sequence for insert jobs (updates are not affected by `IDENTITY`).
5. Compare final statement counts and elapsed time (target about 10× faster).
6. Mention the alternative of one set-based `UPDATE` statement when entity logic is not needed.

Prepares MID-021-LAB1.

**Check:** What was the statement count change after batching? *(Many single-row statements became far fewer batched executions.)*
