# JNR-017 · HTTP in depth — Lecture scripts

**Video:** 65 min · **Analogy used throughout:** the postal service: the method is the kind of request on the envelope, headers are the labels, and a tracking stamp (ETag) lets you ask "has the parcel changed?".
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-017-L01 · Methods revisited: safety and idempotency (12 min)
**Goal:** classify HTTP methods and explain why retries depend on it.

**Key points**
- **Safe** means the request does not change server state (reading only). `GET`, `HEAD`, `OPTIONS` are safe.
- **Idempotent** means doing it once or ten times leaves the server in the same state. `GET`, `PUT`, `DELETE` are idempotent.
- `POST` is neither safe nor idempotent: two identical calls can create two orders.
- `PATCH` is not guaranteed idempotent; it depends on what the patch says.
- Clients, proxies, and load balancers may retry idempotent calls automatically. A non-idempotent retry can duplicate work.

**Show**
| Method | Safe | Idempotent |
| --- | --- | --- |
| GET | yes | yes |
| PUT | no | yes |
| DELETE | no | yes |
| POST | no | no |

**Check:** Why is it fine to retry `PUT /products/5` after a timeout? *(Repeating it leaves the same final state.)*

---

## JNR-017-L02 · Headers that matter to backend engineers (10 min)
**Goal:** know the handful of headers you will use every week.

**Key points**
- Headers are `Name: value` pairs sent before the body, in both requests and responses.
- `Content-Type` says what the body is. `Content-Length` says how big it is.
- `Authorization` carries credentials. `Location` gives the URL of a created resource.
- `User-Agent` and `Host` identify the client and the target server.
- Header names are case-insensitive; never put secrets in URLs, use headers instead.

**Show**
```
POST /products HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Authorization: Bearer <token>

{"name":"Pen","priceCents":150}
```

**Check:** Which response header tells the client where the new resource lives? *(`Location`.)*

---

## JNR-017-L03 · Content negotiation (8 min)
**Goal:** let the client and server agree on a format.

**Key points**
- The client says what it can read with `Accept`. The server says what it sent with `Content-Type`.
- `Accept: application/json` asks for JSON. `Accept: application/xml` asks for XML.
- If the server cannot produce the requested type, it answers `406 Not Acceptable`.
- If the client sends a body type the server cannot read, the answer is `415 Unsupported Media Type`.
- In Spring, `produces` and `consumes` on a mapping declare what an endpoint supports.

**Show**
```java
@GetMapping(value = "/products/{id}", produces = "application/json")
Product get(@PathVariable long id) { ... }
```

**Check:** Which status does a client get when it posts XML to a JSON-only endpoint? *(`415`.)*

---

## JNR-017-L04 · Caching and conditional requests (15 min)
**Goal:** avoid sending data the client already has.

**Key points**
- `Cache-Control` tells caches how long to keep a response (`max-age=60`) or not to (`no-store`).
- An **ETag** is a version stamp for a response, for example a hash of the content.
- The client sends it back as `If-None-Match`. If nothing changed, the server answers `304 Not Modified` with no body.
- `Last-Modified` with `If-Modified-Since` does the same using a date.
- Never cache personalized or sensitive responses in shared caches: use `Cache-Control: private` or `no-store`.

**Show**
```
GET /products/5            ->  200, ETag: "v7", body
GET /products/5
If-None-Match: "v7"        ->  304, no body
```

**Check:** What does `304` save? *(The body transfer; the client reuses its copy.)*

---

## JNR-017-L05 · HTTP/1.1, HTTP/2, HTTP/3 in brief (10 min)
**Goal:** understand versions and connection reuse at a high level.

**Key points**
- HTTP/1.1 is text based. Connections are kept alive and reused, but requests on one connection wait in line.
- HTTP/2 is binary and multiplexes many requests over one connection, and compresses headers.
- HTTP/3 runs over QUIC (on UDP) and avoids one lost packet stalling everything.
- Your controller code does not change between versions; the server and client negotiate it.
- Opening a new connection is expensive (TCP and TLS handshakes), so reuse matters.

**Show:** a diagram of three requests: HTTP/1.1 queued on one connection, HTTP/2 interleaved on one connection.

**Check:** What problem does HTTP/2 multiplexing reduce? *(Requests waiting in line on one connection.)*

---

## JNR-017-L06 · Demo: conditional GET with ETags and curl (10 min)
**Goal:** watch a `304` happen. Prepares JNR-017-LAB1.

**Steps**
1. Run the Shop API and call `curl -i localhost:8080/products/1`. Note the status and any `ETag`.
2. Add an ETag to the response with `ResponseEntity.ok().eTag("\"v" + version + "\"")`.
3. Call again and copy the `ETag` value.
4. Send `curl -i -H 'If-None-Match: "v1"' localhost:8080/products/1` and show `304` with no body.
5. **Planned mistake:** send the ETag without the quotes. The server treats it as a different value and returns `200`. Fix: ETags are quoted strings; copy them exactly.
6. Update the product, repeat step 4, and show `200` with a new ETag.
