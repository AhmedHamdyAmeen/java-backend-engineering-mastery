# JNR-046 · API testing — Lecture scripts

**Video:** 50 min · **Analogy used throughout:** a mystery shopper who walks through the front door of the shop and checks every step.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## JNR-046-L01 · MockMvc vs real HTTP (8 min)
**Goal:** choose the right kind of API test.

**Key points**
- MockMvc (`@WebMvcTest`) tests the web layer without a real server: fast, services mocked.
- Real HTTP tests (`@SpringBootTest` with a random port) test the whole stack, including security, serialization, and the database.
- Use MockMvc for controller rules (validation, status codes, mapping); use real HTTP for journeys.
- Mix both; most endpoint rules in MockMvc, a few journeys in full tests.
- Both can use Testcontainers if the database is involved.

**Show:** a table: speed, what is real, what is mocked, best for.

**Check:** Which is faster, MockMvc or a full HTTP test? *(MockMvc.)*

---

## JNR-046-L02 · REST Assured (12 min)
**Goal:** write readable HTTP tests.

**Key points**
- REST Assured uses `given / when / then` to send requests and check responses. Verify the current version before recording.
- Set the port from `@LocalServerPort`.
- Check status, headers, and body fields with JSON paths: `body("items.size()", is(2))`.
- `extract().path(...)` pulls a value for the next step (for example a token or id).
- Check body fields that matter, not the whole JSON string.

**Show**
```java
given().port(port).contentType(JSON).body(newOrder)
.when().post("/api/orders")
.then().statusCode(201)
    .header("Location", containsString("/api/orders/"))
    .body("status", equalTo("NEW"));
```

**Check:** Why not compare the entire JSON string? *(It breaks on harmless changes such as field order or new fields.)*

---

## JNR-046-L03 · A scenario matrix for every endpoint (10 min)
**Goal:** list the cases an endpoint needs before writing tests.

**Key points**
- For each endpoint list: success, validation failure, unauthenticated (401), unauthorized (403), not found (404), conflict or business-rule failure.
- Write the matrix as a table first; each row becomes a test.
- Check the error body shape too, not just the status code.
- Add boundary data: empty, too long, negative, duplicate.
- Keep the matrix in the repository next to the tests.

**Show:** a matrix for `POST /api/orders`: valid (201), empty cart (400), no token (401), other user's cart (403), unknown product (404), out of stock (409).

**Check:** Which two status codes separate "not logged in" from "not allowed"? *(401 and 403.)*

---

## JNR-046-L04 · Testing secured endpoints (10 min)
**Goal:** test authentication and authorization.

**Key points**
- Get a real token by logging in during the test (or from a test Keycloak) and send it in the `Authorization` header.
- With MockMvc you can use `@WithMockUser` or JWT post-processors from Spring Security Test.
- Test each role: allowed, forbidden, and anonymous.
- Test that a user cannot read another user's data.
- Never put real credentials in test code; use test users.

**Show**
```java
given().port(port).header("Authorization", "Bearer " + token)
.when().get("/api/orders/" + otherUsersOrderId)
.then().statusCode(403);
```

**Check:** A logged-in user opens an admin endpoint. Which status? *(403.)*

---

## JNR-046-L05 · Demo: the checkout journey with REST Assured (10 min)
**Goal:** automate register, login, cart, checkout, and view order. Prepares `JNR-046-LAB1`.

**Steps**
1. Write the scenario matrix for the five steps.
2. Register and log in; extract the token.
3. Add a product to the cart, checkout, and assert the order body and `Location` header.
4. Add failure rows: empty cart, no token, unknown product.
5. **Planned mistake:** assert the whole JSON as a string; add a field and watch the test break; fix with field-level assertions.
6. Run the test against the Testcontainers-backed app.
