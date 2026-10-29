# MID-026 · Messaging fundamentals — Quiz

Outcomes: O1 queues and topics · O2 commands and events · O3 delivery semantics · O4 event payloads.

**Q01 (O1)** In a queue with competing consumers, each message is delivered to: A. Every consumer B. No consumer C. One consumer D. Only the first subscriber ever
**Q02 (O1)** Which model fits "notify all interested services"? A. Topic (publish/subscribe) B. Point-to-point queue C. Database polling only D. Direct HTTP only
**Q03 (O2)** Which name is a well-formed event? A. `ReserveStock` B. `OrderPlaced` C. `PlaceOrderNow` D. `DoPayment`
**Q04 (O2)** A command differs from an event because it: A. Is always past tense B. Has unlimited listeners C. Asks for something to be done and can be rejected D. Cannot be sent
**Q05 (O2)** `OrderPlacedPleaseReserveStock` is a: A. Good event B. Command in disguise C. Schema version D. Delivery guarantee
**Q06 (O3)** At-least-once delivery means: A. Messages can be lost B. Messages can never repeat C. Each message is processed exactly once D. No loss, but duplicates are possible
**Q07 (O3)** Why is end-to-end exactly-once delivery unavailable? A. Brokers are slow B. Acks can be lost, so redelivery cannot be ruled out C. JSON cannot be parsed twice D. Queues cannot store messages
**Q08 (O3)** Effectively-once is achieved by: A. At-most-once delivery B. Idempotent handling with at-least-once delivery C. Disabling acknowledgments D. Faster networks
**Q09 (O4)** The `eventId` is used mainly for: A. Sorting by time B. Encrypting C. Duplicate detection D. Routing to a queue
**Q10 (O4)** A common payload mistake: A. Including a version B. Including the aggregate ID C. Including a timestamp D. Sending an entire database row

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 D · Q07 B · Q08 B · Q09 C · Q10 D

## Practical part
Five exercises `MID-026-EX01` to `EX05` plus the lab. Pass: at least four exercises correct and a peer-reviewed event catalog with owners, past-tense names, schemas, and versions.
