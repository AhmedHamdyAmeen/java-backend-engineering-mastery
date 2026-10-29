# MID-049 · Reliability — Exercises and lab

## Lab
### MID-049-LAB1 · Checkout SLOs
**Outcomes:** 1–4 · **Time:** ~2 h
Define SLIs and SLOs for checkout and search, with burn-rate alerts, and write a short SLO document including the budget policy.
**Acceptance:** SLO document reviewed; alerts tested with injected errors.

## Exercises (assessment: SLO document review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-049-EX01 | 1 | For Shop's search and checkout, write one availability SLI and one latency SLI as good/valid ratios. |
| MID-049-EX02 | 1 | Explain why a SLI measured inside the service can miss failures users see. |
| MID-049-EX03 | 2 | Compute the error budget in requests and in minutes for a 99.9% SLO over 30 days with 10 million requests. |
| MID-049-EX04 | 2 | Propose an SLO for search and justify why it is not 100%. |
| MID-049-EX05 | 3 | Write a two-window burn-rate alert (page and ticket) for checkout. |
| MID-049-EX06 | 4 | Write a budget policy with actions at three remaining-budget levels. |
| MID-049-EX07 | 1–4 | Review a sample SLO document with a 100% target and server-side SLIs; list fixes. |

## Solutions
- **EX01** Availability: successful checkouts / valid checkout requests; latency: search responses under 300 ms / all search responses.
- **EX02** Requests rejected at the load balancer or gateway, or timeouts before reaching the service, never appear in service metrics.
- **EX03** Budget 0.1%: 10,000 failed requests; about 43.2 minutes of full outage (30 days × 24 h × 60 × 0.001).
- **EX04** For example 99.5% of searches under 300 ms; users tolerate an occasional slow search; the cost of 100% is unbounded.
- **EX05** Page: 1h and 5m ratios above 14 × 0.001; ticket: 6h and 30m above 6 × 0.001 (thresholds are a team choice).
- **EX06** Above 50%: normal releases; 10-50%: extra review and canaries; below 10%: reliability work only until recovered.
- **EX07** Replace 100% with a realistic target, measure at the gateway, add the budget policy and burn-rate alerts.
