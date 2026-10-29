# JNR-020 · API design conventions — Exercises and lab

## Lab
### JNR-020-LAB1 · Shop API style guide
**Outcomes:** 1–4 · **Time:** ~3 h
Write a one-page style guide covering naming, money, dates, enums, error shape, paging, filtering, and versioning (with your chosen strategy and reason). Bring every endpoint into compliance, and add filtering by category and price range to the product list.

**Acceptance:** no endpoint violates the guide.

## Exercises (assessment: review an inconsistent API against the style guide)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-020-EX01 | 1 | Write a `from(...)` mapper for `Product` to `ProductResponse` that hides an internal field. |
| JNR-020-EX02 | 1 | In five sentences, justify plain mapping code or MapStruct for the Shop API. |
| JNR-020-EX03 | 2 | Rewrite a response using `price: 19.99`, `date: "03/04/26"`, `status: 2` in the style guide's formats. |
| JNR-020-EX04 | 2 | Given three endpoints with different error shapes, define one shared error shape and apply it. |
| JNR-020-EX05 | 3 | Implement `GET /products?category=&minPrice=&maxPrice=` with all filters optional, and test the combinations. |
| JNR-020-EX06 | 4 | Compare URL, header, and media-type versioning in a table and choose one for Shop API. |

## Solutions
- **EX01** `static ProductResponse from(Product p) { return new ProductResponse(p.getId(), p.getName(), p.getPriceCents()); }`
- **EX02** Sample: small model and few mappings favor plain code (explicit, no extra dependency); many similar mappings favor MapStruct (generated, compile-time checked). Any justified choice is correct.
- **EX03** `"priceCents": 1999`, `"date": "2026-04-03T00:00:00Z"`, `"status": "SHIPPED"`.
- **EX04** e.g. the Problem Details shape (`type`, `title`, `status`, `detail`); returned by one global handler.
- **EX05** Treat each null parameter as "no filter"; reject `minPrice > maxPrice` with `400`.
- **EX06** URL versioning is the usual choice for simplicity and visibility; header and media-type keep URLs clean but are harder to test. Justification matters.

**Outcome 2** (money, dates) is also checked by quiz Q05 to Q07.
