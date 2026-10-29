# JNR-029 · Spring Data JPA — Exercises and lab

## Lab
### JNR-029-LAB1 · Catalog on JPA
**Outcomes:** 1–4 · **Time:** ~3 h
1. Move products and categories to Spring Data JPA repositories.
2. Add `findBySku` (derived) and a paged search by name, category, and price range (`@Query`).
3. Return a `ProductListItem` projection for the listing; map to the API response in the service.
4. Keep all existing endpoints and JSON unchanged.
5. Run the existing API tests plus a repository test for the search.

**Acceptance:** API contract unchanged; tests pass.

## Exercises (assessment: implement three queries from requirements)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-029-EX01 | 1 | Declare `CustomerRepository` and use `findById`, `save`, `count`; explain who implements it. |
| JNR-029-EX02 | 2 | Write derived queries: products by status, products with name containing text (ignore case). |
| JNR-029-EX03 | 2 | Rewrite a 60-character derived method as a `@Query`. |
| JNR-029-EX04 | 3 | Write a JPQL query with named parameters: orders of a customer between two dates. |
| JNR-029-EX05 | 3 | Write a native query counting products per category and explain why native was chosen. |
| JNR-029-EX06 | 4 | Return a record projection and a `Page` sorted by price descending. |

## Solutions
- **EX01** `interface CustomerRepository extends JpaRepository<Customer, Long> {}`; Spring Data creates a proxy implementation at startup.
- **EX02** `List<Product> findByStatus(ProductStatus s);` and `List<Product> findByNameContainingIgnoreCase(String text);`
- **EX03** `@Query("select p from Product p where p.category.id = :cid and p.price.amount <= :max order by p.name") List<Product> findAffordable(@Param("cid") Long cid, @Param("max") BigDecimal max);`
- **EX04** `select o from Order o where o.customer.id = :cid and o.createdAt between :from and :to`.
- **EX05** `select category_id, count(*) from product group by category_id` with `nativeQuery = true`; chosen for a reporting aggregate returned as a projection, not because it is the default.
- **EX06** `Page<ProductListItem> list(Pageable p);` called with `PageRequest.of(0, 20, Sort.by(Sort.Direction.DESC, "price.amount"))` (check the property path against your mapping).
- Assessment covers EX02, EX04, and EX06 (three queries from requirements).
