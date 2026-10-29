# SRC-003 · Architecture trade-offs — Quiz

Outcomes: O1 one-way and two-way doors · O2 lightweight evaluation · O3 complexity as cost · O4 trade-offs in ADRs.

**Q01 (O1)** Which decision is most like a one-way door? A. Choosing a logging format B. Renaming an internal class C. Changing a pool size D. Choosing a shard key for the order data
**Q02 (O1)** A common failure is: A. Deciding reversible things fast B. Deciding irreversible things quickly and reversible ones slowly C. Using feature flags D. Writing ADRs
**Q03 (O1)** Which makes a door easier to reverse? A. Bigger releases B. Skipping tests C. Expand-and-contract migrations and feature flags D. Fewer reviews
**Q04 (O2)** In a lightweight ATAM-style review you walk through: A. Only the code B. The team's calendar C. The vendor list D. High-priority scenarios for each option
**Q05 (O2)** The best input to an architecture evaluation is: A. The utility tree B. Personal preference C. The newest technology D. The cheapest estimate
**Q06 (O3)** Operational burden belongs in a comparison because: A. It is cheap B. The team runs the system for years C. It never changes D. Vendors say so
**Q07 (O3)** A weak reason for an abstraction layer is: A. A stable boundary B. Two real implementations needed now C. "We might switch databases someday" D. Enforcing module ownership
**Q08 (O4)** A decision that improves one attribute and hurts another is a: A. Trade-off point B. Sensitivity point C. Risk register D. Constraint
**Q09 (O4)** A parameter whose value strongly changes an attribute (for example replica lag) is a: A. Trade-off point B. Constraint C. Sensitivity point D. Assumption
**Q10 (O2)** A rejected option in an ADR should be described: A. Briefly and negatively B. Omitted C. As a strawman D. With its honest strengths and why it lost

## Answers
Q01 D · Q02 B · Q03 C · Q04 D · Q05 A · Q06 B · Q07 C · Q08 A · Q09 C · Q10 D

## Practical part
Six case exercises `SRC-003-EX01` to `EX06` plus the lab. Pass: quiz at least 8/10, at least five exercises correct, and an ADR defended against assessor challenges with honest rejected options.
