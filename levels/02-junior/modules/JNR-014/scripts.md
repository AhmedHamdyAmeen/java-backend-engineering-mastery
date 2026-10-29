# JNR-014 · Validation — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a security desk at a building entrance that checks every visitor's pass before they go inside.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-014-L01 · Validating at the edge (8 min)
**Goal:** reject bad input before it reaches the service.

**Key points**
- Never trust input: clients, scripts, and attackers send anything.
- Validate at the controller boundary, on the request DTO.
- Jakarta Bean Validation: put constraint annotations on fields; add `@Valid` on the controller parameter.
- Frontend checks are for convenience only; the server must check again.

**Show**
```java
record CreateProductRequest(@NotBlank String name, @Positive BigDecimal price) {}

@PostMapping
ProductResponse create(@Valid @RequestBody CreateProductRequest req) { ... }
```

**Check:** Is frontend validation enough? *(No; anyone can call the API directly.)*

---

## JNR-014-L02 · Built-in constraints (10 min)
**Goal:** pick the right standard constraint.

**Key points**
- `@NotNull` (not null), `@NotBlank` (text with a visible character), `@NotEmpty` (not empty collection or text).
- `@Size(min, max)`, `@Min`, `@Max`, `@Positive`, `@PositiveOrZero`, `@DecimalMin`.
- `@Pattern(regexp=...)`, `@Email`, `@Past`, `@Future`.
- Constraints on nested objects and elements need `@Valid` on the field.
- Null is treated as valid by most constraints except `@NotNull`, `@NotBlank`, `@NotEmpty`.

**Show:** a table of the constraints with one example field each.

**Check:** Which for a required product name? *(`@NotBlank`.)*

---

## JNR-014-L03 · Custom constraints (10 min)
**Goal:** write a reusable constraint.

**Key points**
- Needs two parts: an annotation and a validator class.
- The annotation carries `message`, `groups`, `payload`, and `@Constraint(validatedBy = ...)`.
- The validator implements `ConstraintValidator<Annotation, Type>` with `isValid`.
- Keep it a pure check of the value; no database calls.

**Show**
```java
@Target(FIELD) @Retention(RUNTIME)
@Constraint(validatedBy = SkuValidator.class)
public @interface ValidSku {
    String message() default "invalid SKU";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}
```

**Check:** What are the two parts of a custom constraint? *(The annotation and the validator.)*

---

## JNR-014-L04 · Input validation vs business rules (7 min)
**Goal:** put each kind of rule in the right place.

**Key points**
- Input validation: shape and range of data, checkable from the request alone (not blank, positive, format).
- Business rules: depend on state or domain knowledge (stock is sufficient, SKU is unique, order is not shipped).
- Input rules go on the DTO at the edge; business rules go in the service or domain.
- Create and update often need different rules: use separate DTOs (or validation groups).

**Show:** table: "price > 0" input; "SKU not already used" business; "cannot cancel a shipped order" business.

**Check:** Where does "SKU must be unique" go? *(In the service: it needs stored data.)*

---

## JNR-014-L05 · Sanitization and why validation is not escaping (5 min)
**Goal:** know the limits of validation.

**Key points**
- Validation accepts or rejects; it does not make data safe for every use.
- Output must be escaped for where it lands (HTML, SQL, logs). SQL uses parameters, covered in JNR-P4 and JNR-041.
- Do not silently "clean" input in surprising ways; reject clearly.
- A whitelist (allowed characters) is safer than a blacklist.

**Show:** a name field containing `<script>`; validation may allow it; the output layer must still escape it.

**Check:** Does passing validation mean data is safe to put in HTML? *(No; escape on output.)*

---

## JNR-014-L06 · Demo: writing a custom `@ValidSku` constraint (10 min)
**Goal:** add `@ValidSku` to product creation; prepares JNR-014-LAB1.

**Steps**
1. Define the SKU format (for example three letters, a dash, four digits: `ABC-1234`).
2. Write the `@ValidSku` annotation and `SkuValidator`.
3. Put `@ValidSku` on `CreateProductRequest.sku`.
4. **Planned mistake:** forget `@Valid` on the controller parameter; a bad SKU gets through. Fix: add `@Valid`.
5. Post a bad SKU and see a 400; post a good one and see success.
