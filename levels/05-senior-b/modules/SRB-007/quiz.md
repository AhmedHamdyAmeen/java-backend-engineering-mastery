# SRB-007 · Data platform integration — Quiz

Outcomes: O1 CDC · O2 CDC vs domain events · O3 stream processing · O4 analytics and ownership.

**Q01 (O1)** Debezium on PostgreSQL reads: A. The write-ahead log via logical decoding B. Application logs C. HTTP traffic D. Backups only
**Q02 (O1)** An unmonitored replication slot can: A. Delete data B. Speed up queries C. Fill the disk with retained WAL D. Close connections
**Q03 (O1)** CDC avoids changing legacy code because it: A. Rewrites the code B. Observes the database log C. Uses triggers in code D. Uses polling in code
**Q04 (O2)** A CDC event describes: A. A business reason B. An HTTP call C. A schema design D. A row change
**Q05 (O2)** Public contracts should be: A. Raw table changes B. SQL dumps C. Domain events D. Log lines
**Q06 (O2)** Translation from CDC to domain events belongs in: A. An anti-corruption layer B. The consumer UI C. The broker D. The firewall
**Q07 (O3)** Event time differs from processing time because: A. Clocks stop B. Kafka rewrites time C. Brokers sort by size D. Events can arrive late or out of order
**Q08 (O3)** Stateful stream state is recovered from: A. Browser storage B. Changelog topics C. Emails D. Source code
**Q09 (O4)** Personal data should be filtered: A. Never B. Only in dashboards C. At the source connector D. Only after analytics
**Q10 (O4)** Who owns data given to analytics? A. The analytics team only B. Nobody C. The broker admin D. The producing domain team

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Integration design review of the lab's stock sync, including privacy controls. Pass: 70% on the quiz and a design with a translation layer and filtered personal data.
