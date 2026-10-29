# JNR-014 · Validation — Exercises and lab

## Lab
### JNR-014-LAB1 · Validated product creation
**Outcomes:** 1–4 · **Time:** ~2 h
1. Add `POST /products` with `CreateProductRequest` (name, sku, price, optional description).
2. Add constraints: name not blank and sized, price positive, description size-limited.
3. Write `@ValidSku` with its validator and apply it.
4. Use a separate `UpdateProductRequest` for update rules.
5. Keep "SKU must be unique" as a service check, not an annotation.
**Acceptance:** invalid requests never reach the service (shown by a service call count or log); business rule lives in the service.

## Exercises (assessment: 4 exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-014-EX01 | 1 | Write a `CreateCustomerRequest` with name, email, age (18+) constraints and `@Valid` on the controller. |
| JNR-014-EX02 | 2 | Write `@ValidCountryCode` (two uppercase letters) with a validator. |
| JNR-014-EX03 | 3 | Design `CreateProductRequest` and `UpdateProductRequest` so create requires all fields and update allows a partial set; explain the choice versus groups. |
| JNR-014-EX04 | 4 | Classify each rule as input or business: quantity > 0, stock available, email format, coupon not expired. |

## Solutions
- **EX01** `record CreateCustomerRequest(@NotBlank String name, @Email @NotBlank String email, @Min(18) int age){}` and `create(@Valid @RequestBody ...)`.
- **EX02** Annotation with `@Constraint(validatedBy=...)`; validator: `value == null || value.matches("[A-Z]{2}")`.
- **EX03** Separate DTOs are clearer and easier to read than groups; groups work when you must share one type (`@NotNull(groups=Create.class)`).
- **EX04** Input: quantity > 0, email format. Business: stock available, coupon not expired.
- Outcome 1 is also covered by the lab and quiz; all four outcomes are covered by EX01-EX04.
