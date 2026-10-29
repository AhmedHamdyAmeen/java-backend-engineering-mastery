# JNR-020 · API design conventions — Lecture scripts

**Video:** 55 min · **Analogy used throughout:** road signs: every sign in a country uses the same shapes and colors, so drivers never have to guess.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-020-L01 · Consistency is a feature (7 min)
**Goal:** see why every endpoint should look and behave alike.

**Key points**
- A client developer learns one endpoint and expects the rest to work the same way.
- Decide once: field naming (`camelCase` or `snake_case`), plural paths, error shape, page shape.
- Write the decisions in a short **style guide** and check new endpoints against it.
- Inconsistency costs time in every client, forever.
- Consistency matters more than which choice you made.

**Show:** two endpoints side by side: one returns `created_at`, the other `createdAt`; one returns `{"error":"x"}`, the other a plain string. Mark each mismatch.

**Check:** What is the style guide for? *(One set of decisions applied to every endpoint.)*

---

## JNR-020-L02 · DTO mapping approaches (10 min)
**Goal:** convert between entities and DTOs and choose how.

**Key points**
- A **DTO** (data transfer object) is the shape sent over the API. An **entity** is the internal model.
- Keeping them separate lets you change one without breaking the other and hides internal fields.
- **Plain code:** a `toResponse()` method or a static mapper. Simple, explicit, easy to debug.
- **Mapper library** (for example MapStruct): generates mapping code from interfaces; less typing for large models, with a learning cost.
- For small models prefer plain code; for many similar mappings a library pays off. Be ready to justify.

**Show**
```java
record ProductResponse(long id, String name, long priceCents) {
    static ProductResponse from(Product p) {
        return new ProductResponse(p.getId(), p.getName(), p.getPriceCents());
    }
}
```

**Check:** Why not return the entity directly? *(It exposes internal fields and ties the API to the model.)*

---

## JNR-020-L03 · Representing money, dates, and enums (10 min)
**Goal:** pick formats that never lose information.

**Key points**
- **Money:** never `double` or `float` (rounding errors). Use integer minor units (`priceCents`) or a decimal string, plus a currency code.
- **Dates and times:** ISO 8601 with an offset or UTC, for example `2026-03-01T10:15:30Z`. A time without an offset is ambiguous.
- **Enums:** send stable uppercase strings (`"SHIPPED"`), not ordinal numbers; document the allowed values.
- Use the same formats in requests and responses.
- Unknown enum values from the client should give `400`.

**Show**
```json
{ "total": { "amount": 1999, "currency": "SAR" },
  "createdAt": "2026-03-01T10:15:30Z",
  "status": "SHIPPED" }
```

**Check:** Why not `0.1 + 0.2` for money? *(Floating point cannot represent it exactly.)*

---

## JNR-020-L04 · Filtering (8 min)
**Goal:** let clients narrow a list with query parameters.

**Key points**
- Each filter is a named query parameter: `GET /products?category=3&minPrice=500&maxPrice=2000`.
- All filters are optional; no filter means no restriction.
- Combine filters with AND. Validate values (`minPrice` not greater than `maxPrice`).
- Filtering works together with paging and sorting.
- Allow only filters you documented; ignore or reject unknown ones consistently.

**Show**
```java
@GetMapping
Page<ProductResponse> list(@RequestParam(required = false) Long category,
                           @RequestParam(required = false) Long minPrice,
                           @RequestParam(required = false) Long maxPrice, ...)
```

**Check:** What does a missing `category` parameter mean? *(Do not filter by category.)*

---

## JNR-020-L05 · Versioning strategies (10 min)
**Goal:** compare ways to evolve an API without breaking clients.

**Key points**
- A **breaking change** (removing or renaming a field, changing meaning) breaks existing clients.
- **URL versioning:** `/v1/products`. Visible and simple; the most common.
- **Header versioning:** a custom header such as `X-API-Version: 2`. Clean URLs, but harder to test in a browser.
- **Media-type versioning:** `Accept: application/vnd.shop.v2+json`. Precise, but more complex.
- Adding optional fields is not breaking. Choose one strategy and use it everywhere.

**Show**
| Strategy | Example | Trade-off |
| --- | --- | --- |
| URL | `/v2/products` | Simple, visible |
| Header | `X-API-Version: 2` | Clean URLs |
| Media type | `Accept: ...v2+json` | Precise, complex |

**Check:** Is adding an optional response field a breaking change? *(No.)*

---

## JNR-020-L06 · Demo: enforcing the Shop API style guide (10 min)
**Goal:** write the guide and bring the API into line. Prepares JNR-020-LAB1.

**Steps**
1. Write a one-page style guide: naming, money, dates, enums, errors, paging, filtering, versioning.
2. Audit all endpoints in a table: rule, endpoint, pass or fail.
3. Fix the failures: rename fields, switch prices to cents, use ISO dates.
4. **Planned mistake:** a price returned as `19.99` (double). Fix: `priceCents: 1999`, then update tests.
5. Add `category`, `minPrice`, and `maxPrice` filters to `GET /products` and test them.
