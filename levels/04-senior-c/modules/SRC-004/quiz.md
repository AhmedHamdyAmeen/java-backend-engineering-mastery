# SRC-004 · Capacity planning — Quiz

Outcomes: O1 forecast to load · O2 estimation · O3 validation and headroom · O4 plan and triggers.

**Q01 (O1)** Why count requests per order? A. Orders are free B. Load is requests and each order produces many C. It simplifies billing D. Kafka needs it
**Q02 (O1)** Sizing from the daily average: A. Is safe B. Cancels peaks C. Hides peaks and under-sizes the system D. Over-sizes by a factor of ten
**Q03 (O1)** A burst factor is: A. Peak second relative to peak-hour average B. A caching ratio C. A retry count D. Replica lag
**Q04 (O2)** 2 million rows a day of 1 KB is about: A. 2 MB/day B. 20 GB/day C. 200 MB/day D. 2 GB/day
**Q05 (O2)** Which multiplier is often forgotten in Kafka storage? A. Replication factor and retention B. Font size C. Consumer name D. Topic count only
**Q06 (O2)** A back-of-the-envelope estimate should: A. Hide assumptions B. Show assumptions and units and give the order of magnitude C. Be precise to four digits D. Skip sanity checks
**Q07 (O3)** The first bottleneck is the component with: A. The most code B. The newest version C. The least headroom at target load D. The most replicas
**Q08 (O3)** N-1 headroom asks: A. Can the remaining nodes handle peak if one fails? B. How old is node 1? C. Is there one node? D. How many nodes minus one are idle?
**Q09 (O4)** A good re-planning trigger is: A. "Review sometime" B. "When someone complains" C. "Peak CPU above 60% for a week" D. "Next year"
**Q10 (O3)** Validating an estimate best uses: A. Load-test data B. Another guess C. Marketing slides D. Vendor claims only

## Answers
Q01 B · Q02 C · Q03 A · Q04 D · Q05 A · Q06 B · Q07 C · Q08 A · Q09 C · Q10 A

## Practical part
Six estimation exercises `SRC-004-EX01` to `EX06` (timed) plus the lab. Pass: quiz at least 8/10, at least five exercises within a factor of 2 of the reference with visible assumptions, and a plan with the first bottleneck named.
