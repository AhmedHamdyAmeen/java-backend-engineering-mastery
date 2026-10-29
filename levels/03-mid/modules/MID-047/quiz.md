# MID-047 · Observability — Quiz

Outcomes: O1 logs, metrics, traces · O2 OpenTelemetry and propagation · O3 log-trace correlation · O4 custom metrics.

**Q01 (O1)** Which signal shows where a request spent its time across services? A. Trace B. Counter C. Gauge D. Heap dump
**Q02 (O1)** Counting orders is best done with: A. A log line per order B. A trace per order C. A metric counter D. A database scan
**Q03 (O1)** Observability differs from monitoring because it: A. Needs no data B. Replaces all alerts C. Only checks CPU D. Helps investigate unknown problems
**Q04 (O2)** A trace is made of: A. Counters B. Spans C. Log files D. Dashboards
**Q05 (O2)** Trace context between HTTP services travels in: A. The request body B. Cookies only C. Headers such as `traceparent` D. The URL path
**Q06 (O2)** A trace that stops at the broker usually means: A. Kafka is down B. The trace expired C. Spans are too short D. Context was not propagated through message headers
**Q07 (O2)** A manual span is useful for: A. A business step auto-instrumentation cannot see B. Disabling tracing C. Replacing logs D. Changing the sampling rate
**Q08 (O3)** To join logs to traces, each log line needs: A. The user's password B. The host name only C. The trace id D. The thread count
**Q09 (O4)** Which is a safe metric tag? A. Customer id B. Order id C. Email D. Result (`placed` or `failed`)
**Q10 (O4)** Why avoid high-cardinality labels? A. They create too many time series B. They are illegal C. They slow down Java D. They hide traces

## Answers
Q01 A · Q02 C · Q03 D · Q04 B · Q05 C · Q06 D · Q07 A · Q08 C · Q09 D · Q10 A

## Practical part
Seven exercises `MID-047-EX01` to `EX07` (EX07 is the diagnosis from telemetry alone) plus the Traceable Shop lab. Pass: at least five exercises including EX07, and a lab where any order id can be traced end to end.
