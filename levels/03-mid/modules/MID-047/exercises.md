# MID-047 · Observability — Exercises and lab

## Lab
### MID-047-LAB1 · Traceable Shop
**Outcomes:** 1–4 · **Time:** ~3.5 h
Instrument gateway, services, and Kafka so traces appear in Jaeger or Tempo; add trace ids to logs; add business metrics for orders placed and failed.
**Acceptance:** any order ID can be traced end to end.

## Exercises (assessment: diagnose an issue from telemetry alone)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-047-EX01 | 1 | For five questions (error count, request path, exact exception, time per step, slow tail), name the signal that answers it. |
| MID-047-EX02 | 2 | Enable auto-instrumentation for `orders` and view a trace in Jaeger or Tempo. |
| MID-047-EX03 | 2 | Add a manual span "reserve-stock" with an `order.id` attribute. |
| MID-047-EX04 | 2 | Propagate trace context through Kafka and show one trace across producer and consumer. |
| MID-047-EX05 | 3 | Add `trace_id` and `span_id` to JSON logs; find all logs of one request. |
| MID-047-EX06 | 4 | Add a counter `shop.orders` tagged `result`; explain why `customerId` must not be a tag. |
| MID-047-EX07 | 1–4 | Given screenshots of traces, logs, and metrics from a slow-checkout incident, write a diagnosis with evidence. |

## Solutions
- **EX01** Counts: metric; path: trace; exact exception: log; time per step: trace; slow tail: metric histogram or percentile.
- **EX02** Run the OTel Java agent or the Micrometer Tracing bridge with an exporter to the collector; verify the supported setup for the Boot version.
- **EX03** `tracer.spanBuilder(...)` with `makeCurrent()` and `end()` in `finally`, as in the lecture.
- **EX04** Use the instrumented Kafka client or Spring Kafka observation support so headers carry `traceparent`; check the consumer span's trace id equals the producer's.
- **EX05** Add trace and span ids to the MDC through the tracing bridge and a JSON encoder; search by trace id.
- **EX06** `Counter.builder("shop.orders").tag("result","failed")`; customer id yields unbounded series.
- **EX07** Pattern: symptom (metric), narrowing (traces), cause (widest span), confirmation (logs); propose one fix.

**Outcome 1** is also checked by quiz Q01-Q03.
