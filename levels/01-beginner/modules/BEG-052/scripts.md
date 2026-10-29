# BEG-052 · Web fundamentals — Lecture scripts

**Video:** 58 min · **Analogy used throughout:** ordering at a restaurant: you send an order slip, the kitchen sends back a dish with a note.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-052-L01 · Anatomy of an HTTP request (10 min)
**Goal:** name the parts of a request and a response.

**Key points**
- HTTP is the language browsers and servers use; the client asks, the server answers.
- A request has a method, a URL, headers, and sometimes a body.
- A response has a status code, headers, and often a body.
- It is stateless: each request stands alone.

**Show**
```text
GET /books/7 HTTP/1.1
Host: api.example.com
Accept: application/json

HTTP/1.1 200 OK
Content-Type: application/json

{"id":7,"title":"Dune"}
```

**Check:** Which part tells you if it worked? *(The status code.)*

---

## BEG-052-L02 · Methods: GET, POST, PUT, PATCH, DELETE (10 min)
**Goal:** choose the right method.

**Key points**
- `GET` reads data; it must not change anything.
- `POST` creates something new.
- `PUT` replaces a whole resource; `PATCH` changes part of it.
- `DELETE` removes it.
- A GET that has side effects is a bug: crawlers and caches may call it.

**Show:** table: method / meaning / example (`DELETE /books/7`).

**Check:** Which method creates a new item? *(`POST`.)*

---

## BEG-052-L03 · Status codes (8 min)
**Goal:** read what the server says.

**Key points**
- 2xx success: 200 OK, 201 Created, 204 No Content.
- 3xx redirect: look elsewhere.
- 4xx client error: 400 bad request, 401 not logged in, 403 not allowed, 404 not found.
- 5xx server error: 500 internal error.
- Not every error is a 500; most mistakes by the caller are 4xx.

**Show:** a table of classes with one example each.

**Check:** A missing page returns which code? *(404.)*

---

## BEG-052-L04 · Headers (7 min)
**Goal:** know what headers are for.

**Key points**
- Headers are name-value metadata on requests and responses.
- `Content-Type` says the format of the body, e.g. `application/json`.
- `Accept` says which format the client wants.
- `Authorization` carries credentials; never share it.
- `Host`, `User-Agent`, and cache headers are common too.

**Show:** a request with `Content-Type` and `Accept`.

**Check:** Which header says the body is JSON? *(`Content-Type: application/json`.)*

---

## BEG-052-L05 · JSON (8 min)
**Goal:** read and write JSON and map it to Java.

**Key points**
- JSON is text for data: objects `{}`, arrays `[]`, strings, numbers, booleans, `null`.
- Keys are always in double quotes.
- An object maps to a Java class, an array to a `List`.
- No comments and no trailing commas.

**Show**
```json
{ "id": 7, "title": "Dune", "authors": ["Frank Herbert"], "available": true }
```
Java idea: `class Book { int id; String title; List<String> authors; boolean available; }`

**Check:** Which JSON type maps to a Java `List`? *(An array.)*

---

## BEG-052-L06 · URLs and query parameters (7 min)
**Goal:** pick a URL apart.

**Key points**
- Scheme, host, path, query, fragment: `https://shop.example.com/books/7?lang=en#reviews`.
- The path identifies the resource (`/books/7`).
- Query parameters after `?` filter or modify (`lang=en`, joined by `&`).
- The fragment after `#` is used by the browser and is not sent to the server.

**Show:** the URL above with each part colored.

**Check:** Is the fragment sent to the server? *(No.)*

---

## BEG-052-L07 · Demo: reading real HTTP traffic in the browser (8 min)
**Goal:** inspect real requests. Prepares BEG-052-LAB1.

**Steps**
1. Open a site, press F12, open the Network tab, and reload.
2. Click one request; show method, URL, status, and headers.
3. Filter by Fetch/XHR and open a JSON response in the Preview tab.
4. **Planned mistake:** read the first request only and miss the API call; fix by filtering for JSON.
5. Annotate one request in a table for the lab.
