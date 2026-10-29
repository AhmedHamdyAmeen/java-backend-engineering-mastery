# SRA-017 · Architectural reviews — Quiz

Outcomes: O1 reviewing for risk, complexity, operability · O2 blocking vs preference · O3 questions that teach · O4 improving the practice.

**Q01 (O1)** Who owns the design decision after a review? A. The reviewer B. The authoring team C. The architecture board D. The manager
**Q02 (O1)** A service writes to its database then publishes an event. Which risk matters most? A. Code style B. Naming C. Event lost if the process crashes between the two steps D. Logging format
**Q03 (O1)** A team proposes a new database technology. Which question is most important? A. Is it popular? B. Who is paged and how is it recovered? C. Is it new? D. Does it have a logo?
**Q04 (O1)** Why does complexity matter in review? A. Each component needs an owner and on-call, which costs the organization B. It is unfashionable C. It slows reviews D. It is hard to draw
**Q05 (O2)** Which is a blocking issue? A. Variable naming B. Library preference C. Alternative of similar value D. No way to detect or recover from data loss
**Q06 (O2)** A blocking comment must include: A. A deadline B. The risk and a path forward C. A name D. A code snippet
**Q07 (O2)** Twenty comments of equal weight make the author: A. Unable to see what must be fixed B. More careful C. Confident D. Faster
**Q08 (O3)** Which is the best teaching question? A. "Why didn't you use outbox?" B. "Is this production ready?" C. "What happens if the write succeeds and the publish fails?" D. "Did anyone review this?"
**Q09 (O3)** After one or two questions the author still misses a serious risk. You should: A. Stay silent B. State the concern directly C. Block the launch without explanation D. Rewrite the design
**Q10 (O4)** Which signal best shows your reviews improve outcomes? A. Number of comments B. Length of reports C. Fewer production issues of the kinds reviews target, and author ratings D. Review meeting attendance

## Answers
Q01 B · Q02 C · Q03 B · Q04 A · Q05 D · Q06 B · Q07 A · Q08 C · Q09 B · Q10 C

## Practical part
Six case exercises `SRA-017-EX01` to `EX06` plus the review round lab. Pass: quiz at least 8/10, and a review-quality rubric from authors in which every review separates blocking issues from preferences and states a path forward.
