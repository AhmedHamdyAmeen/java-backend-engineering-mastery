# JNR-P3 — REST API Engineering

**Phase goal:** the learner designs and implements HTTP APIs that are predictable, documented, and safe for clients to depend on.

**Running project:** *Shop API* gains the full catalog, cart, and file features over the in-memory repository from JNR-P2 (persistence follows in JNR-P4).

**Phase total:** ~7.7 h video · ~20 h practice

---

### JNR-017 · HTTP in depth
`n: 71` · **Video:** 65 min · **Practice:** 2 h

**Prerequisites:** BEG-052

**Learning outcomes** — the learner can:
1. Classify methods as safe and/or idempotent and explain why it matters for retries.
2. Use request and response headers for content negotiation (`Accept`, `Content-Type`).
3. Explain HTTP caching (`Cache-Control`, `ETag`, conditional requests) and when to disable it.
4. Explain HTTP versions and connection reuse at a conceptual level.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-017-L01 | Methods revisited: safety and idempotency | 12 |
| JNR-017-L02 | Headers that matter to backend engineers | 10 |
| JNR-017-L03 | Content negotiation | 8 |
| JNR-017-L04 | Caching and conditional requests | 15 |
| JNR-017-L05 | HTTP/1.1, HTTP/2, HTTP/3 in brief | 10 |
| JNR-017-L06 | Demo: conditional GET with ETags and curl | 10 |

**Lab** — `JNR-017-LAB1` *ETags:* add `ETag` support to `GET /products/{id}` and demonstrate a `304 Not Modified` with `curl`. Acceptance: second request returns 304 with no body.

**Common mistakes:** POST for everything; non-idempotent PUT; caching personalized responses.

**Assessment:** quiz plus lab.

**Career relevance:** retries and idempotency (MID-029, MID-033).

---

### JNR-018 · RESTful design
`n: 72` · **Video:** 60 min · **Practice:** 3 h

**Prerequisites:** BEG-053, JNR-017

**Learning outcomes** — the learner can:
1. Model resources, sub-resources, and collections from domain requirements.
2. Design URLs, methods, and status codes for create, read, update, delete, and actions that are not CRUD.
3. Define request/response contracts before writing code.
4. Critique an API design against REST conventions.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-018-L01 | Resources, not functions | 10 |
| JNR-018-L02 | URL design | 10 |
| JNR-018-L03 | Choosing status codes | 10 |
| JNR-018-L04 | Modeling actions (checkout, cancel) | 10 |
| JNR-018-L05 | Contract-first design | 10 |
| JNR-018-L06 | Demo: designing the Shop API contract on a whiteboard | 10 |

**Lab** — `JNR-018-LAB1` *Shop API design doc:* design endpoints for products, categories, cart, and orders as a table plus example requests/responses, then peer-review. Acceptance: design reviewed before any implementation.

**Common mistakes:** verbs in paths; 200 for creation; exposing database IDs and structure as the contract.

**Assessment:** design review using the DES rubric dimension.

**Career relevance:** API contracts (SRC-006) and API evolution (MID-062).

---

### JNR-019 · CRUD APIs
`n: 73` · **Video:** 84 min · **Practice:** 5 h

**Prerequisites:** JNR-013, JNR-018

**Learning outcomes** — the learner can:
1. Implement create, read, update (PUT and PATCH), and delete endpoints with correct status codes and `Location` headers.
2. Bind path variables, query parameters, and request bodies.
3. Implement pagination and sorting with limits on page size and allowed sort fields.
4. Return `201`, `204`, and `404` where appropriate.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-019-L01 | Create: POST, 201, Location | 10 |
| JNR-019-L02 | Read: single and collection | 8 |
| JNR-019-L03 | Update: PUT vs PATCH | 12 |
| JNR-019-L04 | Delete | 6 |
| JNR-019-L05 | Pagination | 12 |
| JNR-019-L06 | Sorting and its safety limits | 12 |
| JNR-019-L07 | Demo: full CRUD for categories, live | 12 |
| JNR-019-L08 | Demo: safe pagination and sorting | 12 |

**Lab** — `JNR-019-LAB1` *Catalog CRUD:* full product and category CRUD with paginated, sortable listing. Acceptance: matches the JNR-018 design; page size capped; controller tests cover every endpoint.

**Common mistakes:** unbounded list endpoints; PATCH that nulls missing fields; sorting by arbitrary user-supplied columns.

**Assessment:** implement an unseen resource from a spec.

**Career relevance:** the daily work of a junior backend engineer.

---

### JNR-020 · API design conventions
`n: 74` · **Video:** 55 min · **Practice:** 3 h

**Prerequisites:** JNR-019

**Learning outcomes** — the learner can:
1. Map between entities and DTOs with plain code or a mapper library, and justify the choice.
2. Apply consistent naming, date formats, money representation, and error shapes across endpoints.
3. Implement filtering with query parameters.
4. Compare API versioning strategies (URL, header, media type) and choose one.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-020-L01 | Consistency is a feature | 7 |
| JNR-020-L02 | DTO mapping approaches | 10 |
| JNR-020-L03 | Representing money, dates, and enums | 10 |
| JNR-020-L04 | Filtering | 8 |
| JNR-020-L05 | Versioning strategies | 10 |
| JNR-020-L06 | Demo: enforcing the Shop API style guide | 10 |

**Lab** — `JNR-020-LAB1` *Shop API style guide:* write a one-page style guide and bring all endpoints into compliance; add filtering by category and price range. Acceptance: no endpoint violates the guide.

**Common mistakes:** money as floating point; local time without offset; breaking changes without a version.

**Assessment:** review an inconsistent API against the style guide.

**Career relevance:** API governance (SRC-006, ARC-025).

---

### JNR-021 · OpenAPI
`n: 75` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** JNR-020

**Learning outcomes** — the learner can:
1. Read an OpenAPI document: paths, operations, schemas, responses.
2. Generate an OpenAPI document from Spring code and serve Swagger UI.
3. Enrich it with descriptions, examples, and error responses.
4. Explain code-first vs contract-first and the trade-offs.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-021-L01 | The OpenAPI specification | 10 |
| JNR-021-L02 | Generating docs from Spring (springdoc) | 10 |
| JNR-021-L03 | Examples and error responses | 10 |
| JNR-021-L04 | Code-first vs contract-first | 10 |
| JNR-021-L05 | Demo: from bare springdoc output to a usable API reference | 10 |

**Lab** — `JNR-021-LAB1` *Documented Shop API:* complete OpenAPI with examples and documented Problem Details; commit the generated spec. Acceptance: a new developer can call every endpoint using only Swagger UI.

**Common mistakes:** undocumented error responses; docs drifting from behavior.

**Assessment:** documentation review.

**Career relevance:** contract testing (MID-045) and API management (ARC-025).

---

### JNR-022 · API clients
`n: 76` · **Video:** 40 min · **Practice:** 1.5 h

**Prerequisites:** BEG-053, JNR-019

**Learning outcomes** — the learner can:
1. Organize Postman collections with environments and variables.
2. Chain requests (capture an ID or token from one response for the next).
3. Write `curl` commands for any endpoint, including headers and JSON bodies.
4. Call an external HTTP API from Spring with `RestClient`.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-022-L01 | Postman collections and environments | 8 |
| JNR-022-L02 | Scripts and chained requests | 8 |
| JNR-022-L03 | `curl` fluency | 6 |
| JNR-022-L04 | Calling other APIs from Spring | 8 |
| JNR-022-L05 | Demo: a chained Postman collection with environments | 10 |

**Lab** — `JNR-022-LAB1` *Shop collection:* a shared Postman collection with `local` and `deployed` environments; fetch exchange rates from an external API via `RestClient` with a timeout. Acceptance: collection runs end-to-end; timeout configured.

**Common mistakes:** hard-coded hosts and tokens in collections; HTTP clients without timeouts.

**Assessment:** lab check.

**Career relevance:** API testing (JNR-046) and resilience (MID-033).

---

### JNR-023 · File operations
`n: 77` · **Video:** 50 min · **Practice:** 2 h

**Prerequisites:** BEG-034, JNR-019

**Learning outcomes** — the learner can:
1. Accept multipart uploads and enforce size and content-type limits.
2. Stream downloads without loading whole files into memory.
3. Store uploaded files outside the application with generated names.
4. Explain upload-related risks (path traversal, oversized files, content sniffing).

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-023-L01 | Multipart uploads | 10 |
| JNR-023-L02 | Limits and validation | 8 |
| JNR-023-L03 | Streaming downloads | 10 |
| JNR-023-L04 | Where to store files | 7 |
| JNR-023-L05 | Upload security | 5 |
| JNR-023-L06 | Demo: product image upload and streaming download | 10 |

**Lab** — `JNR-023-LAB1` *Product images:* upload, list, and download product images with limits; filenames never taken from the client. Acceptance: path traversal attempt rejected; 20 MB file rejected.

**Common mistakes:** trusting the client's filename or content type; storing files inside the JAR's directory.

**Assessment:** lab plus security checklist.

**Career relevance:** object storage (MID-056, ARC-015).

---

### JNR-024 · API security fundamentals
`n: 78` · **Video:** 55 min · **Practice:** 1.5 h

**Prerequisites:** JNR-017

**Learning outcomes** — the learner can:
1. Distinguish authentication from authorization.
2. Compare session-based and token-based authentication.
3. Explain what HTTPS protects and why APIs must never run over plain HTTP in production.
4. Explain CORS and CSRF: what each protects against and when each applies.

**Lectures**
| ID | Title | Min |
| --- | --- | --- |
| JNR-024-L01 | Who are you vs what may you do | 8 |
| JNR-024-L02 | Sessions vs tokens | 10 |
| JNR-024-L03 | HTTPS for APIs | 7 |
| JNR-024-L04 | CORS demystified | 10 |
| JNR-024-L05 | CSRF and when it applies | 10 |
| JNR-024-L06 | Demo: watching CORS fail and fixing it | 10 |

**Lab** — `JNR-024-LAB1` *CORS experiment:* call the Shop API from a page on another origin, observe the browser error, then configure CORS for one allowed origin. Acceptance: only the allowed origin succeeds.

**Common mistakes:** `allowedOrigins("*")` with credentials; thinking CORS protects the server.

**Assessment:** quiz.

**Career relevance:** prepares JNR-P5.
