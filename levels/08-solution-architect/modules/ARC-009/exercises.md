# ARC-009 · Enterprise integration — Exercises and lab

## Lab
### ARC-009-LAB1 · Larkspur integration architecture
**Outcomes:** 1–4 · **Time:** ~4 h
1. Build the interface catalog: system pair, style, direction, volume, latency, owner, error handling.
2. Cover ERP, CRM, payments, stores, and carriers.
3. Justify the style of each interface using latency, volume, coupling, ownership, and system capabilities.
4. Decide where canonical data is used and where not.
5. Draw the target integration diagram.
6. Define monitoring, retry, dead-letter, and escalation rules per interface.
**Acceptance:** every interface justifies its style; failure handling defined.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-009-EX01 | 1 | Compare API, event, ESB, iPaaS, batch, and file exchange for Larkspur across latency, coupling, and operational cost. |
| ARC-009-EX02 | 2 | Choose a style for five interfaces (payment authorization, order to ERP, stock updates from stores, carrier tracking, CRM customer sync) and justify. |
| ARC-009-EX03 | 2 | The ERP's API allows 20 calls per second; the platform needs 200 order updates per second at peak. Propose a design. |
| ARC-009-EX04 | 3 | Decide where Larkspur should use a canonical Order model and where not. |
| ARC-009-EX05 | 4 | Write the failure handling for the order-to-ERP interface when the ERP is down for two hours. |
| ARC-009-EX06 | 4 | Assign owners and define three monitoring checks for each of four interfaces. |

## Solutions
- **EX01** API: immediate, coupling of availability; event: loose, eventual consistency; ESB: central mediation, bottleneck risk; iPaaS: quick connectors, vendor limits; batch/file: simple, high latency, fits legacy.
- **EX02** Payment: synchronous API; order to ERP: event with adapter and queue; stock: events; carrier tracking: carrier API with polling fallback; CRM sync: events with periodic reconcile.
- **EX03** Buffer through a queue, batch updates, and rate-limit toward the ERP; keep the platform as system of engagement for orders; sync to ERP asynchronously.
- **EX04** Canonical Order and Customer events between platform, CRM, and reporting; no canonical model for the carrier API, handled by an adapter.
- **EX05** Queue orders durably, retry with backoff, idempotent posting, alert when backlog exceeds threshold, dead-letter for bad messages, reconcile after recovery.
- **EX06** Owner per interface (named team); checks: lag or backlog, error rate, daily reconciliation count; alert thresholds and escalation path.

**Workplace evidence:** an integration architecture you designed across enterprise systems.
