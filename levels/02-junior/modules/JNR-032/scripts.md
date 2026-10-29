# JNR-032 · ORM pitfalls — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** grocery shopping: one trip with a full list versus a hundred trips for one item each.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-032-L01 · The N+1 problem (12 min)
**Goal:** recognize N+1 in logs and tests.

**Key points**
- N+1: one query loads N parents, then one more query per parent loads its children (or relation).
- 100 orders become 1 + 100 = 101 queries.
- It hides in lazy relations touched in a loop, or in mapping code that reads `order.getCustomer().getName()`.
- Detect it in the SQL log (repeated similar selects) or with a query counter in tests.
- It is fast on a developer machine with 5 rows and slow in production.

**Show**
```java
List<Order> orders = orderRepository.findAll();          // 1 query
for (Order o : orders) {
    System.out.println(o.getLines().size());             // +1 query per order
}
```

**Check:** How many queries for 100 orders with N+1? *(101.)*

---

## JNR-032-L02 · Fetch joins and entity graphs (12 min)
**Goal:** load related data in one query.

**Key points**
- `join fetch` in JPQL loads the relation together with the parent.
- `@EntityGraph(attributePaths = "lines")` on a repository method does the same without writing JPQL.
- A projection that selects only needed columns can avoid loading entities at all.
- Fetch what the use case needs, not everything.
- Verify with the log or the query counter.

**Show**
```java
@Query("select distinct o from Order o join fetch o.lines where o.customer.id = :cid")
List<Order> findWithLines(@Param("cid") Long cid);

@EntityGraph(attributePaths = {"lines", "customer"})
List<Order> findByStatus(OrderStatus status);
```

**Check:** Name two ways to fix N+1 besides projections. *(Fetch join and entity graph.)*

---

## JNR-032-L03 · Lazy loading and its exception (10 min)
**Goal:** explain lazy versus eager and `LazyInitializationException`.

**Key points**
- Lazy: the relation is loaded on first access, using a proxy placeholder.
- Eager: loaded immediately with the parent, always, even when unused.
- `LazyInitializationException`: you touched a lazy relation after the persistence context closed.
- Do not "fix" it by making everything `EAGER`; that creates huge hidden queries.
- Load what you need inside the service transaction, or use a projection/DTO.

**Show**
```java
Order o = orderService.find(1L);        // transaction ended here
o.getLines().size();                    // LazyInitializationException
```

**Check:** Why does `LazyInitializationException` happen? *(The relation was read after the session closed.)*

---

## JNR-032-L04 · Pagination with collections (8 min)
**Goal:** avoid fetch-joining a collection with paging.

**Key points**
- A join fetch on a collection multiplies parent rows (one row per child).
- Hibernate cannot page that in SQL, so it loads everything and pages in memory (warning `HHH000104`: verify wording for your version).
- That can exhaust memory on big tables.
- Safe approach: page the parent ids first, then load children for those ids with a second query.
- Alternative: use `@BatchSize` or a projection.

**Show**
```java
Page<Long> ids = orderRepository.findIds(pageable);                 // page the parents only
List<Order> orders = orderRepository.findWithLinesByIdIn(ids.getContent()); // fetch join
```

**Check:** Why is `join fetch` on a collection plus paging dangerous? *(Paging happens in memory after loading all rows.)*

---

## JNR-032-L05 · Open Session in View: why to turn it off (8 min)
**Goal:** understand and disable Open Session in View (OSIV).

**Key points**
- OSIV keeps the persistence context open until the HTTP response is written.
- It hides `LazyInitializationException`, but lets queries run in controllers and JSON serialization.
- That means unplanned N+1 and a database connection held for the whole request.
- Spring Boot enables it by default (with a startup warning).
- Set `spring.jpa.open-in-view=false` and load data explicitly in services.

**Show**
```yaml
spring:
  jpa:
    open-in-view: false
```

**Check:** What does OSIV hide? *(Lazy loading outside the service layer.)*

---

## JNR-032-L06 · Demo: catching N+1 with a query-count test (12 min)
**Goal:** write a test that fails when queries multiply; prepares JNR-032-LAB1.

**Steps**
1. Seed 100 orders with lines in a test.
2. Add a query counter (Hibernate statistics or a datasource-proxy library; verify your choice).
3. Call the order-history endpoint and print the count: 101.
4. Write the assertion `queryCount <= 2`; the test fails.
5. **Planned mistake:** add `fetch = EAGER` and show the count is still high; revert it.
6. Add the `join fetch` or entity graph; the test passes.

---

## JNR-032-L07 · Demo: fixing lazy loading without Open Session in View (12 min)
**Goal:** keep lazy relations working with OSIV off; prepares JNR-032-LAB1.

**Steps**
1. Set `spring.jpa.open-in-view=false`; call an endpoint that returns an entity with lazy lines.
2. See `LazyInitializationException` in the response.
3. **Planned mistake:** change the relation to `EAGER`; show the extra queries everywhere.
4. Revert; add an entity graph or a DTO projection in the service method.
5. Return a response DTO built inside the transaction; the exception is gone and the query count is low.
