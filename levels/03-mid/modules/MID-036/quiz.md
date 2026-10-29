# MID-036 · Service discovery — Quiz

Outcomes: O1 discovery and balancing styles · O2 DNS-based discovery · O3 health-driven routing and deployments.

**Q01 (O1)** In client-side discovery, who picks the instance? A. A hardware switch B. The caller C. DNS only D. The database
**Q02 (O1)** Which is server-side discovery? A. Caller reading a registry B. Hard-coded IP C. A Kubernetes Service in front of Pods D. A local config list
**Q03 (O1)** Least-connections balancing suits: A. Uniform tiny requests only B. Requests with widely varying durations C. No traffic D. Sticky sessions
**Q04 (O2)** In Docker Compose, services reach each other by: A. Host IP only B. Random ports C. Container ids D. Service name through the Compose network DNS
**Q05 (O2)** Why can balancing look uneven with keep-alive connections? A. DNS is disabled B. Pooled connections stay on one replica C. Replicas are identical D. TLS fails
**Q06 (O2)** A hard-coded replica IP: A. Survives restarts B. Improves balancing C. Breaks when that instance changes or dies D. Is required by Compose
**Q07 (O3)** A readiness probe decides: A. Whether an instance receives traffic B. The JVM heap C. The log format D. The DNS TTL
**Q08 (O3)** When a replica is killed during load, errors are mostly: A. None, ever B. In every request C. Only for new connections D. In requests in flight on that replica
**Q09 (O3)** Graceful shutdown helps by: A. Letting in-flight requests complete before exit B. Skipping health checks C. Increasing latency D. Hiding errors
**Q10 (O3)** On a platform that already provides discovery, adding a registry is: A. Always required B. Usually unnecessary extra moving parts C. Faster than DNS D. Needed for TLS

## Answers
Q01 B · Q02 C · Q03 B · Q04 D · Q05 B · Q06 C · Q07 A · Q08 D · Q09 A · Q10 B

## Practical part
Six exercises `MID-036-EX01` to `EX06` plus `MID-036-LAB1`. Pass: at least five exercises, 8 of 10 quiz answers, and a lab run with errors limited to in-flight requests and a correct explanation.
