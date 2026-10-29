# MID-048 · Monitoring — Quiz

Outcomes: O1 Prometheus and PromQL · O2 dashboards (RED and USE) · O3 alerting.

**Q01 (O1)** Prometheus collects metrics by: A. Receiving pushes only B. Reading log files C. Scraping `/metrics` endpoints D. Querying the database
**Q02 (O1)** A counter is read with: A. `rate()` B. Its raw value only C. `min()` D. Nothing
**Q03 (O1)** Which gives an error percentage? A. Errors minus total B. Sum of errors C. Count of labels D. Error rate divided by total rate
**Q04 (O1)** `histogram_quantile(0.95, ...)` returns: A. The 95th request B. The average C. An estimated 95th percentile D. The slowest request
**Q05 (O2)** RED stands for: A. Rate, Errors, Duration B. Read, Execute, Deliver C. Reliability, Efficiency, Delay D. Requests, Events, Data
**Q06 (O2)** USE dashboards cover: A. Users, sessions, events B. Utilization, Saturation, Errors of resources C. Uptime, speed, errors only D. URLs, status, endpoints
**Q07 (O2)** A dashboard nobody reads should be: A. Kept forever B. Made larger C. Duplicated D. Removed or fixed
**Q08 (O3)** Alerts should be based mainly on: A. Symptoms users feel B. Causes such as CPU C. Disk labels D. Team size
**Q09 (O3)** Every actionable alert has: A. A runbook link B. A random id only C. No threshold D. A hidden owner
**Q10 (O3)** The `for:` clause in an alert rule: A. Sets the severity B. Chooses the dashboard C. Requires the condition to hold for a duration D. Sends email

## Answers
Q01 C · Q02 A · Q03 D · Q04 C · Q05 A · Q06 B · Q07 D · Q08 A · Q09 A · Q10 C

## Practical part
Seven exercises `MID-048-EX01` to `EX07` (EX07 is the dashboard and alert review) plus the dashboards lab. Pass: at least five exercises and a lab where an injected fault triggers exactly one actionable alert.
