# BEG-053 · API fundamentals — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a restaurant menu and waiter: you order from the menu, you never walk into the kitchen.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-053-L01 · What an API is (8 min)
**Goal:** explain an API in plain words.

**Key points**
- API (application programming interface) is a defined way for one program to use another.
- The provider decides what you may ask for and how; the inside stays hidden.
- A web API is used over HTTP and usually answers in JSON.
- Mobile apps, websites, and other services all talk to APIs.

**Show:** a client app, an arrow labeled "HTTP + JSON", and a server with a database behind it.

**Check:** Does the client see the database? *(No, only the API.)*

---

## BEG-053-L02 · REST in plain language (10 min)
**Goal:** understand resources and URLs in a REST style.

**Key points**
- A resource is a thing: books, members, loans.
- Use nouns in URLs, in plural: `/books`, `/books/7`.
- The method is the verb: `GET /books`, `POST /books`, `DELETE /books/7`.
- Use status codes to report results: 200, 201, 404.
- Never put verbs in URLs, like `/getBooks`.

**Show:** table: `GET /books` list, `GET /books/7` one, `POST /books` create, `PUT /books/7` replace, `DELETE /books/7` remove.

**Check:** Fix `/deleteBook?id=7`. *(`DELETE /books/7`.)*

---

## BEG-053-L03 · Postman tour (10 min)
**Goal:** send requests from a friendly tool.

**Key points**
- Postman builds and sends HTTP requests and shows the response.
- Pick the method, type the URL, add params, headers, or a body.
- Save requests in a collection; export it as a file to share.
- Variables such as `{{baseUrl}}` avoid repeating the host.

**Show:** a Postman window with a `GET` request, the Params tab, and the response body.

**Check:** What is a collection for? *(Saving and sharing a set of requests.)*

---

## BEG-053-L04 · `curl` from the terminal (6 min)
**Goal:** send a request without a GUI.

**Key points**
- `curl URL` sends a `GET` and prints the body.
- `-X` sets the method, `-H` adds a header, `-d` sends a body.
- `-i` shows status and headers.
- Scripts and documentation often use `curl` examples.

**Show**
```bash
curl -i https://api.example.com/books/7
curl -X POST https://api.example.com/books \
  -H "Content-Type: application/json" \
  -d '{"title":"Dune"}'
```

**Check:** Which option adds a header? *(`-H`.)*

---

## BEG-053-L05 · Sketching endpoints for a resource (6 min)
**Goal:** design URL + method + status for one resource.

**Key points**
- List what clients need to do: list, read, create, update, delete.
- Map each to a method and URL.
- Choose success and failure statuses: 200, 201, 204, 400, 404.
- Filtering goes in query parameters: `/books?author=herbert`.

**Show**
```text
GET    /books        -> 200 list
GET    /books/{id}   -> 200 or 404
POST   /books        -> 201 or 400
DELETE /books/{id}   -> 204 or 404
```

**Check:** What status when a book is created? *(201.)*

---

## BEG-053-L06 · Demo: exploring a public API with Postman and curl (8 min)
**Goal:** call a real API. Prepares BEG-053-LAB1.

**Steps**
1. Pick a public API with documentation (verify it is still available before recording).
2. Read the docs; find the list endpoint.
3. Call it in Postman: list, then a single item, then a filtered query.
4. **Planned mistake:** use a wrong path; show the 404 and fix by rereading the docs.
5. Repeat one call with `curl -i`; save the Postman collection.
