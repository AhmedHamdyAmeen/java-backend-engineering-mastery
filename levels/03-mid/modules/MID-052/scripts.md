# MID-052 · Application threats — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** a bank vault review: walk the building, ask at each door "how could someone get in, and how would we notice?" Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-052-L01 · Threat modeling with STRIDE (12 min)
**Goal:** find threats systematically with a data-flow diagram.

**Key points**
- A data-flow diagram (DFD) shows actors, processes, data stores, data flows, and trust boundaries.
- STRIDE: Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege.
- Apply STRIDE to each element and each flow that crosses a trust boundary.
- Four questions: what are we building, what can go wrong, what do we do about it, did we do enough.
- Keep the model small and versioned in Git next to the code.

**Show:** DFD of Shop: browser → gateway → orders → PostgreSQL / Kafka; trust boundary at the gateway. Table: element, STRIDE letter, threat, mitigation.

**Check:** Which STRIDE letter is "a user denies placing an order"? *(Repudiation.)*

---

## MID-052-L02 · OWASP API Security Top 10 (14 min)
**Goal:** recognize the most common API weaknesses.

**Key points**
- BOLA (broken object-level authorization): `GET /orders/42` returns someone else's order. Check ownership on every object access.
- Broken authentication, and broken object *property*-level authorization (mass assignment, excessive data exposure).
- Broken function-level authorization: a normal user calls an admin endpoint.
- Unrestricted resource consumption: no rate, size, or pagination limits.
- Also: unrestricted access to sensitive business flows, SSRF, misconfiguration, poor API inventory, unsafe consumption of third-party APIs. Verify the current list edition before recording.

**Show**
```java
Order o = repo.findById(id).orElseThrow();
if (!o.customerId().equals(principal.customerId())) throw new NotFoundException();
```

**Check:** What is BOLA? *(Accessing another user's object by changing its ID because ownership is not checked.)*

---

## MID-052-L03 · Business-logic abuse (10 min)
**Goal:** see attacks that use the API exactly as designed.

**Key points**
- Credential stuffing: stolen passwords tried at scale. Defend with rate limits, MFA, breached-password checks.
- Scraping and bots: price scraping, inventory hoarding. Defend with rate limits, behavior signals, challenges.
- Promo and refund abuse: reusing codes, many accounts, race conditions on "one per customer".
- Controls: server-side limits per account/device/IP, atomic checks (unique constraint), monitoring of unusual patterns.
- No scanner finds these; only people who know the business do.

**Show:** abuse-case table for checkout: coupon reuse, cart hoarding, refund abuse, with a control for each.

**Check:** Why can scanners not find promo abuse? *(Each request is valid; the abuse lies in the business rules.)*

---

## MID-052-L04 · From threats to tests (8 min)
**Goal:** make every important threat a test or backlog item.

**Key points**
- Rank threats by impact and likelihood; handle the top ones first.
- Each mitigation gets a test: BOLA test, role test, rate-limit test.
- Unfixed threats become backlog items with an owner and a risk-acceptance note.
- Revisit the model when a new flow, service, or data store appears.

**Show:** `GET /orders/{id}` with customer B's token for customer A's order must return 404; the test runs in CI.

**Check:** Where should the BOLA test live? *(In the automated suite run by CI.)*

---

## MID-052-L05 · Demo: threat-modeling the checkout flow (12 min)
**Goal:** model checkout end to end and leave with tests and tickets. Prepares MID-052-LAB1.

**Steps**
1. Draw the DFD: browser, gateway, orders, payments (external), PostgreSQL, Kafka; mark trust boundaries.
2. Apply STRIDE to each flow; list threats in a table.
3. **Planned mistake:** list only technical threats (SQL injection, XSS). Fix: add business abuse cases (coupon reuse, price tampering in the request body, double charge by retry).
4. Rank the top five and write the mitigation for each.
5. Write one test per threat (price in body is ignored; coupon unique per customer) and file the rest as backlog items.

**Check:** Where should the price come from at checkout? *(The server's catalog, never the client request.)*
