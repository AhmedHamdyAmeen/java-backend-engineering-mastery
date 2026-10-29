# JNR-014 · Validation — Quiz

Outcomes: O1 constraints and `@Valid` · O2 custom constraints · O3 create vs update · O4 input vs business rules.

**Q01 (O1)** Which annotation on a controller parameter triggers validation? A. `@Validate` B. `@Check` C. `@Constraint` D. `@Valid`
**Q02 (O1)** Best constraint for a required, non-empty-looking name: A. `@NotNull` B. `@NotBlank` C. `@Size(max=0)` D. `@Past`
**Q03 (O1)** Frontend validation is: A. Enough on its own B. Not needed C. A convenience; the server must validate too D. Forbidden
**Q04 (O1)** `@Positive` on a price rejects: A. Zero and negatives B. Only negatives C. Only null D. Only decimals
**Q05 (O2)** A custom constraint needs: A. Only an annotation B. Only a validator C. An annotation and a `ConstraintValidator` D. A database table
**Q06 (O2)** The validator interface is: A. `Validator<T>` B. `ConstraintValidator<A,T>` C. `Checker` D. `Valid<T>`
**Q07 (O3)** A clean way to have different rules for create and update: A. Separate request DTOs B. Disable validation C. Validate in the frontend D. One DTO with no annotations
**Q08 (O4)** "SKU must not already exist" is: A. An input rule on the DTO B. A business rule needing stored data, checked in the service C. A UI rule D. A Java syntax rule
**Q09 (O4)** "Quantity must be greater than zero" is: A. A business rule B. A security rule C. An input rule suited to a constraint D. Not a rule
**Q10 (O4)** Passing validation means output is safe for HTML: A. Always B. Only for numbers and never for text C. Only in the frontend D. Not guaranteed; escape output for its context

## Answers
Q01 D · Q02 B · Q03 C · Q04 A · Q05 C · Q06 B · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Four exercises `JNR-014-EX01` to `EX04` plus the lab. Pass: quiz at least 8/10, all four exercises correct, lab acceptance met.
