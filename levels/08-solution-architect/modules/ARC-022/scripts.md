# ARC-022 · Cloud architecture frameworks — Lecture scripts

**Video:** 57 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.
Framework note: providers publish their own well-architected frameworks and tools; pillar names and review tooling vary, so verify before recording.

---

## ARC-022-L01 · Well-architected frameworks and their pillars (12 min)
**Goal:** explain the pillars and what each one asks of a design.

**Key points**
- A well-architected framework is a structured set of questions and good practices for judging a design.
- Operational excellence: running, monitoring, and improving the system through automation and learning.
- Security: protecting data and systems, identity, detection, and response.
- Reliability: recovering from failure and meeting availability targets.
- Performance efficiency: using resources well as demand changes.
- Cost optimization: delivering value at the lowest sensible cost.
- Sustainability: reducing the environmental impact of the workload.

**Show:** a six-box grid with one Larkspur question per pillar (for example reliability: "what happens to checkout if one zone fails?").

**Check:** Which pillar covers recovering from failure? *(Reliability.)*

---

## ARC-022-L02 · Running a review (12 min)
**Goal:** run a review that finds real issues.

**Key points**
- Prepare: gather the design, requirements, and owners; agree scope and time.
- Work through each pillar by questions; ask for evidence, not opinions.
- Involve the people who build and operate the system, not only the architect.
- Record findings with context: what, where, why it matters, evidence.
- Treat the review as a conversation and a recurring habit, not an audit.

**Show:** a review sheet: pillar, question, answer, evidence, finding, risk.

**Check:** Why ask for evidence? *(Opinions and plans differ from what is actually built.)*

---

## ARC-022-L03 · Prioritizing findings (10 min)
**Goal:** rank findings by risk and effort so high-risk items come first.

**Key points**
- Rate each finding by likelihood and impact; high risk means high likelihood or severe impact.
- Consider effort and dependencies; quick wins can sit beside big risks.
- Fix high risks first; accept low risks consciously with a named owner.
- Do not start with the easiest or the most numerous findings.
- Show the ranking so stakeholders can challenge it.

**Show:** a risk matrix with likelihood on one axis and impact on the other; findings plotted by ID.

**Check:** Which findings come first? *(The highest risk, not the easiest.)*

---

## ARC-022-L04 · From findings to remediation (8 min)
**Goal:** turn findings into an owned remediation plan.

**Key points**
- Each finding becomes an action with an owner, a date, and a success measure.
- Decide per finding: fix, mitigate, accept (with sign-off), or transfer.
- Track in the same backlog the team uses; review progress regularly.
- Record accepted risks with the person who accepted them.
- Re-review after major changes; the review is not a one-time checkbox.

**Show:** a remediation table: finding, risk, decision, owner, due date, status.

**Check:** What must an accepted risk have? *(A named owner who accepted it, and a review date.)*

---

## ARC-022-L05 · Demo: a well-architected review of Larkspur's design (15 min)
**Goal:** review the complete Larkspur infrastructure design and prepare the lab report.

**Steps**
1. Gather the artifacts from ARC-011 to ARC-021: service-model matrix, target architecture, network design, compute ADRs, storage, data platform, identity, network security, HA/DR, landing zone, cost model.
2. Walk the six pillars with questions and collect evidence.
3. Record findings: for example payment segment lacks egress restrictions (security), no DR test scheduled (reliability), no budget alerts on non-prod (cost).
4. **Planned mistake:** starting with the easiest findings, such as tagging gaps, and leaving the missing DR test for later. Re-rank by risk: the DR test and the egress rules come first.
5. Decide per finding: fix in design, accept with owner, or defer with a date.
6. Produce the review report and remediation plan with owners.

---
