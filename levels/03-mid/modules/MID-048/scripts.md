# MID-048 · Monitoring — Lecture scripts

**Video:** 54 min · **Analogy used throughout:** a car dashboard: the warning light should mean "stop and act", and fuel and speed gauges tell you the rest. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-048-L01 · Prometheus model (10 min)
**Goal:** understand how Prometheus collects and stores metrics.

**Key points**
- Prometheus pulls (scrapes) `/metrics` endpoints on a schedule; on Kubernetes it discovers targets automatically.
- Data is time series: a metric name plus labels, with a value per timestamp.
- Types: counter (only goes up), gauge (up and down), histogram (buckets for latency).
- Counters are read with `rate()`, never raw.
- Storage is local and limited in retention; long-term storage is a separate decision.

**Show:** `http_server_requests_seconds_count{route="/orders",status="200"} 10432`.

**Check:** How do you read a counter? *(With `rate()` over a time window.)*

---

## MID-048-L02 · PromQL essentials (12 min)
**Goal:** write the queries dashboards and alerts need.

**Key points**
- Rate: `rate(metric[5m])` is per-second increase.
- Ratio: errors divided by total, both as rates, giving an error percentage.
- Percentile: `histogram_quantile(0.95, sum by (le) (rate(..._bucket[5m])))`.
- Aggregate with `sum by (label)`; keep `le` when using histograms.
- Metric and label names depend on the instrumentation; verify them in the running system before recording.

**Show:**
```
sum(rate(http_server_requests_seconds_count{status=~"5.."}[5m]))
  / sum(rate(http_server_requests_seconds_count[5m]))
```

**Check:** Why keep `le` in the histogram aggregation? *(`histogram_quantile` needs the bucket boundaries.)*

---

## MID-048-L03 · Dashboards: RED and USE (10 min)
**Goal:** build dashboards that answer a question.

**Key points**
- RED for services: Rate, Errors, Duration (percentiles).
- USE for resources: Utilization, Saturation, Errors (CPU, memory, pools, queues).
- One dashboard per service with the same layout, plus a business overview (orders per minute, failures).
- Top row shows health at a glance; details below; link to traces and runbooks.
- A dashboard nobody reads is decoration; delete it.

**Show:** layout: row 1 RED panels, row 2 JVM (heap, GC), row 3 dependencies (DB pool, Kafka lag).

**Check:** What do RED and USE cover? *(RED: services; USE: resources.)*

---

## MID-048-L04 · Alerting that people trust (10 min)
**Goal:** write alerts that are actionable.

**Key points**
- Alert on symptoms users feel (error rate, latency), not on causes (CPU at 80%).
- Every alert needs: what is wrong, impact, first steps, runbook link.
- Use `for:` durations to avoid flapping; route by severity (page versus ticket).
- Group and deduplicate in Alertmanager so one fault gives one alert.
- Review noisy alerts regularly; delete or fix them.

**Show:**
```yaml
- alert: CheckoutHighErrorRate
  expr: checkout_error_ratio > 0.02
  for: 5m
  annotations: { runbook_url: "https://wiki.example/runbooks/checkout-errors" }
```

**Check:** Why not alert on CPU? *(High CPU may harm nobody; users feel errors and latency.)*

---

## MID-048-L05 · Demo: a service dashboard from scratch (12 min)
**Goal:** build the `orders` dashboard and an alert. Prepares `MID-048-LAB1`.

**Steps**
1. Confirm Prometheus scrapes `orders` (targets page).
2. Add RED panels with the queries from L02.
3. Add JVM and DB pool panels (USE).
4. **Planned mistake:** a latency panel using the average; inject slow requests and see nothing. Replace with p95.
5. Create the error-rate alert with a runbook link and test it by injecting errors.
6. Export the dashboard as JSON into Git.
