# SRA-006 · Enterprise resilience — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-006-L01 · Resilience at organization scale (10 min)
**Goal:** widen resilience from single services to the whole organization.

**Key points**
- Resilience is the ability to keep delivering the business outcome through failure and to recover quickly.
- At 25 teams, failures cross team lines: shared platforms, shared vendors, shared people.
- Decide what must keep working (checkout, payments) and what may degrade (recommendations).
- Resilience covers tools, people, and processes, not only services.

**Show:** a tiered list of Commerce 2030 capabilities: must survive, should degrade gracefully, may stop, each with recovery targets (agree with the business).

**Check:** Why is service-level resilience not enough at organization scale? *(Failures cross services through shared dependencies, tools, and people.)*

---

## SRA-006-L02 · Regional and provider failure (12 min)
**Goal:** plan for the loss of a region or of a whole provider and decide what must survive.

**Key points**
- Region failures are rare but real; provider-level events include account suspension or control-plane outages.
- Options: multi-region active-passive, active-active, or accept downtime with a tested restore.
- Cost rises quickly; protect only the capabilities whose outage cost justifies it.
- Test the failover; an untested plan is a hope. Include dependencies such as DNS, identity, and CI.

**Show:** a table: scenario (region loss, provider control-plane outage, account lock), affected capabilities, survival design, recovery target, last test date.

**Check:** Why include identity and deployment tooling in a regional failure plan? *(If they fail, you cannot recover or operate the surviving parts.)*

---

## SRA-006-L03 · Chaos engineering as a program (12 min)
**Goal:** run chaos experiments as a managed learning program.

**Key points**
- An experiment states a hypothesis about steady state, injects a fault, and compares the result.
- Control blast radius: small scope, abort criteria, off-peak start, someone on watch.
- Review every experiment: what we learned, what we fix, who owns it.
- A program has a backlog, a cadence, and growing scope from test to production.

**Show:** an experiment card: hypothesis, steady-state metric, fault, blast radius, abort condition, owner, follow-up actions.

**Check:** What makes chaos engineering different from breaking things? *(A hypothesis, controlled blast radius, abort criteria, and learning.)*

---

## SRA-006-L04 · Systemic and correlated risk (12 min)
**Goal:** find risks that sit between teams.

**Key points**
- Correlated failure: one cause hitting many services (shared database, certificate, DNS, vendor).
- Concentration: one team or one person that everything depends on; knowledge silos.
- Find them by mapping dependencies and reading incident histories for common causes.
- Reduce them with redundancy, diversity, decoupling, or shared ownership.

**Show:** a matrix of services against shared dependencies (identity provider, message broker, certificate authority, cloud region, one on-call engineer) with the heaviest columns highlighted.

**Check:** Name two kinds of systemic risk that are not technical components. *(A single team everything depends on; a knowledge silo.)*

---

## SRA-006-L05 · Resilience investment cases (8 min)
**Goal:** present a resilience posture to leadership with prioritized investments.

**Key points**
- Express risk in business terms: revenue per hour, customers affected, regulatory exposure.
- Rank investments by risk reduced per cost; show alternatives, including accepting a risk.
- Show current posture, target posture, and a staged plan with checkpoints.
- Report outcomes later: incidents avoided and recovery times measured.

**Show:** a one-page summary: top five risks with estimated annual loss (assumptions stated), proposed mitigation, cost, and residual risk.

**Check:** How should the top risk be expressed to leadership? *(In business impact, such as revenue lost per hour of outage with stated assumptions.)*

---

## SRA-006-L06 · Demo: a chaos experiment with a hypothesis and abort criteria (15 min)
**Goal:** design and run a safe experiment on a payment dependency; prepares SRA-006-LAB1.

**Steps**
1. Pick the question: does checkout still succeed if the payment provider is slow?
2. Write the hypothesis, steady-state metric (checkout success rate), and fault (added latency).
3. Set blast radius (one percent of traffic or a test cohort), abort criteria, and who watches.
4. Run, observe, and abort if the criterion is hit.
5. **Planned mistake:** start in production at full traffic with no abort condition. Fix: start in a pre-production environment, then a small cohort, with explicit abort conditions.
6. Hold the review: findings (missing timeout), actions, owner, and a repeat date.

---

## SRA-006-L07 · Demo: finding the shared dependency behind three "unrelated" incidents (15 min)
**Goal:** reveal a systemic risk through incident analysis; prepares SRA-006-LAB1.

**Steps**
1. Gather three incident reports from different teams over six months.
2. Build a timeline and dependency view for each; compare causes and triggers.
3. Find the common factor: an internal certificate authority or a shared configuration service.
4. Quantify the impact and the chance of recurrence; list mitigations.
5. **Planned mistake:** treat each incident as isolated and fix each team's symptom. Fix: assign the shared component an owner, add redundancy, and add a fitness function.
6. Present the finding and its investment case to leadership.
