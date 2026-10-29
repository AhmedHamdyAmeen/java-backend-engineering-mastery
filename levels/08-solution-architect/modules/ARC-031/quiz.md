# ARC-031 · Resilience architecture — Quiz

Outcomes: O1 failure scenarios · O2 fault isolation and degradation · O3 business continuity · O4 resilience tests.

**Q01 (O1)** Resilience for an enterprise solution should start from: A. Critical business processes and their dependencies B. Server counts C. Cloud region names D. Vendor brochures
**Q02 (O1)** The ERP has weekly maintenance windows. The catalog should: A. Ignore it B. Treat it as a scenario with impact and response C. Assume it never overruns D. Move the ERP to the cloud
**Q03 (O1)** A slow dependency is often more dangerous than a dead one because: A. Slowness exhausts threads and queues B. It is cheaper C. It is easier to detect D. It never recovers
**Q04 (O2)** A bulkhead is: A. A caching layer B. A deployment tool C. A retry loop D. A separate resource pool so one failing dependency cannot consume everything
**Q05 (O2)** A degraded mode is: A. A full outage B. A reduced but working behavior while a dependency is down C. A performance test D. A security setting
**Q06 (O2)** The ERP is down; the platform should preferably: A. Stop taking orders B. Delete the queue C. Accept orders, queue postings, and replay later D. Ask customers to call
**Q07 (O3)** A store continuity plan must include: A. Only server restart steps B. Offline procedure, limits, owner, and reconnection reconciliation C. Marketing text D. Vendor names only
**Q08 (O3)** Offline sales replayed after reconnection require: A. Idempotent sale IDs to avoid duplicates B. Manual retyping C. Deleting the queue D. Bigger screens
**Q09 (O4)** A resilience test for payment failover should: A. Only be reviewed on paper B. Inject the failure and measure switch time and duplicate charges C. Wait for a real outage D. Be run once at design time
**Q10 (O4)** A critical process without a documented degraded mode: A. Is acceptable B. Has no dependencies C. Is a gap against the lab acceptance D. Is automatically resilient

## Answers
Q01 A · Q02 B · Q03 A · Q04 D · Q05 B · Q06 C · Q07 B · Q08 A · Q09 B · Q10 C

## Practical part
Scenario walkthrough with the assessor over the lab catalog and continuity plans plus exercises `ARC-031-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab where every critical business process has a documented degraded mode.
