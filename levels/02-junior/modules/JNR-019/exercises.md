# JNR-019 · CRUD APIs — Exercises and lab

## Lab
### JNR-019-LAB1 · Catalog CRUD
**Outcomes:** 1–4 · **Time:** ~5 h
Implement full product and category CRUD over the in-memory repository, following your JNR-018 design. The product list must be paginated and sortable with a maximum page size and an allow-list of sort fields. Write controller tests (`@WebMvcTest`) for every endpoint, including `404` and invalid-input cases.

**Acceptance:** matches the JNR-018 design; page size capped; controller tests cover every endpoint.

## Exercises (assessment: implement an unseen resource from a spec)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-019-EX01 | 1, 4 | Implement `POST /suppliers` returning `201` with a `Location` header. |
| JNR-019-EX02 | 2, 4 | Implement `GET /suppliers/{id}` (path variable) returning `404` when missing, and `GET /suppliers?country=` (query parameter). |
| JNR-019-EX03 | 1 | Implement `PUT /suppliers/{id}` (replace) and explain how it differs from PATCH. |
| JNR-019-EX04 | 1 | Implement `PATCH /suppliers/{id}` so omitted fields stay unchanged. |
| JNR-019-EX05 | 1, 4 | Implement `DELETE /suppliers/{id}` returning `204`, and decide what a missing ID returns. |
| JNR-019-EX06 | 3 | Add `page`, `size`, `sort` to `GET /suppliers` with max size 50 and allowed sort fields `name` and `country`. |

## Solutions
- **EX01** `ResponseEntity.created(URI.create("/suppliers/" + s.id())).body(s)`.
- **EX02** `@PathVariable long id`; throw `ResponseStatusException(NOT_FOUND)` when empty; `@RequestParam(required = false) String country`.
- **EX03** PUT requires all fields and replaces the item (idempotent); PATCH changes only supplied fields.
- **EX04** Patch DTO with nullable fields; set only those that are not null; test that an unsent field keeps its value.
- **EX05** `ResponseEntity.noContent().build()`; document `404` for missing (or `204`, but be consistent).
- **EX06** `size = Math.min(size, 50)`; `Set.of("name","country").contains(field)` else `400`; add `id` as tie-breaker.

**Outcome 2** is also covered by the lab (path, query, body binding in the catalog endpoints).
