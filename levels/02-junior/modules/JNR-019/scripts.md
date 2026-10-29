# JNR-019 · CRUD APIs — Lecture scripts

**Video:** 84 min · **Analogy used throughout:** a filing cabinet: add a folder, read it, replace or amend its pages, remove it, and never hand over the whole cabinet at once (pagination).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-019-L01 · Create: POST, 201, Location (10 min)
**Goal:** implement creation the standard way.

**Key points**
- `POST /categories` with a JSON body creates a new item. The server picks the ID.
- Bind the body with `@RequestBody` into a request DTO (a plain record).
- Return `201 Created` and a `Location` header with the URL of the new item.
- Return the created representation in the body so the client sees the ID.
- Invalid input gives `400`; validation is covered in JNR-P2 and applied here.

**Show**
```java
@PostMapping
ResponseEntity<CategoryResponse> create(@RequestBody CreateCategoryRequest req) {
    CategoryResponse c = service.create(req);
    URI location = URI.create("/categories/" + c.id());
    return ResponseEntity.created(location).body(c);
}
```

**Check:** Which header holds the new item's URL? *(`Location`.)*

---

## JNR-019-L02 · Read: single and collection (8 min)
**Goal:** read one item or a list, with correct statuses.

**Key points**
- `GET /categories/{id}` binds the ID with `@PathVariable`.
- If the item does not exist, return `404`, not `200` with null.
- `GET /categories` returns a list. Query parameters are bound with `@RequestParam`.
- Use `defaultValue` for optional parameters so the code never sees surprises.
- Never return a raw entity; return a response DTO.

**Show**
```java
@GetMapping("/{id}")
CategoryResponse get(@PathVariable long id) {
    return service.find(id)
        .orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND));
}
```

**Check:** What status for a missing ID? *(`404`.)*

---

## JNR-019-L03 · Update: PUT vs PATCH (12 min)
**Goal:** choose and implement the right update style.

**Key points**
- `PUT /categories/5` **replaces** the whole item. The client sends every field.
- `PATCH /categories/5` changes **only** the fields sent.
- A `PUT` is idempotent. Return `200` with the body or `204` without.
- Danger: a PATCH that treats a missing field as `null` wipes data. Missing means "leave unchanged".
- Use optional fields in the patch DTO and apply only the ones present; verify the exact approach before recording.

**Show**
```java
if (req.name() != null) category.setName(req.name());
if (req.description() != null) category.setDescription(req.description());
```

**Check:** What should a PATCH do with a field the client did not send? *(Leave it unchanged.)*

---

## JNR-019-L04 · Delete (6 min)
**Goal:** remove an item with the right response.

**Key points**
- `DELETE /categories/5` removes the item.
- Success returns `204 No Content` with no body.
- Missing item: `404` is common; some teams return `204` to keep it idempotent. Choose one and document it.
- Deleting something other data depends on should return `409`, not break the data.
- Use `@ResponseStatus(HttpStatus.NO_CONTENT)` or `ResponseEntity.noContent()`.

**Show**
```java
@DeleteMapping("/{id}")
ResponseEntity<Void> delete(@PathVariable long id) {
    service.delete(id);
    return ResponseEntity.noContent().build();
}
```

**Check:** Does `204` carry a body? *(No.)*

---

## JNR-019-L05 · Pagination (12 min)
**Goal:** return lists in pages.

**Key points**
- An unbounded list grows until it breaks the server and the client.
- Use `page` (starting at 0 or 1; pick one) and `size` query parameters.
- Cap the size: if the client asks for 10,000, return at most your maximum (for example 100).
- Return the page items plus metadata: page, size, total elements, total pages.
- Spring Data offers `Pageable`; with the in-memory repository now, implement it by hand and swap later (JNR-P4).

**Show**
```java
int safeSize = Math.min(Math.max(size, 1), 100);
List<Product> slice = all.stream().skip((long) page * safeSize).limit(safeSize).toList();
```

**Check:** Why cap `size`? *(One request must not be able to load everything.)*

---

## JNR-019-L06 · Sorting and its safety limits (12 min)
**Goal:** allow sorting without opening a hole.

**Key points**
- Format: `?sort=price,desc`. Default to a stable sort such as `id`.
- Accept only an allow-list of fields: `name`, `price`, `createdAt`.
- Never put the user's text into a query or column name; with a database that is SQL injection.
- Unknown field gives `400` with a clear message.
- Always add a tie-breaker (`id`) so pages do not repeat or skip items.

**Show**
```java
private static final Set<String> SORTABLE = Set.of("name", "price", "createdAt");
if (!SORTABLE.contains(field)) throw new BadRequestException("Cannot sort by " + field);
```

**Check:** Why an allow-list? *(Users must not choose arbitrary fields or columns.)*

---

## JNR-019-L07 · Demo: full CRUD for categories, live (12 min)
**Goal:** build all five category operations end to end. Prepares JNR-019-LAB1.

**Steps**
1. Create `CategoryController` with a record DTO for create and update, using the in-memory repository.
2. Implement POST (`201` plus `Location`) and GET by ID and list.
3. Implement PUT and DELETE (`204`).
4. **Planned mistake:** the GET for an unknown ID returns `200` with an empty body. Fix: throw a not-found error so the client gets `404`.
5. Call every endpoint with `curl -i`, then add a `@WebMvcTest` for each.

---

## JNR-019-L08 · Demo: safe pagination and sorting (12 min)
**Goal:** add capped paging and allow-listed sorting to the product list. Prepares JNR-019-LAB1.

**Steps**
1. Add `page`, `size`, and `sort` parameters with defaults to `GET /products`.
2. Cap `size` at 100 and clamp `page` to 0 or more.
3. Add the sort allow-list with a tie-breaker on `id`.
4. **Planned mistake:** `?sort=password` (or any unknown field) is accepted and crashes. Fix: reject with `400`.
5. Return items plus page metadata and test with `size=1000` and a bad sort field.
