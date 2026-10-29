# SRC-012 · SLO engineering — Exercises and lab

## Lab
### SRC-012-LAB1 · 99.95% for orders
**Outcomes:** 1–4 · **Time:** ~4 h
Define SLIs and SLOs for the order journey consistent with the 99.95% commitment, with dependency SLOs and a composition check. Write an error-budget policy and agree it with role-played product leadership. Build multi-window burn-rate alerts and tune them by replaying recorded error data.
**Acceptance:** alert simulation shows no pages for brief blips and fast pages for real outages.

## Exercises (assessment: SLO and policy review)
| ID | Outcome | Task |
| --- | --- | --- |
| SRC-012-EX01 | 1 | Define an SLI and SLO for "customer sees order confirmation": good and valid events, window, target. |
| SRC-012-EX02 | 1 | Compute the composite availability for gateway 99.99%, orders 99.95%, payment provider 99.9% in series. Is 99.95% achievable? What would you change? |
| SRC-012-EX03 | 2 | Write an error-budget policy with three thresholds, actions, and an exception process. |
| SRC-012-EX04 | 3 | Given a 99.95% SLO over 30 days, pick burn-rate rules for page and ticket and justify the windows. |
| SRC-012-EX05 | 3 | A rule pages 12 times a month, 2 for real incidents. Compute precision and propose a fix. |
| SRC-012-EX06 | 4 | Review an SLO set: one at 100% for a year, one measured inside the service, one never alerted on. Recommend actions. |

## Solutions
- **EX01** Good: HTTP 2xx confirmation under the latency target; valid: all order submissions excluding client errors; 30 days; 99.95%.
- **EX02** 0.9999 × 0.9995 × 0.999 ≈ 0.9984, about 99.84%: not enough. Make the payment dependency soft (queue and confirm later), add retries with limits, or negotiate the dependency SLO.
- **EX03** Example: below 50% spent, normal; over 50%, risky changes need extra review; over 100%, freeze feature releases except reliability work; exception by named approver, logged.
- **EX04** Page: 14.4× over 1 h with 5 min check (about 2% budget spent); ticket: 1× over 3 days with 6 h check. Verify against your window. Long window gives significance, short gives reset.
- **EX05** Precision 2/12, about 17%. Replace with burn-rate windows or lengthen window; replay to confirm recall is kept.
- **EX06** Retire or tighten the 100% SLO; move the SLI to the edge; add alerting or drop the unused one.
- Outcome 2 is also covered by the lab policy and Q04-Q05.

**Workplace evidence:** an SLO or error-budget policy adopted by your team.
