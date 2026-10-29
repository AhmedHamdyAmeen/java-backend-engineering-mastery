# MID-046 · Performance testing — Lecture scripts

**Video:** 64 min · **Analogy used throughout:** stress-testing a bridge: normal traffic, a rush hour, a sudden crowd, and a week of steady use each reveal different cracks. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-046-L01 · Kinds of performance tests (10 min)
**Goal:** pick the right test for the question.

**Key points**
- Load: expected traffic; does it meet the latency and error targets?
- Stress: grow beyond capacity; where and how does it break, and does it recover?
- Spike: a sudden jump (a flash sale); do queues, pools, and autoscaling cope?
- Soak: moderate load for hours; reveals leaks, slow growth, and resource exhaustion.
- Define a pass criterion (for example p95 below 300 ms, errors below 0.1%) before running.

**Show:** four load-over-time shapes (flat, ramp up, sharp jump, long flat).

**Check:** Which test finds a memory leak? *(A soak test.)*

---

## MID-046-L02 · Writing k6 scenarios (12 min)
**Goal:** script a realistic user journey in k6.

**Key points**
- k6 scripts are JavaScript: `options` (load shape, thresholds) and a default function (one user iteration).
- Use checks for correctness and thresholds for pass or fail.
- Add think time (`sleep`) between steps; real users pause.
- Parametrize data (users, SKUs) so caches are not unrealistically warm.
- Run the load generator on a separate machine from the system under test. Verify tool version before recording; Gatling is an alternative.

**Show:**
```javascript
export const options = { thresholds: { http_req_duration: ['p(95)<300'], http_req_failed: ['rate<0.001'] } };
export default function () {
  http.get(`${BASE}/products?q=${pick(terms)}`); sleep(2);
  http.post(`${BASE}/cart`, JSON.stringify({sku: pick(skus), qty: 1}), params); sleep(3);
}
```

**Check:** What does a threshold do? *(Fails the run when a metric violates the limit.)*

---

## MID-046-L03 · Workload models (10 min)
**Goal:** make the test resemble production.

**Key points**
- Traffic mix: for Shop, mostly browse and search, fewer carts, even fewer checkouts; take ratios from production logs.
- Closed model (fixed number of users waiting for responses) versus open model (arrivals at a fixed rate regardless of response time).
- Open models fit public web traffic; closed models hide overload because slow responses reduce arrival rate.
- Realistic data: large catalog, varied users, realistic cart sizes.

**Show:** table of Shop's journeys with percent share and arrival rate, plus k6 executor `constant-arrival-rate`.

**Check:** Why is an open model better for web traffic? *(Users keep arriving even when the system is slow.)*

---

## MID-046-L04 · Percentiles and coordinated omission (10 min)
**Goal:** report latency honestly.

**Key points**
- Averages hide the slow tail; report p50, p95, p99 and the max, plus throughput and error rate.
- Percentiles cannot be averaged across machines; combine histograms.
- Coordinated omission: a closed-loop tool that waits for a slow response stops sending, so it records fewer slow samples and the result looks better than reality.
- Use arrival-rate (open) executors or tools that correct for it; state the method in the report.

**Show:** a stall of 10 seconds: a closed loop records one slow request, an open model records every request that should have been sent.

**Check:** Why is average latency a poor report? *(It hides the slow requests users actually feel.)*

---

## MID-046-L05 · From test result to bottleneck (10 min)
**Goal:** find the first bottleneck with evidence.

**Key points**
- Look at latency against load: where does the curve bend?
- Correlate with metrics: CPU, GC pauses, connection pool wait, DB query time, thread pool queues.
- Use profiles (flame graphs) and traces on the slow path.
- Change one thing at a time and retest.
- Name the first bottleneck; the next one only appears after you fix it.

**Show:** timeline: p95 rises at 400 req/s; the DB connection pool wait metric rises at the same time.

**Check:** Why change one thing at a time? *(Otherwise you cannot tell which change helped.)*

---

## MID-046-L06 · Demo: a soak test that finds a slow leak (12 min)
**Goal:** find a slow resource leak with a soak. Prepares `MID-046-LAB1`.

**Steps**
1. Run a 20-minute load test of checkout: green.
2. Start the soak at moderate load and open heap and GC dashboards.
3. **Planned mistake:** judge success from the first 20 minutes; at hour one old-generation memory keeps climbing and GC pauses grow.
4. Take a heap dump or profile; find the growing cache or unclosed resource.
5. Fix it, rerun the soak, and show flat memory.
6. Write the finding with graphs and the evidence chain.
