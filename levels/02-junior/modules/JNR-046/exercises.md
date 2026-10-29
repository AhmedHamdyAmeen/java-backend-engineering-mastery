# JNR-046 · API testing — Exercises and lab

## Lab
### JNR-046-LAB1 · Checkout journey
**Outcomes:** 1–4 · **Time:** ~2.5 h
Automate register → login → add to cart → checkout → view order, plus the failure scenario for each step, with REST Assured against the running Shop.
**Acceptance:** matrix documented; all scenarios automated.

## Exercises (assessment: scenario matrix for an unseen endpoint)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-046-EX01 | 1 | Write a REST Assured test for `GET /api/products/{id}` checking status, content type, and two fields. |
| JNR-046-EX02 | 2 | For five checks (validation, mapping, full journey, security filter chain, DB constraint) choose MockMvc or full HTTP and justify. |
| JNR-046-EX03 | 3 | Write a scenario matrix for `POST /api/orders` with at least six rows. |
| JNR-046-EX04 | 3 | Automate the 401, 403, and 404 rows of that matrix. |
| JNR-046-EX05 | 4 | Assert the `Location` header and an error body (`code`, `message`) on a 400 response. |
| JNR-046-EX06 | 3 | Prove user A cannot read user B's order. |

## Solutions
- **EX01** `given().port(port).when().get("/api/products/1").then().statusCode(200).contentType(JSON).body("id", equalTo(1)).body("name", notNullValue());`
- **EX02** MockMvc: validation, mapping. Full HTTP: journey, security filter chain, DB constraint (needs the real stack).
- **EX03** Rows: valid 201; empty cart 400; no token 401; foreign cart 403; unknown product 404; out of stock 409.
- **EX04** Omit the header for 401; use a second user's token for 403; use a non-existent id for 404.
- **EX05** `.header("Location", containsString("/api/orders/"))`; error: `.body("code", equalTo("VALIDATION_ERROR")).body("message", not(emptyString()))`.
- **EX06** Create an order as A, request it with B's token, expect 403 (or 404 if the design hides existence).
- Outcome 2 is also covered by quiz Q01–Q02.
