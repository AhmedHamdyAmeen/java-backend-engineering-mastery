# SRB-009 · Service mesh — Quiz

Outcomes: O1 mesh capabilities · O2 mTLS and canary · O3 adopt or reject.

**Q01 (O1)** A service mesh primarily moves which concerns? A. Networking concerns out of app code B. Business rules C. Database schemas D. UI code
**Q02 (O1)** The control plane: A. Runs business logic B. Stores orders C. Distributes config and certificates D. Replaces DNS
**Q03 (O1)** Sidecar-less meshes aim to: A. Remove mTLS B. Reduce per-pod overhead C. Replace Kubernetes D. Eliminate proxies entirely
**Q04 (O2)** mTLS authenticates: A. Only the server B. Only the client C. Neither D. Both client and server
**Q05 (O2)** Workload identity is preferred over IPs because: A. IPs are encrypted B. IPs are shorter C. Pods move and IPs are reused D. DNS is faster
**Q06 (O2)** A canary split sends: A. A small share to the new version B. All traffic C. No traffic D. Only admin traffic
**Q07 (O3)** Duplicate retries in mesh and code cause: A. Lower load B. Better caching C. Exactly-once D. Retry amplification
**Q08 (O3)** A mesh is a poor fix for: A. mTLS needs B. Problems of process C. Polyglot telemetry D. Canary routing
**Q09 (O3)** Evidence for adoption should come from: A. A vendor slide B. A blog post only C. A measured trial D. Team votes only
**Q10 (O1)** Policies should be: A. Edited live B. Hidden C. Written once D. Code reviewed and tested in audit mode

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
ADR defense: present the lab ADR and defend its measurements. Pass: 70% on the quiz and an ADR citing measured latency and effort.
