# JNR-013 · Layered architecture — Quiz

Outcomes: O1 layer responsibilities · O2 DTOs vs domain · O3 package by feature · O4 minimal controller.

**Q01 (O1)** Where do business rules belong? A. Controller B. Repository C. Service D. DTO
**Q02 (O1)** What is a controller's job? A. Translate HTTP to a service call and back B. Run SQL C. Hold all business rules D. Store sessions
**Q03 (O1)** Which dependency direction is correct? A. Repository → controller B. Controller → service → repository C. Service → controller D. Repository → service
**Q04 (O1)** A service method returning `ResponseEntity` is: A. Best practice B. Required by Spring C. A layering mistake: it leaks HTTP into the service D. Faster
**Q05 (O2)** A DTO is: A. A database table B. The shape of data crossing the API boundary C. A Spring bean type D. A test double
**Q06 (O2)** Why not serialize domain objects directly? A. It is slower B. It exposes internals and ties the API to them C. Jackson cannot do it D. It is illegal
**Q07 (O2)** Using one DTO for create, update, and response is risky because: A. It saves time B. Clients may set fields they should not and shapes cannot evolve separately C. DTOs cannot be reused D. It breaks Maven
**Q08 (O3)** Package by feature means: A. `controllers/`, `services/` at the top B. A package per feature containing its layers C. One package for all D. Packages per developer
**Q09 (O3)** Another feature needs product data. Best: A. Use `ProductService` B. Use `ProductRepository` directly C. Copy the table D. Read the products' internals by reflection
**Q10 (O4)** A minimal REST controller: A. Contains the SQL B. Holds the discount rules C. Parses, delegates to a service, and returns the result D. Creates the repository with `new`

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 B · Q07 B · Q08 B · Q09 A · Q10 C

## Practical part
Seven exercises `JNR-013-EX01` to `EX07` plus the lab. The assessment: review a provided feature's layering (EX02 is the template). Pass: quiz at least 8/10, review finds at least four violations, lab acceptance met.
