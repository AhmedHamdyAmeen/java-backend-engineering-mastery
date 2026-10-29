# JNR-018 · RESTful design — Quiz

Outcomes: O1 resources · O2 URLs, methods, status codes · O3 contract-first · O4 critique.

**Q01 (O1)** Which is a resource? A. `calculateTotal` B. `order` C. `POST` D. `404`
**Q02 (O1)** `/orders/7/items` is: A. A query B. A header C. A sub-resource collection D. A verb
**Q03 (O2)** Best URL to list products: A. `GET /getProducts` B. `POST /products/list` C. `GET /product/all.php` D. `GET /products`
**Q04 (O2)** Successful creation returns: A. 200 B. 201 C. 204 D. 302
**Q05 (O2)** Delete succeeded, no body to return: A. 204 B. 201 C. 400 D. 500
**Q06 (O2)** Cancelling an order that already shipped is best answered with: A. 201 B. 404 C. 409 D. 204
**Q07 (O2)** Which request should NOT use `GET`? A. Read a product B. List categories C. Search products D. Cancel an order
**Q08 (O3)** Contract-first means: A. Code first, docs later B. Agree URLs, bodies, and statuses before coding C. Generate everything from the database D. Skip reviews
**Q09 (O4)** What is wrong with `POST /products/5/delete`? A. Verb in path and wrong method for delete B. Nothing C. Plural noun D. It uses JSON
**Q10 (O4)** Exposing table names like `/tbl_products` is bad because: A. It is slower B. URLs must be uppercase C. It leaks internal structure into the contract D. HTTP forbids it

## Answers
Q01 B · Q02 C · Q03 D · Q04 B · Q05 A · Q06 C · Q07 D · Q08 B · Q09 A · Q10 C

## Practical part
Six exercises `JNR-018-EX01` to `EX06` plus the design doc. Pass: at least five exercises and a design doc that was reviewed (DES rubric: meets or exceeds on contract clarity and consistency) before implementation.
