# MID-048 · Monitoring — Exercises and lab

## Lab
### MID-048-LAB1 · Shop dashboards
**Outcomes:** 1–3 · **Time:** ~2.5 h
Build one dashboard per service plus a business overview. Add alerts for error rate and latency, each with a runbook.
**Acceptance:** a fault injected by the instructor triggers exactly one actionable alert.

## Exercises (assessment: dashboard and alert review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-048-EX01 | 1 | Configure Prometheus to scrape a Shop service and confirm the target is up. |
| MID-048-EX02 | 1 | Write PromQL for request rate, error ratio, and p95 latency of `orders`. |
| MID-048-EX03 | 1 | Explain why `rate()` is needed for counters and what a range of `[5m]` means. |
| MID-048-EX04 | 2 | Build a RED dashboard and a USE row (heap, GC, DB pool) for one service. |
| MID-048-EX05 | 3 | Write an error-rate alert with `for:`, severity, and a runbook link. |
| MID-048-EX06 | 3 | Rewrite a CPU-above-80% alert as a symptom-based alert. |
| MID-048-EX07 | 2–3 | Review a given dashboard and alert set: list what to delete, fix, and add. |

## Solutions
- **EX01** Add a scrape config or a service/pod monitor; the targets page shows `UP`.
- **EX02** Rate: `sum(rate(..._count[5m]))`; ratio as in the lecture; p95 with `histogram_quantile`.
- **EX03** Counters only increase and reset on restart; `rate` gives per-second increase over the window and handles resets.
- **EX04** Panels: rate, errors, p50/p95/p99, heap used, GC pause, pool active versus max.
- **EX05** `expr` on the error ratio, `for: 5m`, label `severity: page`, annotation `runbook_url`.
- **EX06** Alert on checkout error ratio and p95 latency; keep CPU as a dashboard panel (cause), not a page.
- **EX07** Typical findings: averages, no runbook links, alerts on causes, duplicate alerts for one fault.

**Outcome 3** is also checked by the lab criterion "exactly one actionable alert".
