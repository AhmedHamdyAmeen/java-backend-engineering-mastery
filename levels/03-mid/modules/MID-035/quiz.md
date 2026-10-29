# MID-035 · API gateways — Quiz

Outcomes: O1 responsibilities · O2 Spring Cloud Gateway · O3 gateway vs services · O4 BFF.

**Q01 (O1)** Which is a typical gateway responsibility? A. Price calculation B. Database migration C. TLS termination D. Order business rules
**Q02 (O1)** A gateway gives clients: A. Several public addresses B. One public entry point C. Direct service ports D. No authentication
**Q03 (O2)** In Spring Cloud Gateway a predicate: A. Matches requests to a route B. Modifies the response C. Starts the service D. Stores sessions
**Q04 (O2)** `StripPrefix=1` does what? A. Adds a header B. Encrypts the path C. Removes the first path segment before forwarding D. Blocks the request
**Q05 (O2)** Gateway filters should: A. Block threads with JDBC calls B. Never be used C. Run only in services D. Stay non-blocking
**Q06 (O3)** "Customer may only see their own orders" belongs in: A. The orders service B. The gateway C. The browser D. DNS
**Q07 (O3)** A gateway full of business rules becomes: A. Faster B. A new monolith and bottleneck C. Stateless D. A BFF
**Q08 (O3)** Services should: A. Trust any internal request without a token B. Accept all headers as identity C. Be exposed publicly D. Still validate identity and not be directly reachable from outside
**Q09 (O4)** A BFF is: A. A client-specific backend API B. A database C. A cache eviction policy D. A message broker
**Q10 (O4)** The BFF differs from the gateway because it: A. Handles TLS B. Shapes data for a specific client C. Replaces services D. Does rate limiting only

## Answers
Q01 C · Q02 B · Q03 A · Q04 C · Q05 D · Q06 A · Q07 B · Q08 D · Q09 A · Q10 B

## Practical part
Six exercises `MID-035-EX01` to `EX06` including the responsibility-placement exercise, plus `MID-035-LAB1`. Pass: at least five exercises, correct placement of at least 8 of 10 concerns, and a lab where services are unreachable except through the gateway.
