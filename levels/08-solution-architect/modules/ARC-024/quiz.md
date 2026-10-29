# ARC-024 · Integration patterns — Quiz

Outcomes: O1 choosing a style · O2 coupling, latency, failure · O3 integration catalog · O4 integration patterns.

**Q01 (O1)** Card authorization during checkout needs an answer immediately. The best style is: A. Nightly batch B. File exchange C. Synchronous API D. Daily CDC export
**Q02 (O1)** You cannot change the ERP application but need its stock changes quickly. Choose: A. CDC on its database B. Manual spreadsheets C. A weekly file D. Changing the ERP code
**Q03 (O2)** Temporal coupling means: A. Both sides share a database B. Both systems must be up at the same time C. Both use the same language D. Both use the same schema
**Q04 (O2)** If the consumer of stock events is down for an hour, usually: A. The sender fails B. Events are lost C. Events queue and the consumer catches up D. The ERP restarts
**Q05 (O2)** Which style has the loosest timing but tight format agreement? A. Synchronous API B. File exchange C. Direct database link D. Streaming only
**Q06 (O3)** An integration catalog row must include at least: A. Owner, style, frequency, and SLA B. Only the system name C. Only the vendor D. Only the diagram
**Q07 (O3)** A common catalog mistake is: A. Listing the SLA B. Naming an owner C. Having no owner for an interface D. Reviewing quarterly
**Q08 (O4)** Which pattern converts one system's message format to another's? A. Aggregator B. Content-based router C. Splitter D. Message translator
**Q09 (O1)** A marketing tool refreshes audiences once a day. The cheapest suitable integration is: A. Real-time events B. A daily file C. Synchronous API per customer D. CDC stream
**Q10 (O4)** Which pattern sends click-and-collect orders to stores and home delivery to warehouses? A. Content-based router B. Aggregator C. Translator D. Batch loader

## Answers
Q01 C · Q02 A · Q03 B · Q04 C · Q05 B · Q06 A · Q07 C · Q08 D · Q09 B · Q10 A

## Practical part
Integration catalog defense for Larkspur: the assessor challenges three style choices against latency and coupling needs. Pass: quiz at least 8/10, at least five of six exercises correct, and a catalog where every interface has an owner, SLA, and a justified style.
