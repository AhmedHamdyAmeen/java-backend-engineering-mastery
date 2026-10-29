# SRB-007 · Data platform integration — Exercises and lab

## Lab
### SRB-007-LAB1 · Stock sync
**Outcomes:** 1, 2, 3, 4 · **Time:** ~4 h
1. Set up Debezium on a copy of FulfillCo's database with a table include list.
2. Translate change events into the StockLevelChanged domain event.
3. Consume it in Shop's inventory and measure end-to-end delay.
4. Exclude personal data and record replication slot monitoring.
**Acceptance:** Shop sees stock changes within seconds; FulfillCo code unchanged.

## Exercises
| ID | Outcome | Task |
| --- | --- | --- |
| SRB-007-EX01 | 1 | List three constraints in capturing from legacy and the CDC mitigation for each. |
| SRB-007-EX02 | 1 | Describe monitoring for a PostgreSQL replication slot. |
| SRB-007-EX03 | 2 | Translate this row change (qty 12 to 9) into a domain event and explain what is unknown. |
| SRB-007-EX04 | 2 | Review a design that exposes the raw stock_levels topic to all teams. Write the critique. |
| SRB-007-EX05 | 3 | Design an aggregation of stock per warehouse per minute and state the late-event policy. |
| SRB-007-EX06 | 4 | Plan pushing stock data to analytics with personal data removed and deletion handled. |

## Solutions
- **EX01** No code change: log-based; load: reads WAL; ordering: transaction log order and source positions.
- **EX02** Alert on retained WAL size and slot lag; plan for a stalled connector.
- **EX03** StockLevelChanged with available 9; the reason is unknown unless more context; do not guess.
- **EX04** Couples consumers to the schema, leaks columns, no owner; add a translation layer and a contract.
- **EX05** Tumbling 1-minute windows with a grace period, late events dropped or counted separately.
- **EX06** Source-side filter, data product contract, retention and deletion propagation, lineage.

**Workplace evidence:** a legacy integration you delivered with CDC or a similar technique.
