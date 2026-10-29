# JNR-040 · Role-based authorization — Quiz

Outcomes: O1 roles and method security · O2 ownership checks · O3 IDOR · O4 where authorization belongs.

**Q01 (O1)** In Spring, `hasRole("ADMIN")` matches the authority: A. `ADMIN` B. `ROLE_ADMIN` C. `admin_role` D. `ROLE:ADMIN`
**Q02 (O1)** `@PreAuthorize` needs: A. `@EnableMethodSecurity` B. `@EnableCaching` C. `@EnableAsync` D. Nothing
**Q03 (O1)** RBAC stands for: A. Remote bean access control B. Role-based access control C. Rapid backend API calls D. Read-only basic access control
**Q04 (O2)** The current user's id should come from: A. The request body B. A query parameter C. The authenticated principal D. A cookie the user edits
**Q05 (O2)** For another customer's order, return: A. 403 B. 404 C. 200 D. 500
**Q06 (O2)** The preferred ownership check is: A. Load all and filter in Java B. Put the owner in the query C. Check in JavaScript D. Skip it for admins and customers
**Q07 (O3)** IDOR means: A. Slow database queries B. Direct object access without an ownership check C. A hashing mode D. A token format
**Q08 (O3)** Using UUIDs instead of numbers: A. Fully fixes IDOR B. Makes ownership checks unnecessary C. Does not replace ownership checks D. Encrypts the data
**Q09 (O4)** "Only admins may list all orders" is best placed in: A. A database trigger B. Method security (or the URL rule) C. The browser D. A log
**Q10 (O4)** "A customer sees only their own orders" is best placed in: A. A domain query with the owner B. A CSS rule C. The README D. A cookie

## Answers
Q01 B · Q02 A · Q03 B · Q04 C · Q05 B · Q06 B · Q07 B · Q08 C · Q09 B · Q10 A

## Practical part
Seven exercises `JNR-040-EX01` to `EX07` plus the lab; finding IDOR bugs in the provided API (EX05) is the assessment. Pass: at least six exercises correct, all three IDOR bugs found, and the 404 test passing.
