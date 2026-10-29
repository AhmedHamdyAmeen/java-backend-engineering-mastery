# ARC-019 · High availability and DR — Quiz

Outcomes: O1 RPO and RTO · O2 multi-AZ and DR patterns · O3 dependencies · O4 DR testing.

**Q01 (O1)** RPO is: A. How long recovery takes B. The cost of recovery C. How much recent data may be lost D. The number of regions
**Q02 (O1)** RTO is: A. The maximum acceptable time to restore service B. Data loss tolerance C. Backup frequency D. The retention period
**Q03 (O1)** Why set targets per capability? A. Regulations forbid one target B. Checkout and reporting have different impact and cost C. It is easier D. Cloud requires it
**Q04 (O2)** The cheapest and slowest DR pattern is: A. Active-active B. Warm standby C. Pilot light D. Backup-restore
**Q05 (O2)** Warm standby means: A. A scaled-down full copy running in another location B. Only backups C. Two full active regions D. Nothing is running
**Q06 (O2)** Multi-AZ design should size so that: A. Losing one zone still leaves enough capacity B. Each zone is idle C. One zone carries nothing D. Capacity is minimal
**Q07 (O3)** A DR plan that ignores the ERP and payment provider: A. Is complete B. Is cheaper and sound C. Depends on them recovering with no fallback D. Needs no testing
**Q08 (O3)** A good degraded mode for stores is: A. Closing all stores B. Selling offline with limits and reconciling after C. Cash only forever D. Ignoring the outage
**Q09 (O4)** Evidence that a DR plan works is: A. A signed document B. A diagram C. A vendor claim D. Measured results from tests against targets
**Q10 (O4)** DR tests should be repeated: A. Never B. On a schedule and after major changes C. Only after disasters D. Only once at launch

## Answers
Q01 C · Q02 A · Q03 B · Q04 D · Q05 A · Q06 A · Q07 C · Q08 B · Q09 D · Q10 B

## Practical part
HA/DR design defense using the `ARC-019-LAB1` design, the costed options, and exercises `ARC-019-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and targets met at an accepted cost or the trade-off escalated.
