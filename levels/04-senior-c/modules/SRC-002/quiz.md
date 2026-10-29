# SRC-002 · Quality attributes — Quiz

Outcomes: O1 measurable attribute definitions · O2 trade-offs and cost · O3 utility tree · O4 tactics.

**Q01 (O1)** Which statement makes availability measurable? A. "Highly available" B. "As few outages as possible" C. "No downtime ever" D. "99.95% of requests succeed at the load balancer per calendar month"
**Q02 (O1)** Two components in series, each 99.9%, give roughly: A. 99.8% B. 99.95% C. 100% D. 99.9%
**Q03 (O1)** Which is a measure of operability? A. Lines of code B. Time to diagnose a failing dependency C. Number of classes D. Test count
**Q04 (O2)** Adding a read cache to lower latency typically costs: A. Nothing B. Lower availability always C. Possible stale reads and extra invalidation logic D. Fewer deployments
**Q05 (O2)** Why can't every attribute be top priority? A. They trade off and compete for limited budget B. Stakeholders disagree C. Tools forbid it D. It is a convention
**Q06 (O3)** A utility tree's leaves are: A. Team names B. Technologies C. Servers D. Concrete scenarios rated for importance and difficulty
**Q07 (O3)** Which leaves need the most design effort? A. Low importance, low difficulty B. Low importance, high difficulty C. High importance, high difficulty D. High importance, low difficulty
**Q08 (O3)** A stakeholder rates every leaf High. Best response? A. Accept it B. Force-rank with a limited vote budget and ask what to sacrifice first C. Remove the tree D. Pick the ones you like
**Q09 (O4)** Which is an availability tactic? A. Memoization of reports B. Code formatting C. Health checks with automated failover D. Longer variable names
**Q10 (O4)** Besides the tactic itself, what should be recorded? A. Its cost and side effects B. The author's name only C. Nothing D. The vendor

## Answers
Q01 D · Q02 A · Q03 B · Q04 C · Q05 A · Q06 D · Q07 C · Q08 B · Q09 C · Q10 A

## Practical part
Six case exercises `SRC-002-EX01` to `EX06` plus the lab. Pass: quiz at least 8/10, at least five exercises correct, and a utility tree passing review with the top three attributes agreed and justified.
