# SRA-005 · Multi-region trade-offs — Quiz

Outcomes: O1 availability versus consistency per capability · O2 jurisdiction and residency · O3 cost and complexity · O4 sequencing expansion.

**Q01 (O1)** A new request says "we need multi-region". The best first step is to ask: A. Which cloud B. Which driver, capability, and failure or rule it must meet C. Which database D. How many engineers
**Q02 (O1)** Which capability usually tolerates the most staleness across regions? A. Payments B. Inventory reservation C. Product catalog display D. Seller payouts
**Q03 (O1)** A single global consistency choice is a mistake because: A. It is illegal B. Capabilities differ in the cost of staleness C. Databases forbid it D. It is too simple
**Q04 (O2)** Who determines what a data transfer rule requires? A. The newest engineer B. The cloud vendor C. Legal and compliance partners, with engineering translating it D. The load balancer
**Q05 (O2)** A design response to a local residency rule is: A. Copy all data everywhere B. Ignore it until audited C. Move to one global region D. A regional store for the restricted fields with tokenized references elsewhere
**Q06 (O2)** Before relying on a residency assumption you should: A. Delete the data B. Verify it with compliance C. Encrypt it twice D. Add a region
**Q07 (O3)** Which is an often-missed cost of adding a region? A. On-call and tooling load B. Logo design C. Coffee D. Office space
**Q08 (O3)** An option comparison based only on infrastructure bills: A. Is complete B. Is required by law C. Usually misses staffing and operations cost D. Is about on-call only
**Q09 (O4)** Complexity in an expansion plan should be added: A. Up front for all countries B. Never C. At random D. When a trigger such as regulation, volume, or revenue requires it
**Q10 (O4)** Go/no-go criteria in the plan are used to: A. Decide at each stage whether to proceed based on evidence B. Delay everything C. Replace budgets D. Avoid reporting

## Answers
Q01 B · Q02 C · Q03 B · Q04 C · Q05 D · Q06 B · Q07 A · Q08 C · Q09 D · Q10 A

## Practical part
Six case exercises `SRA-005-EX01` to `EX06` plus the lab, presented as a regional strategy to a role-played legal/compliance advisor. Pass: at least five of six exercises correct, quiz at least 8/10, and a strategy with per-capability decisions, residency mapping, and a costed sequence.
