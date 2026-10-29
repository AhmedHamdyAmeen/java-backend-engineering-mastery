# JNR-018 · RESTful design — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a library: things (books, members) have addresses, and you use a few standard actions on them instead of inventing a new desk for every request.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-018-L01 · Resources, not functions (10 min)
**Goal:** think in nouns (things) rather than verbs (actions).

**Key points**
- A **resource** is a thing the API exposes: a product, a category, an order.
- A **collection** is a group of resources (`/products`). A **sub-resource** belongs to a parent (`/orders/7/items`).
- The HTTP method is the verb. The URL is the noun.
- Model from the domain requirements, not from database tables.
- The contract should not leak internal structure such as table names or database IDs by accident.

**Show**
| Bad (functions) | Good (resources) |
| --- | --- |
| `POST /createProduct` | `POST /products` |
| `GET /getOrderItems?id=7` | `GET /orders/7/items` |

**Check:** What is the verb in `DELETE /products/5`? *(`DELETE`, the method, not the path.)*

---

## JNR-018-L02 · URL design (10 min)
**Goal:** write URLs that are predictable.

**Key points**
- Use plural nouns for collections: `/products`, `/categories`.
- Identify one item by its ID: `/products/5`.
- Nest only one or two levels: `/categories/3/products` is fine; deeper is hard to use.
- Lowercase, hyphens for words (`/order-items`), no trailing slash, no file extensions.
- Filters, sorting, and paging go in the query string: `/products?category=3&sort=price`.

**Show**
```
GET    /products           list
POST   /products           create
GET    /products/5         read
PUT    /products/5         replace
DELETE /products/5         remove
```

**Check:** Where does `?page=2` belong? *(In the query string.)*

---

## JNR-018-L03 · Choosing status codes (10 min)
**Goal:** pick the status code that tells the client exactly what happened.

**Key points**
- `2xx` success: `200` OK, `201` Created, `204` No Content.
- `4xx` client mistake: `400` bad input, `401` not authenticated, `403` not allowed, `404` not found, `409` conflict, `422` valid shape but invalid meaning.
- `5xx` server fault: `500`, `503`.
- Creation returns `201`, not `200`. A successful delete with no body returns `204`.
- The status code is part of the contract; clients branch on it.

**Show**
| Situation | Code |
| --- | --- |
| Product created | 201 |
| Product not found | 404 |
| Duplicate SKU | 409 |
| Missing required field | 400 |

**Check:** Which code for "you are logged in but may not do this"? *(`403`.)*

---

## JNR-018-L04 · Modeling actions (checkout, cancel) (10 min)
**Goal:** model operations that are not plain CRUD.

**Key points**
- Prefer to model the result as a resource: `POST /orders` to check out a cart.
- Model state changes as a sub-resource or a state field: `POST /orders/7/cancellation`, or `PATCH /orders/7` with a new status.
- If it really is a command, a clear action sub-path is acceptable: `POST /orders/7/cancel`. Be consistent.
- Actions that change state use `POST` (or `PUT`/`PATCH`), never `GET`.
- Document which state transitions are allowed; an invalid one returns `409`.

**Show**
```
POST /carts/9/checkout   -> 201, Location: /orders/42
POST /orders/42/cancel   -> 200 (or 409 if already shipped)
```

**Check:** Why not `GET /orders/42/cancel`? *(`GET` must be safe; cancelling changes state.)*

---

## JNR-018-L05 · Contract-first design (10 min)
**Goal:** agree on the API shape before writing code.

**Key points**
- A **contract** lists URLs, methods, request and response bodies, and status codes.
- Write example requests and responses first; they are the cheapest way to find mistakes.
- Review the design with a peer or a client team before implementation.
- Changing a contract later costs more than changing a table on a whiteboard.
- The contract is not your entities: design DTOs for the client's needs.

**Show:** one table row plus examples
```
POST /products  body {"name","priceCents","categoryId"}
201 Location: /products/5  body {"id":5,"name":"Pen",...}
400 {"type":"...","title":"Invalid request"}
```

**Check:** What is reviewed before implementation? *(The contract: endpoints, bodies, status codes.)*

---

## JNR-018-L06 · Demo: designing the Shop API contract on a whiteboard (10 min)
**Goal:** design products, categories, cart, and orders together. Prepares JNR-018-LAB1.

**Steps**
1. List nouns from requirements: product, category, cart, cart item, order.
2. Draw collections and sub-resources, then write one URL per use case.
3. Fill a table: method, URL, success code, error codes.
4. **Planned mistake:** add `POST /addToCart` and `POST /placeOrder`. Fix: `POST /carts/{id}/items` and `POST /carts/{id}/checkout` (or `POST /orders`).
5. Write one example request and response per endpoint.
6. Peer-review with the checklist: nouns, plural, status codes, no leaked database structure.
