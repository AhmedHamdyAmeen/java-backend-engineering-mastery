# JNR-013 · Layered architecture — Exercises and lab

## Lab
### JNR-013-LAB1 · Products feature
**Outcomes:** 1–4 · **Time:** ~4 h
1. In package `com.shop.api.products`, create `Product`, `ProductRepository`, `InMemoryProductRepository`, `ProductService`, `ProductController`.
2. Implement `GET /products` and `GET /products/{id}`.
3. Return `ProductResponse` DTOs through a mapper; never the domain class.
4. Throw a not-found exception from the service for an unknown id (the HTTP mapping comes in JNR-015).
**Acceptance:** the controller contains no business logic; domain objects are never serialized directly; the service has no HTTP types.

## Exercises (assessment: layering review of a provided feature)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-013-EX01 | 1 | Sort these into layers: parse JSON, check stock, find by id, set HTTP 404, compute total with tax. |
| JNR-013-EX02 | 1 | Review a provided "fat controller" and list five violations. |
| JNR-013-EX03 | 2 | Write `OrderResponse` and a mapper from `Order` that hides `internalNotes`. |
| JNR-013-EX04 | 2 | Explain what breaks for clients if you rename a field of a serialized domain class. |
| JNR-013-EX05 | 3 | Reorganize a package-by-layer tree into package-by-feature. |
| JNR-013-EX06 | 4 | Write a `@RestController` with `GET /customers/{id}` that only delegates to a service. |
| JNR-013-EX07 | 3 | Decide: may `orders` use `ProductRepository` directly? Justify and write the alternative. |

## Solutions
- **EX01** Controller: parse JSON, set HTTP 404. Service: check stock, compute total with tax. Repository: find by id.
- **EX02** Typical violations: repository calls in the controller, business rules in it, a returned entity, `try/catch` and status logic, one DTO for everything.
- **EX03** `record OrderResponse(long id, List<ItemResponse> items, BigDecimal total){}` and `static OrderResponse toResponse(Order o)`.
- **EX04** The JSON field name changes, so clients break; a DTO decouples this.
- **EX05** `products/{ProductController, ProductService, ProductRepository, dto/}` and the same for `orders`.
- **EX06** `@RestController @RequestMapping("/customers") class CustomerController { ... @GetMapping("/{id}") CustomerResponse get(@PathVariable long id){ return service.get(id);} }`
- **EX07** No: use `ProductService` (or a narrow interface) so the products feature controls its own data and rules.
