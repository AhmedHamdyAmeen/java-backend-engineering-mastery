# SRB-007 · Data platform integration — Lecture scripts

**Video:** 86 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-007-L01 · Integrating systems you can't change (10 min)
**Goal:** choose integration approaches when legacy code is off limits.

**Key points**
- Options: database triggers, polling, file exports, API wrappers, and log-based CDC.
- Constraints: no code changes, load on the legacy database, data ownership.
- Pick the least invasive approach that meets latency needs.
- Always keep a path to reconcile.

**Show:** a comparison table of polling, triggers, and log-based CDC with latency, load, risk, and the need to change legacy code.

**Check:** Why prefer CDC for legacy databases? *(It reads the log without changing application code.)*

---

## SRB-007-L02 · Change data capture with Debezium (14 min)
**Goal:** explain how Debezium turns database changes into events.

**Key points**
- Debezium reads the database's transaction log (for PostgreSQL, logical decoding) and emits change events.
- Each event has before, after, operation, and source position.
- Initial snapshot then streaming; the replication slot must be monitored or it fills disk.
- Schema changes in the source reach consumers; plan for them. Verify version before recording.

**Show:** a YAML outline of a connector config (database host, slot name, table include list, snapshot mode) and a sample change event JSON with before/after.

**Check:** What must you monitor with PostgreSQL CDC? *(The replication slot lag and retained WAL size.)*

---

## SRB-007-L03 · From CDC events to domain events (10 min)
**Goal:** translate table changes into meaningful business events.

**Key points**
- A CDC event says a row changed, not why.
- Domain events carry business meaning and a stable contract.
- Translate in an anti-corruption layer owned by the consuming or integration team.
- Never expose raw table changes as the public contract.

**Show:** mapping: stock_levels row update (qty 12 -> 9) becomes StockLevelChanged {sku, warehouse, available, reason: unknown, occurredAt}; a translator service with tests.

**Check:** Why not publish raw CDC as the contract? *(It couples consumers to the legacy schema.)*

---

## SRB-007-L04 · Stream processing concepts (12 min)
**Goal:** describe enrichment and aggregation on streams.

**Key points**
- Stream processors apply stateful operations: joins, windows, aggregations.
- Event time versus processing time; late events need a policy.
- State stores are rebuilt from changelog topics, so recovery has a cost.
- Choose Kafka Streams for library-style, Flink for larger stateful jobs; verify before recording.

**Show:** a topology: stock changes joined with a product table, aggregated per warehouse in 1-minute windows, written to a topic.

**Check:** What is a late event? *(One arriving after its time window was processed.)*

---

## SRB-007-L05 · Analytics pipelines and data ownership (10 min)
**Goal:** feed analytics without losing control of data.

**Key points**
- The owning team decides what leaves the domain; consumers do not read raw tables.
- Minimize and mask personal data before it reaches analytics.
- Record lineage: where data comes from and who uses it.
- Retention and deletion requests must reach copies.

**Show:** a data product outline: owner, schema, sensitivity, retention, deletion path, consumers.

**Check:** Who decides what data leaves a domain? *(The owning team.)*

---

## SRB-007-L06 · Demo: streaming FulfillCo's stock table without touching its code (15 min)
**Goal:** capture stock changes from the legacy database.

**Steps**
1. Show the stock table and enable logical replication with a dedicated user (verify setup before recording).
2. Configure the Debezium connector and take the initial snapshot.
3. Update a stock row and watch the change event.
4. **Planned mistake:** capture all columns of the table; fix by using a column include list.
5. Translate to StockLevelChanged and show Shop's consumer updating within seconds.

Prepares SRB-007-LAB1.

---

## SRB-007-L07 · Demo: filtering personal data out of a CDC stream (15 min)
**Goal:** keep personal data out of downstream topics.

**Steps**
1. Show a table mixing stock and customer pickup contact columns.
2. Connector column exclude and masking for sensitive fields.
3. Verify downstream topics contain no personal data using a scan.
4. **Planned mistake:** filter only in the consumer, leaving personal data on the broker; fix by filtering at the source connector.
5. Document the control in the data product description.

Prepares SRB-007-LAB1.

---
