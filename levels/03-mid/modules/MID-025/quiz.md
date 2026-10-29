# MID-025 · Service boundaries — Quiz

Outcomes: O1 bounded contexts · O2 data ownership · O3 replacing joins · O4 evaluating boundaries.

**Q01 (O1)** Bounded contexts are best identified from: A. Database tables B. Class names C. Package sizes D. Language and ownership
**Q02 (O1)** The same word with different meanings in two areas suggests: A. A typo B. Two contexts C. A missing index D. A single shared model
**Q03 (O1)** What should contexts share about a product? A. The whole class B. The ORM entity C. The identifier D. The table
**Q04 (O2)** Who may read `inventory`'s tables directly? A. `orders` B. `payments` C. A reporting job from any service D. Only the inventory service
**Q05 (O2)** A shared database between services mainly creates: A. Hidden coupling B. Faster releases C. Independent scaling D. Clear ownership
**Q06 (O3)** Which replaces a cross-service join? A. A foreign key between databases B. Shared credentials C. A snapshot, local copy, or API composition D. A bigger server
**Q07 (O3)** Why store the unit price in the order line? A. Catalog prices never change B. It saves disk space C. It is required by SQL D. The price at purchase time must stay fixed
**Q08 (O3)** A local copy built from events is: A. Always fresh B. Possibly stale for a short time C. Forbidden D. A shared table
**Q09 (O4)** A sign of a wrong boundary: A. One use case touching one service B. Few calls C. Chatty calls and lockstep releases D. Separate data
**Q10 (O4)** Boundaries drawn by technical layer (UI service, DB service) are: A. Recommended B. Required by DDD C. Required by Kubernetes D. A common mistake

## Answers
Q01 D · Q02 B · Q03 C · Q04 D · Q05 A · Q06 C · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Five exercises `MID-025-EX01` to `EX05` plus the lab. Pass: at least four exercises correct, no cross-service table access in the lab, and a documented context map.
