# JNR-017 · HTTP in depth — Exercises and lab

## Lab
### JNR-017-LAB1 · ETags
**Outcomes:** 1–4 · **Time:** ~2 h
Add `ETag` support to `GET /products/{id}` in the Shop API. Derive the ETag from the product's content or version. Honor `If-None-Match` by returning `304 Not Modified` with no body. Show the full exchange with `curl -i`.

**Acceptance:** the second request (with `If-None-Match`) returns `304` with no body; after an update the ETag changes and the response is `200`.

## Exercises (assessment: quiz plus lab)
| ID | Outcome | Task |
| --- | --- | --- |
| JNR-017-EX01 | 1 | Classify GET, HEAD, POST, PUT, PATCH, DELETE as safe and/or idempotent in a table. |
| JNR-017-EX02 | 1 | A client retries `POST /orders` after a timeout. Describe what can go wrong and one way to prevent it. |
| JNR-017-EX03 | 2 | Make `GET /products/{id}` return JSON only and show the status for `Accept: application/xml`. |
| JNR-017-EX04 | 3 | Choose a `Cache-Control` value for: a public product image, a user's order list, a bank balance. Justify each. |
| JNR-017-EX05 | 3 | Using `curl -i`, record a 200 with ETag and then a 304 for the same URL. |
| JNR-017-EX06 | 4 | Write three sentences: what connection reuse is and what HTTP/2 adds over HTTP/1.1. |

## Solutions
- **EX01** Safe: GET, HEAD. Idempotent: GET, HEAD, PUT, DELETE. PATCH and POST are neither guaranteed.
- **EX02** The server may create two orders. Prevent with an idempotency key header that the server remembers (covered later in MID-029).
- **EX03** `@GetMapping(value = "/{id}", produces = MediaType.APPLICATION_JSON_VALUE)`; XML request gives `406`.
- **EX04** Image: `public, max-age=86400`. Order list: `private, no-cache` (or short `private` max-age). Balance: `no-store`.
- **EX05** `curl -i URL` then `curl -i -H 'If-None-Match: "<etag>"' URL`; second response has `304` and no body.
- **EX06** Connection reuse avoids repeated TCP/TLS setup; HTTP/2 multiplexes many requests on one connection and compresses headers.

**Outcome 2** (headers) is also checked by quiz Q04 and Q05; **outcome 4** by quiz Q09 and Q10.
