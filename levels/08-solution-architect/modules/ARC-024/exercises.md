# ARC-024 · Integration patterns — Exercises and lab

## Lab
### ARC-024-LAB1 · Integration catalog
**Outcomes:** 1–4 · **Time:** ~4 h
1. Draw the context diagram of Larkspur and list every interface (ERP, CRM, payments, carriers, stores, marketing).
2. For each interface record direction, data set, owner, frequency, volume, and SLA.
3. Choose a style and justify it against latency need and coupling.
4. Add the failure behavior: what happens in an hour of downtime.
5. Mark where an integration pattern (translator, router, aggregator) is used and why.
6. Defend the catalog to a role-played integration lead.
**Acceptance:** each style choice justified against latency and coupling needs.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-024-EX01 | 1 | Choose a style for: card authorization, daily store takings, carrier tracking updates, loyalty points posted to CRM. Justify each in two lines. |
| ARC-024-EX02 | 2 | Fill a table for APIs, events, batch, and files: coupling, typical latency, and behavior during a one-hour outage. |
| ARC-024-EX03 | 3 | A catalog lists 14 interfaces and 5 have no owner and 4 no SLA. Write the fixes and who must agree. |
| ARC-024-EX04 | 4 | A multi-warehouse order must show one status. Name the patterns you use and sketch the flow. |
| ARC-024-EX05 | 1, 2 | A manager wants everything real-time. Write a short reply using the cost of coupling and the freshness actually needed. |
| ARC-024-EX06 | 3 | Review a catalog row "ERP to platform: sync REST, owner: IT". Give three corrections. |

## Solutions
- **EX01** Authorization: synchronous API (answer needed now). Takings: nightly batch (finance needs completeness, not speed). Tracking: carrier webhooks or polling API, event inside platform. Loyalty: asynchronous event with retry, as a short delay is fine.
- **EX02** API: tight, milliseconds, caller fails; events: loose, seconds, consumer catches up; batch: loose, hours, last data stays; files: loose on time, tight on format, wait for next file.
- **EX03** Assign a named owning team per interface, record an SLA agreed with consumers, review quarterly; owner and consumer agree on change notice.
- **EX04** Content-based router to warehouses, aggregator to join confirmations, translator for warehouse formats; status emitted as one OrderStatusChanged event.
- **EX05** Real-time adds temporal coupling and operating cost; ask who acts on the data and how quickly; use real-time only where a decision depends on it.
- **EX06** Name the owning team and contact; state frequency, volume, and SLA; justify the style or choose events or CDC given ERP availability.

Outcomes 1 and 3 are also covered by the lab defense; outcome 4 by the quiz.

**Workplace evidence:** an integration design you produced and how it held up in operation.
