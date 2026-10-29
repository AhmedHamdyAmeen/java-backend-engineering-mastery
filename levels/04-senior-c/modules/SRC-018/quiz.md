# SRC-018 · Security reviews — Quiz

Outcomes: O1 secure design review · O2 authorization boundaries · O3 risk assessment · O4 working with security.

**Q01 (O1)** A design-stage security review is valuable because: A. Changes are cheapest early B. It replaces testing C. It removes the security team D. It is optional paperwork
**Q02 (O1)** STRIDE is: A. A deployment tool B. A set of threat categories to prompt analysis C. A cipher D. A test framework
**Q03 (O1)** A trust boundary is where: A. Code is compiled B. Teams meet C. Data crosses between different levels of trust D. Logs are stored
**Q04 (O2)** Authorization answers: A. Who you are B. How fast you are C. Where you live D. What you may do on which object
**Q05 (O2)** Changing an order ID in a request to see another customer's order tests: A. Latency B. Object-level authorization C. Encryption D. Caching
**Q06 (O2)** An internal endpoint should: A. Trust any caller in the cluster B. Be public C. Authenticate and authorize callers D. Skip logging
**Q07 (O3)** Risk is commonly assessed as: A. Cost times time B. Likelihood times impact C. Size of code D. Number of users
**Q08 (O3)** An accepted risk requires: A. Nothing B. A hidden note C. A lower rating D. A named owner, rationale, and review date
**Q09 (O4)** Working with a security team as a peer means: A. Engaging early with a prepared package B. Avoiding them C. Escalating immediately D. Hiding findings
**Q10 (O1)** Findings without owners tend to: A. Fix themselves B. Remain unresolved C. Raise ratings D. Improve trust

## Answers
Q01 A · Q02 B · Q03 C · Q04 D · Q05 B · Q06 C · Q07 B · Q08 D · Q09 A · Q10 B

## Practical part
Review-quality rubric (SRC-018 assessment) applied to the `SRC-018-LAB1` review. Pass: at least 8/10 on the quiz, a review covering all access paths, rated findings with owners and dates, and acceptance by the peer and the role-played security lead.
