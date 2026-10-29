# MID-065 · Engineering ownership — Lecture scripts

**Video:** 56 min · **Analogy used throughout:** owning a restaurant, not just cooking one dish: you answer for service at night, the bills, the health inspection, and the plan for next year.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-065-L01 · You build it, you run it (8 min)
**Goal:** describe what owning a service means.

**Key points**
- Owning means responsibility for the service in production, not only for the code you wrote.
- Ownership covers on-call, SLOs, dependencies, cost, security updates, and the roadmap.
- The owning team feels the pain of its own failures, which drives better design.
- Ownership is shared and documented: an ownership page with names, contacts, and links.
- "I wrote it" is history; "I answer for it" is ownership.

**Show:** an ownership page outline: purpose, owners, SLOs, dashboards, runbooks, dependencies, cost, risks, debt.

**Check:** Name three things ownership includes beyond code. *(For example on-call, SLOs, dependencies, cost.)*

---

## MID-065-L02 · On-call well (10 min)
**Goal:** run on-call sustainably and effectively.

**Key points**
- Page only on symptoms that need a human now; every page has a runbook.
- Handover: current incidents, recent changes, known risks.
- During incidents: acknowledge, assess impact, mitigate first, investigate later (see MID-050).
- Afterwards: blameless review and action items that actually get scheduled.
- Protect people: rotation size, rest after a bad night, track alert noise and fix it.

**Show:** a weekly on-call report: pages, false alarms, time to acknowledge, top three noisy alerts.

**Check:** What should you do first in an incident, mitigate or find the root cause? *(Mitigate to limit impact.)*

---

## MID-065-L03 · Prioritizing reliability and debt (10 min)
**Goal:** choose between features, reliability, and debt using evidence.

**Key points**
- Use the error budget: budget left allows feature work; budget spent shifts effort to reliability.
- Evidence for debt: incident count, time lost, change failure rate, onboarding pain.
- Express debt as cost and risk: "this costs two days per release" beats "the code is ugly".
- Rank by impact over effort; pick the top few and schedule them, with capacity reserved.
- A debt list that is never prioritized is only a complaint list.

**Show:** a table: item, evidence, cost per month, effort, decision.

**Check:** What does a spent error budget suggest? *(Prioritize reliability work over new features.)*

---

## MID-065-L04 · Production readiness checklist (8 min)
**Goal:** verify readiness before launch.

**Key points**
- Observability: dashboards, alerts tied to SLOs, tracing, structured logs.
- Reliability: timeouts, retries, health probes, graceful shutdown, capacity and load test results.
- Operations: runbooks, rollback tested, on-call owner, backups and restore tested.
- Security: secrets managed, dependencies scanned, authentication and authorization reviewed.
- Data and dependencies: migrations safe, contracts documented, failure of each dependency considered.
- A checklist is a conversation starter; record the exceptions you accept and who accepted them.

**Show:** a checklist table with status, owner, and link to evidence.

**Check:** Why test a restore, not only take a backup? *(A backup that cannot be restored is not protection.)*

---

## MID-065-L05 · Communicating as an owner (8 min)
**Goal:** explain health and trade-offs to non-engineers and other teams.

**Key points**
- Lead with impact and decision needed, then evidence.
- Report health in SLO terms: "99.7% of checkouts succeeded this month; target 99.9%".
- Present trade-offs with options and costs: "Option A ships in two weeks with known risk X".
- Tell dependent teams about changes and incidents early; publish a changelog.
- Say no with data, and offer an alternative.

**Show:** a one-paragraph monthly service health note for product.

**Check:** What should a message to product start with? *(The impact and the decision needed.)*

---

## MID-065-L06 · Demo: a readiness review of the payments service (12 min)
**Goal:** run the checklist against the Shop payments service. Prepares `MID-065-LAB1`.

**Steps**
1. Open the checklist and the payments dashboards, alerts, and runbooks.
2. Walk each section; mark pass, fail, or accepted risk with evidence links.
3. Test one claim: trigger a rollback in staging and time it.
4. **Planned mistake:** marking "backups" as done because the job exists. Fix: perform a restore and record the time taken.
5. Rank the gaps by risk; create work items with owners.
6. Write a summary: ready, ready with accepted risks, or not ready, with reasons.
