# MID-035 · API gateways — Exercises and lab

## Lab
### MID-035-LAB1 · Shop gateway
**Outcomes:** 1–4 · **Time:** ~2.5 h
Build a Spring Cloud Gateway (or an equivalent) as the single public entry point for `catalog`, `orders`, `inventory`, and `payments`. Validate JWTs at the edge, route by path, add a correlation id, and apply rate limits (MID-034). Remove published ports from the services so they are reachable only through the gateway on the Compose network, and keep token validation in services.

**Acceptance:** services are not reachable directly from outside; requests without a valid token get `401` at the gateway; a request with a forged identity header does not gain access.

## Exercises (assessment: responsibility-placement exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-035-EX01 | 1 | List five responsibilities of an API gateway with one sentence each. |
| MID-035-EX02 | 2 | Write the route configuration for `catalog` and `orders` with path predicates and prefix stripping. |
| MID-035-EX03 | 2 | Configure JWT validation so `/api/products/**` is public and everything else needs a token. |
| MID-035-EX04 | 3 | Responsibility placement: for 10 concerns (TLS, CORS, discount calculation, order ownership, rate limit, JWT signature check, response aggregation, request logging, retry of payment, feature flags per customer), decide gateway, service, or BFF. |
| MID-035-EX05 | 3 | A team wants to add stock-based pricing rules to the gateway. Write a short rejection with the better place. |
| MID-035-EX06 | 4 | Describe when Shop needs a BFF and sketch a mobile BFF response for the home screen. |

## Solutions
- **EX01** Routing, TLS termination, authentication, rate limiting, request shaping (headers, rewrites, correlation id); also CORS and logging.
- **EX02** Two routes with `Path=/api/products/**` to `http://catalog:8080` and `Path=/api/orders/**` to `http://orders:8080`, filter `StripPrefix=1`.
- **EX03** Resource-server config with `permitAll()` for `/api/products/**` and `authenticated()` otherwise; configure issuer or JWK set URI.
- **EX04** Gateway: TLS, CORS, rate limit, JWT signature check, request logging. Service: discount calculation, order ownership, payment retry (with idempotency). BFF: response aggregation. Feature flags per customer: service (or a flag service), not the gateway.
- **EX05** Pricing is business logic; it would couple the gateway to inventory data and force gateway releases for every rule. Put it in `catalog` or a pricing component.
- **EX06** A BFF is justified when mobile needs aggregated, smaller payloads (featured products, cart count, order status) in one call, different from web; it calls `catalog` and `orders` and returns one tailored JSON.

Quiz Q09 and Q10 also cover outcome 4.
