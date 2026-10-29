# JNR-022 · API clients — Lecture scripts

**Video:** 40 min · **Analogy used throughout:** a phone with a contacts list: saved contacts (collections), a profile per place (environments), and one phone that can call anyone (curl and RestClient).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-022-L01 · Postman collections and environments (8 min)
**Goal:** organize requests so the whole team can reuse them.

**Key points**
- A **collection** is a saved, shareable group of requests, organized in folders (Products, Cart, Orders).
- An **environment** is a set of variables such as `baseUrl` and `token`. Switch between `local` and `deployed` with one click.
- Use `{{baseUrl}}/products` instead of hard-coding the host.
- Never commit real tokens or passwords in a shared collection; keep secrets in environment values that are not shared.
- Name requests clearly and add a one-line description.

**Show:** two environments: `local` with `baseUrl = http://localhost:8080` and `deployed` with the staging URL; the same request runs against both.

**Check:** Why `{{baseUrl}}`? *(One request works against many environments.)*

---

## JNR-022-L02 · Scripts and chained requests (8 min)
**Goal:** pass data from one response into the next request.

**Key points**
- A **post-response script** runs after a response arrives and can save values to variables.
- Typical chain: create a product, capture its ID, use `{{productId}}` in the next requests.
- The same works for tokens: log in, store the token, send it in `Authorization`.
- Add simple tests (status is `201`, body has `id`) so a run shows pass or fail.
- Run the whole collection in order with the collection runner.

**Show**
```javascript
const body = pm.response.json();
pm.environment.set("productId", body.id);
pm.test("created", () => pm.response.to.have.status(201));
```

**Check:** How does request 2 get the ID created by request 1? *(Request 1 stores it in a variable.)*

---

## JNR-022-L03 · `curl` fluency (6 min)
**Goal:** call any endpoint from the terminal.

**Key points**
- `curl -i URL` shows status and headers. `-X METHOD` sets the method.
- `-H 'Name: value'` adds a header. `-d '...'` sends a body.
- JSON needs `-H 'Content-Type: application/json'`.
- Quote carefully; on Windows PowerShell quoting differs (verify before recording).
- Use `-s` for quiet output and `-o file` to save the body.

**Show**
```bash
curl -i -X POST http://localhost:8080/products \
  -H 'Content-Type: application/json' \
  -d '{"name":"Pen","priceCents":150}'
```

**Check:** Which flag shows the status line and headers? *(`-i`.)*

---

## JNR-022-L04 · Calling other APIs from Spring (8 min)
**Goal:** call an external HTTP API from your service with `RestClient`.

**Key points**
- **`RestClient`** is Spring's modern synchronous HTTP client (Spring 6.1+; verify your version).
- Build it once as a bean with a base URL, and inject it where needed.
- Always set **timeouts** (connect and read); without them a slow partner can freeze your threads.
- Convert the JSON response into a record with `.body(MyRecord.class)`.
- Handle failures: the remote may return `4xx`, `5xx`, or time out; decide what your API returns then.

**Show**
```java
RestClient client = RestClient.builder().baseUrl("https://rates.example.com").build();
Rates r = client.get().uri("/latest?base=SAR").retrieve().body(Rates.class);
```

**Check:** Why configure timeouts? *(A slow remote must not block your service forever.)*

---

## JNR-022-L05 · Demo: a chained Postman collection with environments (10 min)
**Goal:** build a collection that runs end to end. Prepares JNR-022-LAB1.

**Steps**
1. Create the `Shop` collection with folders and the `local` and `deployed` environments.
2. Add create category, create product, get product, update, and delete requests using `{{baseUrl}}`.
3. Add post-response scripts that store `categoryId` and `productId`.
4. **Planned mistake:** the host is typed into every request. Fix: replace it with `{{baseUrl}}`; any shared token becomes an environment variable.
5. Run the collection with the runner and show all tests passing.
6. Export it and review the file for secrets before sharing.
