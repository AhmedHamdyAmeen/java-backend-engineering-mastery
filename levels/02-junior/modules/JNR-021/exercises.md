# JNR-021 · OpenAPI — Exercises and lab

## Lab
### JNR-021-LAB1 · Documented Shop API
**Outcomes:** 1–4 · **Time:** ~2 h
Add springdoc to Shop API and serve Swagger UI. Add descriptions and examples to every operation and DTO, and document the Problem Details error responses. Commit the generated spec file to the repository.

**Acceptance:** a new developer can call every endpoint using only Swagger UI.

## Exercises (assessment: documentation review)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-021-EX01 | 1 | Given a small OpenAPI YAML, list its paths, operations, schemas, and the response codes of one operation. |
| JNR-021-EX02 | 2 | Add springdoc to Shop API and open Swagger UI; find the raw JSON spec URL. |
| JNR-021-EX03 | 3 | Add summary, field descriptions, and a request example to `POST /products`. |
| JNR-021-EX04 | 3 | Document `400` and `404` responses on `GET /products/{id}` and `POST /products`. |
| JNR-021-EX05 | 4 | Compare code-first and contract-first for a partner-facing API and choose one with reasons. |
| JNR-021-EX06 | 1, 3 | Review a deliberately poor spec: find five problems (missing errors, no examples, wrong status, ...). |

## Solutions
- **EX01** Check that you listed the `paths` keys, each HTTP method under them, `components/schemas` names, and each `responses` key.
- **EX02** Usually `/swagger-ui.html` and `/v3/api-docs` (verify for the springdoc version used).
- **EX03** `@Operation(summary = "...")`, `@Schema(description = "...", example = "Pen")` on the record components.
- **EX04** `@ApiResponse(responseCode = "404", ...)` per operation, referencing the Problem Details schema.
- **EX05** Contract-first suits partner APIs: the design is reviewed and agreed before code; mention the sync risk and a check in CI.
- **EX06** Typical problems: missing error responses, no examples, wrong create status, missing descriptions, undocumented parameters.

**Outcome 4** is also checked by quiz Q09 and Q10; the lab criterion covers outcome 2 end to end.
