# JNR-013 · Layered architecture — Lecture scripts

**Video:** 79 min · **Analogy used throughout:** a restaurant: the waiter takes orders (controller), the kitchen cooks (service), the pantry stores ingredients (repository), and the menu card is not the same as the food (DTO vs domain).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-013-L01 · Why layers (8 min)
**Goal:** explain why we split code into layers.

**Key points**
- One class doing HTTP, rules, and data access is hard to read, test, and change.
- Each layer has one job and talks only to the layer below.
- Flow: controller → service → repository; the domain model is shared by service and repository.
- Layers let you change one part (say, the database) without rewriting the rest.

**Show:** a diagram: HTTP → Controller → Service → Repository → storage, with arrows pointing down only.

**Check:** Should a repository call a controller? *(No; dependencies go downward only.)*

---

## JNR-013-L02 · Controllers: the HTTP edge (10 min)
**Goal:** write a thin controller.

**Key points**
- A controller translates HTTP to a method call and the result back to HTTP.
- It handles paths, methods, status codes, and request/response bodies.
- It contains no business rules and no database code.
- `@RestController` returns data (JSON), not pages.

**Show**
```java
@RestController
@RequestMapping("/products")
class ProductController {
    private final ProductService service;
    ProductController(ProductService service) { this.service = service; }

    @GetMapping("/{id}")
    ProductResponse get(@PathVariable long id) { return service.get(id); }
}
```

**Check:** Where does "a discount cannot exceed 50%" go? *(In the service, not the controller.)*

---

## JNR-013-L03 · Services: business logic and orchestration (10 min)
**Goal:** place rules and workflows in the service.

**Key points**
- A service holds business rules and coordinates repositories and other services.
- It works with domain objects and plain values, not HTTP types.
- A service never returns `ResponseEntity` or reads request headers.
- Keep services stateless (JNR-010).

**Show**
```java
@Service
class ProductService {
    private final ProductRepository repo;
    ProductService(ProductRepository repo) { this.repo = repo; }
    ProductResponse get(long id) {
        return ProductMapper.toResponse(repo.findById(id).orElseThrow(() -> new ProductNotFound(id)));
    }
}
```

**Check:** Should a service return `ResponseEntity`? *(No; that is an HTTP concern for the edge.)*

---

## JNR-013-L04 · Repositories: data access behind an interface (8 min)
**Goal:** hide storage behind an interface.

**Key points**
- The repository interface says what you can store and find, not how.
- In this phase the implementation is in memory (a `Map`); JNR-P4 swaps in a database.
- The service depends on the interface, so it does not change when storage does.
- `@Repository` marks the implementation.

**Show**
```java
interface ProductRepository {
    Optional<Product> findById(long id);
    List<Product> findAll();
}
```

**Check:** Why return `Optional`? *(A product may not exist; the type says so.)*

---

## JNR-013-L05 · DTOs vs domain models (12 min)
**Goal:** keep the API shape separate from the domain.

**Key points**
- A DTO (data transfer object) is the shape of a request or response.
- The domain model holds business data and rules; it may have fields clients must never see.
- If you serialize the domain object directly, any internal change breaks API clients.
- Use different DTOs for create, update, and response.
- Map in one place with a mapper (manual method or a library).

**Show**
```java
record ProductResponse(long id, String name, BigDecimal price) {}
class Product { long id; String name; BigDecimal priceNet; int costCents; /* internal */ }
```

**Check:** Why not return `Product` directly? *(It may expose internal fields and ties the API to internals.)*

---

## JNR-013-L06 · Package by feature, layer within (7 min)
**Goal:** organize code by feature.

**Key points**
- Package by layer (`controllers/`, `services/`) scatters one feature across the project.
- Package by feature (`products/`, `orders/`) keeps related code together.
- Inside each feature: `ProductController`, `ProductService`, `ProductRepository`, DTOs.
- Features talk through services, not by reaching into each other's repositories.

**Show:** tree: `com.shop.api.products` with controller, service, repository, `dto` folder; sibling `orders`.

**Check:** Which makes a feature easier to find? *(Package by feature.)*

---

## JNR-013-L07 · Demo: building the products feature layer by layer (12 min)
**Goal:** build `GET /products` and `GET /products/{id}`; prepares JNR-013-LAB1.

**Steps**
1. Create the `Product` domain class and `ProductRepository` interface.
2. Implement `InMemoryProductRepository` with a `Map` and sample data.
3. Write `ProductService` with `list()` and `get(id)`.
4. **Planned mistake:** put the "not found" decision and a price calculation in the controller. Fix: move both into the service; the controller only delegates.
5. Write `ProductController`, run the app, and call both endpoints with `curl`.

---

## JNR-013-L08 · Demo: separating DTOs from domain models (12 min)
**Goal:** stop serializing domain objects; prepares JNR-013-LAB1.

**Steps**
1. Call the endpoint and see the raw `Product` JSON, including internal `costCents`.
2. Create `ProductResponse` with only public fields.
3. Add a mapper method `toResponse(Product)`.
4. **Planned mistake:** reuse one `ProductDto` for create, update, and response; clients can then send an `id` or change fields they should not. Fix: `CreateProductRequest`, `UpdateProductRequest`, `ProductResponse`.
5. Rename a domain field and show the API response does not change.
