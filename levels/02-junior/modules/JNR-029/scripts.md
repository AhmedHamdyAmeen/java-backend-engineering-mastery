# JNR-029 · Spring Data JPA — Lecture scripts

**Video:** 74 min · **Analogy used throughout:** an order form at a restaurant: you write what you want, the kitchen (generated code) prepares it.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-029-L01 · Repository interfaces (10 min)
**Goal:** get a working repository by declaring an interface.

**Key points**
- Extend `JpaRepository<Entity, IdType>`; Spring generates the implementation at startup.
- You get `findById`, `findAll`, `save`, `deleteById`, `count`, and paging for free.
- `save` inserts a new entity or merges an existing one; for managed entities it is not needed for updates.
- `findById` returns an `Optional`.
- Repositories belong to the persistence layer; services use them, controllers do not.

**Show**
```java
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

**Check:** Who writes the implementation class? *(Spring Data, generated at runtime.)*

---

## JNR-029-L02 · Derived queries (10 min)
**Goal:** write queries from method names, and know when to stop.

**Key points**
- Spring parses names like `findByNameContainingIgnoreCase` into JPQL.
- Keywords: `And`, `Or`, `Between`, `LessThan`, `OrderBy`, `Containing`, `IsNull`.
- Great for one or two conditions.
- When the name grows past about 3 conditions, it is hard to read: switch to `@Query`.
- Typos in property names fail at startup, which is a useful early warning.

**Show**
```java
List<Product> findByCategoryIdAndPriceAmountLessThanOrderByNameAsc(Long categoryId, BigDecimal max); // too long
Optional<Product> findBySku(String sku);                                                             // good
```

**Check:** When should you replace a derived query with `@Query`? *(When the name becomes hard to read, around three or more conditions.)*

---

## JNR-029-L03 · JPQL with `@Query` (10 min)
**Goal:** write explicit queries on entities.

**Key points**
- JPQL queries entities and their fields, not tables and columns.
- Use named parameters with `@Param`.
- Optional filters can be written as `(:name is null or lower(p.name) like lower(concat('%', :name, '%')))`.
- Never concatenate input; parameters are safe.
- Add `@Modifying` for update/delete queries (they bypass the persistence context, so use sparingly).

**Show**
```java
@Query("""
    select p from Product p
    where p.category.id = :categoryId and p.price.amount <= :max
    order by p.name
    """)
List<Product> findAffordable(@Param("categoryId") Long categoryId, @Param("max") BigDecimal max);
```

**Check:** Does JPQL use table names or entity names? *(Entity names.)*

---

## JNR-029-L04 · Native queries (8 min)
**Goal:** use plain SQL when JPQL cannot express the query.

**Key points**
- `@Query(nativeQuery = true)` runs real SQL against the database.
- Use it for database-specific features (window functions, full-text search) and heavy reports.
- It is not portable and bypasses entity names; refactoring does not update it.
- Default to JPQL or derived queries; native is the exception.
- Pair native queries with projections, not entities, for reports.

**Show**
```java
@Query(value = "select c.name as category, count(*) as total from product p " +
               "join category c on c.id = p.category_id group by c.name", nativeQuery = true)
List<CategoryCount> countPerCategory();
```

**Check:** Should native queries be your default? *(No; use them only when needed.)*

---

## JNR-029-L05 · Projections and paging (12 min)
**Goal:** return only the columns a screen needs, one page at a time.

**Key points**
- A projection is a read-only view: an interface with getters or a record.
- It selects only the needed columns, no entity tracking.
- `Pageable` carries page number, size, and sort; `PageRequest.of(0, 20, Sort.by("name"))`.
- Return `Page<T>` (with total count) or `Slice<T>` (no count query).
- Map to a response DTO in the service; never return entities from controllers.

**Show**
```java
public record ProductListItem(Long id, String name, BigDecimal priceAmount) {}

@Query("select new com.shop.ProductListItem(p.id, p.name, p.price.amount) from Product p")
Page<ProductListItem> list(Pageable pageable);
```

**Check:** What does `Page` have that `Slice` does not? *(The total count.)*

---

## JNR-029-L06 · Demo: migrating the catalog to Spring Data JPA (12 min)
**Goal:** move products and categories from Spring JDBC to Spring Data JPA; prepares JNR-029-LAB1.

**Steps**
1. Keep the `ProductRepository` contract the service uses; add JPA entities from JNR-028.
2. Create `ProductJpaRepository extends JpaRepository` and adapt the existing implementation to call it.
3. Add `findBySku` and a name search with `@Query`.
4. **Planned mistake:** write a 60-character derived method name; show it, then replace it with `@Query`.
5. Run the API tests; the contract is unchanged.
6. Remove the old Spring JDBC code once tests pass.

---

## JNR-029-L07 · Demo: projections for paged listings (12 min)
**Goal:** build the paged, filtered product list; prepares JNR-029-LAB1.

**Steps**
1. Define `ProductListItem` (id, name, price, category name).
2. Write one `@Query` with optional name, category, and price-range filters and a `Pageable` parameter.
3. Call it from the service with `PageRequest.of(page, size, Sort.by("name"))`.
4. **Planned mistake:** return the entity from the controller; show the extra columns and lazy-loading trouble, then switch to the projection.
5. Check the SQL log: only the listed columns are selected, plus a count query.
