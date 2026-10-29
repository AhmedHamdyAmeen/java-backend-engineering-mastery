# SRC-014 · Data integrity — Exercises and lab

## Lab
### SRC-014-LAB1 · Money matches
**Outcomes:** 1–4 · **Time:** ~4 h
Build a daily reconciliation between orders, payments, and the payment provider's settlement file. Plant three discrepancy types (for example charge without order, order without charge, amount mismatch). Detect and repair them, with audit rows for every repair.
**Acceptance:** report with counts, repairs logged and auditable.

## Exercises (assessment: invariant analysis of an unseen workflow)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-014-EX01 | 1 | List five invariants spanning orders, inventory, and payments, and state prevent, detect, or repair for each. |
| SRC-014-EX02 | 2 | Explain to a product manager why "exactly-once delivery" is not offered, and what the team builds instead. |
| SRC-014-EX03 | 2 | Design an idempotent payment call, including key generation, storage, and behavior on timeout. |
| SRC-014-EX04 | 3 | Write the reconciliation algorithm and the repair rules for the three planted discrepancy types. |
| SRC-014-EX05 | 4 | Design the audit schema for refunds and write which events must be recorded. |
| SRC-014-EX06 | 1 | Case (unseen): a workflow with order, stock reservation, payment, shipment. Identify where invariants can break on partial failure. |

## Solutions
- **EX01** Examples: payment captured implies order (detect by reconciliation, repair by refund or order creation); stock not negative (prevent with conditional update); order total equals line sum (prevent with a constraint or domain rule); event published implies row committed (prevent with outbox); refund at most captured (prevent in code, detect).
- **EX02** Networks can drop messages or acknowledgments, so senders retry. We make operations idempotent so repeats have one effect.
- **EX03** Key derived from order ID and attempt, persisted before the call; on timeout, retry with the same key or query the provider; store the provider response per key.
- **EX04** Join by provider reference; charge without order: create or refund after review; order without charge: mark unpaid or retry capture; amount mismatch: flag and adjust per policy. All repairs write audit rows and the job is re-runnable.
- **EX05** Columns: actor, time, entity, before and after, reason, correlation ID; append-only; record refund request, approval, provider call, and result.
- **EX06** Partial failures: payment captured but reservation failed; stock reserved but payment failed (release); shipment created but payment reversed. Each needs prevention (saga, outbox) and detection.
- Outcome 3 is also covered by the lab report and Q06-Q08.

**Workplace evidence:** a reconciliation or integrity check you introduced and what it found.
