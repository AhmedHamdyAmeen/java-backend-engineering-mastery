# MID-061 · Microservices introduction — Quiz

Outcomes: O1 benefits and costs · O2 modular monolith first · O3 extraction criteria · O4 distributed monolith.

**Q01 (O1)** A true benefit of microservices is: A. Free consistency across services B. No network calls C. Fewer deployments D. Independent deployment
**Q02 (O1)** A cost of microservices is: A. Local ACID transactions across services B. More operational work C. Fewer failure modes D. Simpler debugging
**Q03 (O1)** Replacing a cross-service transaction usually requires: A. A shared database B. A distributed lock only C. Eventual consistency, e.g. a saga D. Ignoring failures
**Q04 (O2)** Why is a modular monolith often a good first step? A. It is always faster at runtime B. Boundaries can be learned cheaply before paying network costs C. It forbids modules D. It needs Kubernetes
**Q05 (O3)** A valid driver for extracting a service is: A. It is trendy B. A team wants its own repository C. Every entity needs a service D. Independent scaling backed by load data
**Q06 (O3)** Before extracting a module you should confirm: A. It owns its data and has a clear context B. It has many callers C. It shares tables D. It has no tests
**Q07 (O3)** "Not extracting" as an ADR outcome is: A. Never allowed B. Acceptable when justified C. A failure D. Only for small teams
**Q08 (O4)** A sign of a distributed monolith: A. Independent releases B. Own database per service C. Lockstep releases and a shared database D. Async events
**Q09 (O4)** A common mistake when splitting: A. One service per entity B. Using bounded contexts C. Owning data per service D. Writing an ADR
**Q10 (O1)** Splitting "to scale" without data is risky because: A. Scaling is impossible B. The real bottleneck may be elsewhere and a cache could suffice C. Services cannot scale D. It reduces latency

## Answers
Q01 D · Q02 B · Q03 C · Q04 B · Q05 D · Q06 A · Q07 B · Q08 C · Q09 A · Q10 B

## Practical part
Five exercises `MID-061-EX01` to `EX05` plus the lab. Pass: at least four exercises correct and an ADR whose decision follows explicit criteria.
