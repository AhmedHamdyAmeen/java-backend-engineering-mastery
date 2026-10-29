# MID-049 · Reliability — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a train timetable promise: "99 of 100 trains on time" is a target, and the late trains you may still afford this month are your budget. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-049-L01 · What reliability means to users (8 min)
**Goal:** define reliability from the user's side.

**Key points**
- A user sees: does it work, is it fast, is the answer right.
- Internal health (CPU, pods running) is not the same as user happiness.
- Reliability has a cost; perfect is impossible and not wanted.
- Different journeys matter differently: checkout over browsing recommendations.

**Show:** a green dashboard of pods while users see failed payments.

**Check:** Why is "all pods running" not reliability? *(Users can still fail or wait; reliability is measured from their experience.)*

---

## MID-049-L02 · SLIs (10 min)
**Goal:** choose indicators that reflect user experience.

**Key points**
- An SLI (service level indicator) is a ratio: good events over valid events.
- Availability: successful requests / all valid requests.
- Latency: requests faster than a threshold (for example 300 ms) / all requests.
- Correctness: orders processed without wrong results / all orders.
- Measure as close to the user as practical (gateway or load balancer, or client), not only inside the service.

**Show:** `good = requests with status < 500 and duration < 0.3 s`; `valid = all requests excluding 4xx caused by clients`.

**Check:** What is the shape of an SLI? *(Good events divided by valid events.)*

---

## MID-049-L03 · SLOs and error budgets (12 min)
**Goal:** set targets and compute the budget.

**Key points**
- An SLO is a target for an SLI over a window: 99.9% of checkouts succeed over 30 days.
- Error budget = 100% minus the SLO: 0.1% of requests may fail.
- 99.9% over 30 days is about 43 minutes of full outage equivalent; verify the arithmetic when recording.
- Never 100%: it is unaffordable and blocks all change.
- Set targets from user needs and history, and agree with the product owner.

**Show:** budget table: 99% → ~7.2 h, 99.9% → ~43 min, 99.99% → ~4.3 min per 30 days.

**Check:** What is the error budget of a 99.5% SLO? *(0.5% of requests, or time, in the window.)*

---

## MID-049-L04 · Burn-rate alerts (10 min)
**Goal:** alert when the budget is being consumed too fast.

**Key points**
- Burn rate = observed error rate / allowed error rate. Burn rate 1 uses the budget exactly over the window.
- A high burn rate over a short window pages (for example 14x over 1 h with a 5 min confirmation); a lower burn over a longer window creates a ticket (for example 6x over 6 h).
- Pairing a long and a short window reduces false alarms and speeds up recovery detection.
- Exact thresholds are a team choice; check against a current SRE reference before recording.

**Show:**
```
(error_ratio_1h > 14 * 0.001) and (error_ratio_5m > 14 * 0.001)
```

**Check:** What does burn rate 1 mean? *(The budget is used up exactly at the end of the window.)*

---

## MID-049-L05 · Using the budget (8 min)
**Goal:** let the budget guide decisions.

**Key points**
- Budget left: ship features faster, take more risk.
- Budget nearly spent: slow releases, fix reliability first, freeze risky changes.
- The policy is agreed in advance and written down.
- Review SLOs periodically; they change with the product.
- Budgets make the trade-off between features and reliability a shared, factual one.

**Show:** a policy table: budget above 50%, 10-50%, below 10%, with actions.

**Check:** What happens when the budget is nearly spent? *(Slow risky releases and prioritize reliability work.)*

---

## MID-049-L06 · Demo: SLO dashboard and burn-rate alert for checkout (12 min)
**Goal:** implement a checkout SLO end to end. Prepares `MID-049-LAB1`.

**Steps**
1. Define the SLI from the gateway metrics: checkout requests with status < 500, valid excluding 4xx.
2. Add recording rules for the ratio over 5 m, 1 h, and 30 d.
3. Build the dashboard: SLO, remaining budget, burn rate.
4. **Planned mistake:** measure the SLI only inside `orders`; requests failing at the gateway are missing. Move the measurement to the gateway.
5. Add the two-window burn-rate alerts with runbook links.
6. Inject errors and watch the alert fire.
