# ARC-026 · Event architecture — Quiz

Outcomes: O1 event ownership · O2 event catalog and schemas · O3 compatibility and evolution · O4 event backbone decision.

**Q01 (O1)** Who should own an event? A. Every consumer B. The system of record for the fact C. The broker vendor D. The newest team
**Q02 (O1)** Two systems publishing the same event name leads to: A. Faster delivery B. Better security C. Conflicting versions D. Lower cost
**Q03 (O2)** An event catalog entry should include: A. Owner, schema, consumers, and delivery guarantee B. Only a name C. Only a diagram D. Only the topic
**Q04 (O2)** Why avoid events that mirror database tables? A. They leak the internal schema and couple consumers to it B. They are too small C. Brokers reject them D. They are faster
**Q05 (O3)** Which change is usually backward compatible? A. Removing a field B. Renaming a field C. Adding an optional field D. Changing a field type
**Q06 (O3)** A breaking change should be handled by: A. Silent overwrite B. A new version published alongside the old with a retirement date C. Email only D. Deleting the old consumers
**Q07 (O3)** Where should compatibility checks run? A. Manually after release B. In production only C. In customer support D. Automatically in the owner's build
**Q08 (O4)** Which situation most supports an event backbone? A. Two systems with a few daily messages B. One consumer C. Many producers and consumers with replay needs D. No integration
**Q09 (O4)** What is a cost of adopting a backbone? A. No operations B. A platform to run, skills, and governance C. Fewer events D. No schemas
**Q10 (O1)** In a past-tense event name such as OrderPlaced, the event: A. Orders a system to act B. Asks for permission C. Is optional D. Reports a fact that has happened

## Answers
Q01 B · Q02 C · Q03 A · Q04 A · Q05 C · Q06 B · Q07 D · Q08 C · Q09 B · Q10 D

## Practical part
Catalog review of the Larkspur event catalog: the reviewer checks one owner per event and the documented evolution process. Pass: quiz at least 8/10, all five exercises correct, and a catalog with no shared ownership.
