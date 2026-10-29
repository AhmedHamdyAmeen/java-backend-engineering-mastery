# MID-036 · Service discovery — Exercises and lab

## Lab
### MID-036-LAB1 · Scale out
**Outcomes:** 1–3 · **Time:** ~1.5 h
Run three `inventory` replicas behind Compose DNS (no fixed host ports). Make `orders` call `inventory` by name and log which replica answered. Run a load test and kill one replica partway through. Record error counts and latency before, during, and after.

**Acceptance:** errors are limited to in-flight requests on the killed replica; a short written explanation says why, and what retries and graceful shutdown would change.

## Exercises (assessment: quiz)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-036-EX01 | 1 | Compare client-side and server-side discovery in a table with an example of each. |
| MID-036-EX02 | 2 | Replace hard-coded hosts in the Shop config with Compose service names and environment variables. |
| MID-036-EX03 | 2 | Show that DNS resolves `inventory` to several addresses inside the Compose network and explain JVM caching effects. |
| MID-036-EX04 | 3 | Explain what a readiness probe does for routing during a rolling deployment. |
| MID-036-EX05 | 1 | Choose a load-balancing strategy for fast uniform GETs and for mixed fast and slow requests. |
| MID-036-EX06 | 3 | List steps for a graceful shutdown of a Spring Boot service so in-flight requests finish. |

## Solutions
- **EX01** Client-side: caller asks a registry and picks (Eureka). Server-side: caller uses a stable name or proxy that picks (Compose DNS, Kubernetes Service). Client-side adds library and registry; server-side hides it.
- **EX02** `INVENTORY_URL: http://inventory:8080` in Compose and `@Value("${inventory.url}")` or a property class.
- **EX03** From the `orders` container, `getent hosts inventory` (or `nslookup`) lists addresses; JVM and HTTP client caches plus keep-alive connections can pin traffic to one replica.
- **EX04** Only instances reporting ready receive traffic; new Pods join after passing readiness and old ones leave before termination, so traffic does not hit instances that are starting or stopping.
- **EX05** Round robin for uniform GETs; least connections (or power of two choices) for mixed durations.
- **EX06** Enable `server.shutdown=graceful`, set a shutdown timeout, fail readiness first, wait for load balancer to stop sending traffic, then finish in-flight work and exit (verify property names for your Spring Boot version).

Outcome 3 is also covered by quiz Q08 to Q10.
