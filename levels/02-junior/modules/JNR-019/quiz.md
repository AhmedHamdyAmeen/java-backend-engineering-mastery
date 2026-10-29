# JNR-019 · CRUD APIs — Quiz

Outcomes: O1 create, read, update, delete · O2 binding · O3 pagination and sorting · O4 status codes.

**Q01 (O1)** After a successful create, the `Location` header holds: A. The new item's URL B. The server's IP C. The user's name D. The page number
**Q02 (O1)** `PUT` differs from `PATCH` because `PUT`: A. Only reads B. Replaces the whole item C. Deletes the item D. Needs no body
**Q03 (O1)** A PATCH body has only `name`. The `description` should: A. Become null B. Cause an error C. Stay unchanged D. Be deleted from the API
**Q04 (O2)** Which annotation binds `{id}` in the path? A. `@RequestBody` B. `@RequestParam` C. `@Autowired` D. `@PathVariable`
**Q05 (O2)** Which binds the JSON body? A. `@RequestBody` B. `@PathVariable` C. `@Value` D. `@Bean`
**Q06 (O3)** Why cap the page size? A. To change the URL B. To stop one request loading everything C. To enable caching D. To sort faster
**Q07 (O3)** Sorting should accept: A. Any text from the client B. Only an allow-list of fields C. SQL fragments D. Nothing, ever
**Q08 (O3)** A tie-breaker such as `id` in sorting is used to: A. Hide data B. Encrypt pages C. Keep page order stable D. Delete duplicates
**Q09 (O4)** A successful delete with no body returns: A. 200 B. 201 C. 204 D. 404
**Q10 (O4)** `GET /categories/999` where none exists returns: A. 404 B. 201 C. 204 D. 200 with null

## Answers
Q01 A · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 B · Q08 C · Q09 C · Q10 A

## Practical part
Six exercises `JNR-019-EX01` to `EX06` on an unseen resource plus the catalog lab. Pass: at least five exercises and a lab with capped paging and tests for every endpoint.
