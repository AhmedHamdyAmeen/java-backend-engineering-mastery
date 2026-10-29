# JNR-015 · Error handling — Exercises and lab

## Lab
### JNR-015-LAB1 · Consistent errors
**Outcomes:** 1–4 · **Time:** ~2 h
1. Create `ShopException` with `NotFoundException`, `ConflictException`, `BusinessRuleException`.
2. Write `@RestControllerAdvice` mapping: validation to 400 (with a `errors` list of field and message), not found to 404, conflict (duplicate SKU) to 409, anything else to 500.
3. Make all bodies `ProblemDetail`.
4. Log unexpected exceptions server-side; return a generic message.
5. Document the single error shape in the README.
**Acceptance:** every error matches one documented shape; no stack trace or internal message appears in any response.

## Exercises (assessment: error-contract review)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-015-EX01 | 1 | Draw the hierarchy for Shop: base, not found, conflict, business rule; state who throws each. |
| JNR-015-EX02 | 2 | Remove `try/catch` from a given controller and add the equivalent handler. |
| JNR-015-EX03 | 3 | Return a `ProblemDetail` for a 409 duplicate SKU, with a custom `sku` property. |
| JNR-015-EX04 | 4 | Review a response containing `org.postgresql... duplicate key` text; rewrite the handler. |
| JNR-015-EX05 | 3 | Review an error contract: a 200 with `"error": true`, three error shapes, one exposed stack trace; list fixes. |

## Solutions
- **EX01** `ShopException` (base) with `NotFoundException` (repositories/services), `ConflictException` (services on duplicates), `BusinessRuleException` (domain rules).
- **EX02** `@ExceptionHandler(NotFoundException.class)` returning `ProblemDetail.forStatusAndDetail(NOT_FOUND, ex.getMessage())`.
- **EX03** `var pd = ProblemDetail.forStatusAndDetail(CONFLICT, "SKU exists"); pd.setProperty("sku", sku); return pd;`
- **EX04** Log the original exception; return `ProblemDetail` 409 or 500 with a safe message.
- **EX05** Use proper status codes; one shape (`ProblemDetail`); hide traces and log them.
- Outcome 3 is also covered by the lab and quiz.
