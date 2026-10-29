# MID-059 · Architectural styles — Quiz

Outcomes: O1 compare styles · O2 isolate the domain · O3 modular monolith · O4 choose a style.

**Q01 (O1)** In hexagonal architecture, who owns a port interface? A. The domain B. The adapter C. The framework D. The database
**Q02 (O1)** The dependency rule says source dependencies point: A. Downward to the database B. Outward to frameworks C. Inward toward the domain D. In any direction
**Q03 (O1)** A main weakness of classic layering is: A. Too many modules B. The domain ends up depending on persistence C. It cannot be tested D. It needs microservices
**Q04 (O2)** Which import should the domain package NOT contain? A. `java.time.Instant` B. `jakarta.persistence.Entity` C. `java.util.List` D. Its own port interface
**Q05 (O2)** Swapping the payment provider should require changes in: A. The domain B. The use cases C. The adapter D. The ports and domain
**Q06 (O3)** A boundary in a modular monolith is reliable when: A. Developers agree to respect it B. A build or ArchUnit check fails on violations C. Packages are named well D. It is documented in a wiki
**Q07 (O3)** Modules in a modular monolith should: A. Share tables freely B. Import each other's internals C. Use one giant package D. Call each other's public API
**Q08 (O2)** Interfaces for every class "just in case" is: A. Required by hexagonal B. Mandatory in Spring C. A common mistake without boundary meaning D. Faster at runtime
**Q09 (O4)** A small team with an unclear, fast-changing domain should usually start with: A. Twenty microservices B. One shared database for everyone C. No structure at all D. A modular monolith
**Q10 (O4)** Which driver is NOT central when choosing a style? A. Team size B. Domain complexity C. Change rate D. The IDE colour theme

## Answers
Q01 A · Q02 C · Q03 B · Q04 B · Q05 C · Q06 B · Q07 D · Q08 C · Q09 D · Q10 D

## Practical part
Five exercises `MID-059-EX01` to `EX05` plus the lab. Pass: at least four exercises correct (including EX05 with the three drivers named), ArchUnit tests passing, and the payment adapter swapped without domain changes.
