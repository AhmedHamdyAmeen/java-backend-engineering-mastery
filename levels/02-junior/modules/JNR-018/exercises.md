# JNR-018 · RESTful design — Exercises and lab

## Lab
### JNR-018-LAB1 · Shop API design doc
**Outcomes:** 1–4 · **Time:** ~3 h
Design endpoints for products, categories, cart, and orders. Produce a table (method, URL, success status, error statuses) plus an example request and response for each endpoint, including checkout and cancel. Then ask a peer to review it against a checklist (nouns, plural names, status codes, no leaked database structure) and record the changes.

**Acceptance:** the design is reviewed before any implementation starts.

## Exercises (assessment: design review using the DES rubric dimension)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-018-EX01 | 1 | From "a library lends books to members; members can reserve books", list resources, collections, and sub-resources. |
| JNR-018-EX02 | 2 | Rewrite these as REST: `POST /createUser`, `GET /getUser?id=3`, `POST /deleteUser`. |
| JNR-018-EX03 | 2 | Give the status code for: created, updated with body, deleted, not found, duplicate, invalid body. |
| JNR-018-EX04 | 2 | Design the endpoint to cancel an order, including the response when it is already shipped. |
| JNR-018-EX05 | 3 | Write a contract (request, response, errors) for `POST /products` before any code. |
| JNR-018-EX06 | 4 | Critique: `GET /products/delete/5`, `POST /products/5/get`, creation returning `200`, `/api/tbl_products`. List the problems. |

## Solutions
- **EX01** Resources: book, member, reservation. Collections: `/books`, `/members`, `/reservations`. Sub-resource: `/members/{id}/reservations`.
- **EX02** `POST /users`, `GET /users/3`, `DELETE /users/3`.
- **EX03** 201, 200, 204, 404, 409, 400.
- **EX04** `POST /orders/{id}/cancel` returns `200`; if shipped, `409` with an error body explaining the state.
- **EX05** Request `{"name","priceCents","categoryId"}`; `201` with `Location` and the created body; `400` for invalid fields; `404` or `422` for an unknown category (pick one and document it).
- **EX06** Verb in path, `GET` that deletes (unsafe), verb in path again, creation must be `201`, and the database table name leaks into the contract.

**Outcome 4** is also exercised during the peer review in the lab.
