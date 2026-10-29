# MID-035 · API gateways — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** the front desk of an office building: it checks your badge and points you to the right floor, but it does not do anyone's work for them.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-035-L01 · Why a gateway (8 min)
**Goal:** list what a gateway does for a set of services.

**Key points**
- A **gateway** is the single public entry point in front of services.
- Routing: `/api/orders/**` goes to `orders`, `/api/products/**` to `catalog`.
- Cross-cutting edge concerns in one place: TLS termination, authentication, rate limiting, CORS, request logging, correlation ids.
- Hides internal topology: clients do not know service names or ports.
- Cost: an extra hop, an extra thing to scale and keep highly available.

**Show:** diagram: browser → gateway → `catalog`, `orders`, `inventory`, `payments` on a private network.

**Check:** Name two concerns a gateway centralizes. *(For example TLS termination and rate limiting.)*

---

## MID-035-L02 · Routing and filters (10 min)
**Goal:** configure Spring Cloud Gateway routes and filters.

**Key points**
- A **route** has an id, a destination URI, **predicates** (match path, method, header) and **filters** (change the request or response).
- Common filters: strip a path prefix, add headers, rewrite paths, rate limit, retry.
- Destination URIs use service names from DNS (`http://orders:8080`), not hard-coded IPs.
- Gateway is reactive (WebFlux); never block in a filter.
- Verify the starter name and property keys for your Spring Cloud version before recording.

**Show**
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: orders
          uri: http://orders:8080
          predicates: [ Path=/api/orders/** ]
          filters: [ StripPrefix=1 ]
```

**Check:** What does a predicate do? *(Decides whether a request matches the route.)*

---

## MID-035-L03 · Authentication at the edge (10 min)
**Goal:** validate tokens at the gateway without making services blindly trust callers.

**Key points**
- The gateway can validate the JWT (signature, expiry, issuer) and reject bad requests early.
- It forwards identity to services (the token itself, or trusted headers).
- Services must still check authorization for their own data and must not accept unauthenticated requests just because they are "internal".
- Network isolation: only the gateway is exposed; services listen on a private network.
- Use the token's audience and scopes; do not trust identity headers that clients could set (strip them at the edge).

**Show**
```java
http.oauth2ResourceServer(o -> o.jwt(Customizer.withDefaults()))
    .authorizeExchange(a -> a.pathMatchers("/api/products/**").permitAll()
                              .anyExchange().authenticated());
```

**Check:** Why must services still validate identity? *(A gateway bypass or misroute would otherwise expose them; defense in depth.)*

---

## MID-035-L04 · What not to put in a gateway (8 min)
**Goal:** keep the gateway thin.

**Key points**
- No business rules (pricing, discounts, order validation); they belong in services.
- No data aggregation that grows into a service of its own (see BFF).
- No shared database access, and no per-service special cases that need constant redeploys.
- Keep it stateless and fast; every request pays its cost.
- A gateway that every team must change for each feature becomes a new monolith and a bottleneck.

**Show**
| Concern | Gateway | Service |
| --- | --- | --- |
| TLS, CORS, token validation | yes | no |
| Rate limits, correlation id | yes | no |
| Price calculation | no | yes |
| Order ownership check | no | yes |

**Check:** Where does "customer may only see their own orders" belong? *(In the `orders` service.)*

---

## MID-035-L05 · Backend for frontend (8 min)
**Goal:** explain BFF and when to use it.

**Key points**
- A **backend for frontend (BFF)** is an API tailored to one client type (web, mobile, partner).
- It aggregates and reshapes data so each client makes fewer calls and gets the right payload.
- Each BFF is owned by the team of its client, so it can change with the UI.
- It is not the generic gateway: the gateway handles edge concerns; the BFF handles presentation needs.
- Avoid duplicating business logic across BFFs; call services for it.

**Show:** diagram: web app → web BFF, mobile app → mobile BFF, both behind the gateway, both calling the services.

**Check:** What problem does a BFF solve? *(Different clients need different shapes of data without bloating one generic API.)*

---

## MID-035-L06 · Demo: one entry point for four services (12 min)
**Goal:** put Shop behind one gateway. Prepares MID-035-LAB1.

**Steps**
1. Add a `gateway` service to Compose with routes for `catalog`, `orders`, `inventory`, and `payments`.
2. Call `GET localhost:8080/api/products` and see it routed to `catalog`; show the headers added.
3. Add JWT validation; call `orders` without a token and get `401`.
4. Add the rate-limit filter from MID-034.
5. **Planned mistake:** leave the services' ports published in Compose. Call `localhost:8083` directly and bypass the gateway. Fix: remove published ports so only the gateway is reachable, and make services validate tokens too.
6. Verify the correlation id header flows to all services.
