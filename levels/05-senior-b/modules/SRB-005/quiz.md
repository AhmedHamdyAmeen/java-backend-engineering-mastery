# SRB-005 · High-availability design — Quiz

Outcomes: O1 redundancy and SPOFs · O2 shedding · O3 fault containment · O4 availability math.

**Q01 (O4)** Two 99.9% serial services give about: A. 99.8% B. 99.9% C. 99.99% D. 100%
**Q02 (O4)** Parallel redundancy math assumes: A. Shared failures B. No traffic C. Independent failures D. One data center
**Q03 (O4)** Dependencies cap availability because: A. They add redundancy B. Hard dependencies multiply downtime C. They reduce latency D. They remove deploys
**Q04 (O1)** A hidden SPOF could be: A. A second replica B. A load balancer pair C. A tested failover D. An expiring certificate
**Q05 (O1)** Redundancy that is never tested: A. Is always safe B. Is free C. May fail when needed D. Is faster
**Q06 (O2)** Load shedding should drop first: A. Low-priority traffic B. Paying customers C. Payment confirmations D. Admins
**Q07 (O2)** Admission control means: A. Retrying forever B. Queueing without limit C. Ignoring overload D. Rejecting excess work early
**Q08 (O3)** A cell is: A. A single table B. A complete stack serving part of customers C. A cache D. A team
**Q09 (O3)** Cells mainly limit: A. Disk usage B. Test time C. Blast radius D. License costs
**Q10 (O3)** Shuffle sharding reduces: A. Number of workers B. Latency to zero C. Need for monitoring D. Overlap between clients' workers

## Answers
Q01 A · Q02 C · Q03 B · Q04 D · Q05 C · Q06 A · Q07 D · Q08 B · Q09 C · Q10 D

## Practical part
Availability calculation problems (series, parallel, fallback) plus the lab's experiment evidence. Pass: 70% on the quiz and correct math in the lab.
