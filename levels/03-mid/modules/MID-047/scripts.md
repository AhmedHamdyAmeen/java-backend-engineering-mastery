# MID-047 · Observability — Lecture scripts

**Video:** 94 min · **Analogy used throughout:** a hospital patient monitor plus the patient's chart: vital signs (metrics), the nurse's notes (logs), and the path through departments (traces). Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-047-L01 · Monitoring vs observability (8 min)
**Goal:** tell known-problem checks from open-ended investigation.

**Key points**
- Monitoring watches for questions you already know to ask ("is CPU high?").
- Observability lets you ask new questions about a system from the data it emits, without shipping new code.
- Microservices need it: one request crosses many services, and no single log shows the story.
- It is built from telemetry: logs, metrics, traces.

**Show:** a customer says "checkout is slow": which service, which step, which orders?

**Check:** What does observability add to monitoring? *(The ability to investigate unknown problems from existing data.)*

---

## MID-047-L02 · Logs, metrics, traces (10 min)
**Goal:** know which signal answers which question.

**Key points**
- Metrics: numbers over time, cheap, good for "is something wrong and how much?".
- Logs: events with detail, good for "what exactly happened here?".
- Traces: one request's path across services with timing, good for "where is the time spent?".
- Use counters for counts; do not log a line per event to count it.
- Keep metric labels low-cardinality (route, status), never user or order ids.

**Show:** table: question | signal | Shop example.

**Check:** Which signal shows where a request spent its time? *(A trace.)*

---

## MID-047-L03 · OpenTelemetry concepts (12 min)
**Goal:** understand the OpenTelemetry (OTel) model.

**Key points**
- OTel is a vendor-neutral standard and set of libraries for traces, metrics, and logs.
- A trace is a tree of spans; each span has a name, start, duration, attributes, and a parent.
- Context (trace id, span id) is passed between services in headers (W3C `traceparent`).
- The OpenTelemetry Collector receives, processes, and exports telemetry to backends (Jaeger or Tempo for traces).
- Sampling decides which traces are kept; verify defaults and versions before recording.

**Show:** diagram: gateway span → orders span → inventory span, with `traceparent` on each hop.

**Check:** What carries trace context between services? *(Headers such as `traceparent`.)*

---

## MID-047-L04 · Instrumenting Spring services (12 min)
**Goal:** add traces to a Spring Boot service.

**Key points**
- Auto-instrumentation (Java agent or Spring Boot's Micrometer Tracing with an OTel bridge) covers HTTP, JDBC, and Kafka clients. Verify the supported setup for the Boot version in use before recording.
- Manual spans add business steps: "reserve-stock", "charge-payment".
- Add useful attributes (order id as span attribute is fine; as a metric label it is not).
- Configure the exporter endpoint and sampling through properties or environment variables.

**Show:**
```java
Span span = tracer.spanBuilder("reserve-stock").startSpan();
try (Scope s = span.makeCurrent()) { span.setAttribute("order.id", id); inventory.reserve(lines); }
finally { span.end(); }
```

**Check:** When do you need a manual span? *(For a business step the auto-instrumentation cannot see.)*

---

## MID-047-L05 · Context propagation through Kafka (10 min)
**Goal:** keep a trace unbroken across the broker.

**Key points**
- The producer injects trace context into message headers; the consumer extracts it and continues the trace.
- Without this, the trace ends at the broker: a classic gap.
- Consumers often create a span linked to the producer span; async processing may use links rather than parent-child.
- Check both the producer and consumer instrumentation, including batch listeners.

**Show:** headers of an `OrderPlaced` record containing `traceparent`; the consumer span in the same trace.

**Check:** Where do trace headers travel in Kafka? *(In the record headers.)*

---

## MID-047-L06 · Correlating logs and traces (8 min)
**Goal:** find all logs for one request.

**Key points**
- Put `trace_id` and `span_id` in every log line (MDC fields, JSON logs).
- In the tracing tool jump from a span to its logs; in the log tool search by trace id.
- Log structured JSON, not free text.
- Never log secrets or personal data.

**Show:** a JSON log line: `{"level":"WARN","trace_id":"4bf9…","msg":"stock low","sku":"A12"}`.

**Check:** Which id joins a log line to a trace? *(The trace id.)*

---

## MID-047-L07 · Custom metrics with Micrometer (8 min)
**Goal:** expose business metrics.

**Key points**
- Micrometer is Spring's metrics facade; Prometheus scrapes the output.
- Counter (orders placed), timer (checkout duration), gauge (queue size).
- Name by meaning: `shop.orders.placed`, tag by `result` and `channel`.
- High-cardinality labels (customer id) can overload the metrics backend.

**Show:**
```java
Counter.builder("shop.orders").tag("result", "placed").register(registry).increment();
```

**Check:** Why not tag a metric with order id? *(Millions of series overload the backend.)*

---

## MID-047-L08 · Demo: following one order through four services (14 min)
**Goal:** trace one order end to end. Prepares `MID-047-LAB1`.

**Steps**
1. Place an order through the gateway and copy the trace id from the response header or logs.
2. Open the trace in Jaeger/Tempo: gateway, `orders`, `inventory`, `payments`.
3. Search the logs by the same trace id and read the story.
4. **Planned mistake:** the Kafka hop breaks the trace (shipping service shows a separate trace). Add header propagation to the consumer.
5. Show the repaired single trace including the consumer span.
6. Show the business counter for orders placed rising.

---

## MID-047-L09 · Demo: finding a slow span in a saga (12 min)
**Goal:** diagnose slowness using telemetry only. Prepares `MID-047-LAB1`.

**Steps**
1. Start from the symptom: p95 of checkout rose.
2. Pick slow traces; compare with fast ones.
3. Find the widest span: a payment call with retries.
4. **Planned mistake:** blame the database because "it is usually the database"; the trace shows only 5 ms in SQL. Follow the evidence instead.
5. Confirm with the metric of payment retries and the log lines of the same trace.
6. Write a short diagnosis: symptom, evidence, cause, proposed fix.
