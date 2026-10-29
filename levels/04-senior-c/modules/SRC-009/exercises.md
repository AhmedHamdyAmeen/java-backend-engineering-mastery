# SRC-009 · Failure-mode analysis — Exercises and lab

## Lab
### SRC-009-LAB1 · Order subsystem FMEA
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. Map dependencies for the order subsystem, including hidden ones, and mark failure domains.
2. Run an FMEA with likelihood, impact, and detection ratings; rank the results.
3. Design graceful degradation for the top failure modes.
4. Run three failure-injection experiments against the platform (hypothesis, blast radius, stop condition) and record results.
**Acceptance:** at least one previously unknown weakness found and fixed.

## Exercises (FMEA review; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-009-EX01 | 1 | Add five hidden dependencies to a checkout dependency map and mark critical versus optional. |
| SRC-009-EX02 | 1 | Two services share one database cluster. Describe the failure domain and a way to reduce blast radius. |
| SRC-009-EX03 | 2 | Complete three FMEA rows (payment slow, certificate expiry, replica lag) with L, I, D and score. |
| SRC-009-EX04 | 3 | Design degradation for "inventory service unavailable" during checkout, including data safety. |
| SRC-009-EX05 | 4 | Write an experiment sheet for "payment provider adds 3 s latency". |
| SRC-009-EX06 | 3 | Review a degradation design that drops order events when Kafka is down; fix it. |

## Solutions
- **EX01** For example DNS, identity provider, config service, certificate authority, secrets store, container registry; critical ones need timeouts and fallbacks.
- **EX02** Both fail together if the cluster fails; reduce with separate clusters or schemas with resource isolation, connection limits, and independent failover.
- **EX03** Payment slow: L3 I5 D2 = 30; certificate expiry: L2 I5 D4 = 40, detect with expiry monitoring; replica lag: L4 I3 D3 = 36. Actions follow from the highest scores. Ratings are examples; justify yours.
- **EX04** Options: reserve against cached stock with a flag, accept orders as "pending confirmation" with reconciliation, or show unavailable; never promise stock you cannot reserve without telling the user; keep data consistent via idempotent reconciliation.
- **EX05** Hypothesis: checkout p99 stays under budget by timing out and queueing payment retry; injection latency 3 s on the payment stub in staging; metrics: threads, error rate; stop if error rate exceeds 5%; record the result and fixes.
- **EX06** Dropping events silently corrupts downstream state; use an outbox so events persist in the database and publish later, with alerts on backlog.

**Workplace evidence:** a failure-mode review or game day you led.
