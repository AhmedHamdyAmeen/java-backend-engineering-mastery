# SRB-002 · Event-driven architecture — Quiz

Outcomes: O1 contracts · O2 ownership and catalog · O3 schema evolution · O4 replay and backfill.

**Q01 (O1)** Event-carried state transfer means the event: A. Contains the data consumers need B. Only holds an ID C. Is always encrypted D. Is never versioned
**Q02 (O1)** A good domain event name is: A. orders_table_changed B. UpdateOrderRow C. OrderReadyForFulfillment D. ORDER_DATA
**Q03 (O1)** Leaking internal models as events causes: A. Faster delivery B. Consumers coupled to publisher internals C. Smaller schemas D. Lower cost
**Q04 (O2)** Event ownership belongs to: A. Every consuming team B. The broker admin C. The newest team D. The team publishing the fact
**Q05 (O2)** An event catalog should record: A. Only topic names B. Only developer names C. Owner, schema, sensitivity, consumers D. Only retention
**Q06 (O3)** Which change is backward compatible? A. Adding an optional field B. Renaming a field C. Removing a field D. Changing a field's meaning
**Q07 (O3)** A breaking change is best released as: A. An in-place edit B. A silent change C. A Friday deploy D. A new versioned topic or type run in parallel
**Q08 (O4)** Replay danger arises mostly from: A. Small payloads B. Consumers with external side effects C. Using Avro D. Many partitions
**Q09 (O4)** A safe replay for an email consumer uses: A. Faster consumers B. Deleting the topic C. Replay mode and dedupe by event id D. More partitions
**Q10 (O4)** Backfills should be: A. Run at maximum speed B. Run on the live consumer group C. Skipped D. Throttled and isolated from live traffic

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Contract review: review a peer's event contract against the checklist. Pass: 70% on the quiz and a review that finds at least three real issues in a flawed contract.
