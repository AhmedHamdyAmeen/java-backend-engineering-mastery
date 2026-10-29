# ARC-032 · Integration with enterprise systems — Quiz

Outcomes: O1 ERP and systems of record · O2 CRM integration · O3 payments and identity providers · O4 anti-corruption layers.

**Q01 (O1)** A system of record is: A. The newest system B. The cheapest system C. The fastest system D. The authoritative place for a data set
**Q02 (O1)** To write an order posting into the ERP you should: A. Write to its database tables B. Send a command through its supported interface or adapter C. Edit exports by hand D. Ask users to retype
**Q03 (O1)** Queueing postings to the ERP mainly: A. Absorbs peaks and outages and protects the ERP B. Removes the need for reconciliation C. Makes the ERP faster D. Stores card data
**Q04 (O2)** In CRM integration the urgent direction for consent changes is: A. Granting B. Reporting C. Withdrawal D. Archiving
**Q05 (O2)** For a single service-agent view you should: A. Copy all data everywhere B. Show orders and cases through APIs from their owners C. Give agents database access D. Use spreadsheets
**Q06 (O3)** A payment call times out. The state is: A. Failed B. Succeeded C. Cancelled D. Unknown, so query the provider with the idempotency key
**Q07 (O3)** Payment reconciliation compares: A. Gateway settlement, platform records, and ERP postings B. Only the platform records C. Only emails D. Logs and screenshots
**Q08 (O3)** If the identity provider is down, the design should: A. Define what existing sessions and staff can still do B. Disable all logins forever C. Share one password D. Ignore it
**Q09 (O4)** The main purpose of an anti-corruption layer is to: A. Speed up the ERP B. Encrypt traffic C. Keep the ERP's model and codes out of the new platform's domain D. Replace the ERP
**Q10 (O4)** An ERP upgrade changes field names. With a good ACL: A. Only the adapter changes B. All services change C. Nothing can be done D. The platform stops

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 B · Q06 D · Q07 A · Q08 A · Q09 C · Q10 A

## Practical part
Integration design defense of the lab design plus exercises `ARC-032-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab where every flow names the system of record and the behavior when the other side is down.
