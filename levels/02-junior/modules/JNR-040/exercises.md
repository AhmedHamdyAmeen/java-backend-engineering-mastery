# JNR-040 · Role-based authorization — Exercises and lab

## Lab
### JNR-040-LAB1 · My orders only
**Outcomes:** 1–4 · **Time:** ~2.5 h
Customers see only their own carts and orders; admins see all.
**Acceptance:** a test where customer A requests customer B's order receives 404 (no existence leak).

## Exercises (assessment: find IDOR bugs in a provided API)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-040-EX01 | 1 | Define roles and authorities for Shop (customer, admin) and map five endpoints to them. |
| JNR-040-EX02 | 1 | Protect `OrderService.listAll()` with `@PreAuthorize` and say what else must be enabled. |
| JNR-040-EX03 | 2 | Rewrite `findById(id)` so it only returns the caller's order. |
| JNR-040-EX04 | 2 | A create-order request body contains `customerId`. Explain the risk and fix it. |
| JNR-040-EX05 | 3 | In a provided API, find three IDOR bugs (read, update, delete) and write the attack request for each. |
| JNR-040-EX06 | 3 | Write a MockMvc test where customer A requests customer B's order. |
| JNR-040-EX07 | 4 | For each rule, pick filter, method, or query: "must be logged in"; "only admins list all orders"; "only own orders". |

## Solutions
- **EX01** For example: `GET /api/products` public; `POST /api/products` ADMIN; `GET /api/orders/{id}` CUSTOMER with ownership; `GET /api/orders` ADMIN; `POST /api/orders` CUSTOMER.
- **EX02** `@PreAuthorize("hasRole('ADMIN')")` and `@EnableMethodSecurity` on a configuration class.
- **EX03** `findByIdAndCustomerId(id, currentUserId)`; empty result leads to 404.
- **EX04** A customer could place orders as someone else; take the customer from the authenticated principal and delete the field from the request.
- **EX05** Change the ID in `GET`, `PUT`, and `DELETE` requests while logged in as another customer; each returns the other's data or modifies it.
- **EX06** Log in as A, request B's order id, `status().isNotFound()`.
- **EX07** Must be logged in: filter (URL rule); only admins list all: method security; only own orders: domain query.
