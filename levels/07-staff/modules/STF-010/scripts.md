# STF-010 · Technical due diligence — Lecture scripts

**Video:** 96 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-010-L01 · When due diligence is needed (10 min)
**Goal:** recognize the situations that call for an outside technical assessment.

**Key points**
- Acquisitions, major vendor selection, partnerships, and internal modernization decisions.
- The question is: what are we buying or depending on, and what will it cost to own?
- Time is short and access is limited; plan for that.
- The output is a decision input, not a perfect audit.

**Show:** a list of four triggers with the decision each supports: acquire, select a vendor, rely on a partner, modernize a legacy system.

**Check:** What is the output of due diligence for? *(To inform a decision with known risks and costs.)*

---

## STF-010-L02 · Assessing architecture and code health (12 min)
**Goal:** judge structure and code quality fast, focusing on risk.

**Key points**
- Review architecture docs, deployment layout, data stores, and integrations.
- Sample the repository: tests, dependency age, build time, change history.
- Look for risk signals: no tests, single points of failure, unsupported versions.
- Do not judge style; judge what makes change slow or dangerous.

**Show:** a checklist: structure, coupling, test coverage and quality, dependency health, build reproducibility, with a rating scale per item.

**Check:** Why avoid judging style? *(Style rarely drives risk; slow, unsafe change does.)*

---

## STF-010-L03 · Assessing operations and security (12 min)
**Goal:** judge how safely the system runs and protects data.

**Key points**
- Operations: monitoring, incident history, deploy practice, backups and recovery tests.
- Security: access control, secrets handling, patching, data protection, past breaches.
- Ask for evidence: incident reports, restore test results, scan outputs.
- Check compliance for payments and personal data where relevant.

**Show:** a table of evidence requests: last three incidents, backup restore test, access list, vulnerability scan, certifications.

**Check:** Why ask for a restore test result? *(Backups that were never restored may not work.)*

---

## STF-010-L04 · Assessing team capability and key-person risk (12 min)
**Goal:** judge the people side that often decides the outcome.

**Key points**
- Interview engineers and leads about decisions, incidents, and how work flows.
- Key-person risk: knowledge held by one or two people, unwritten processes.
- Look at retention, hiring, and culture of quality.
- Treat interviews respectfully; people's futures may depend on the result.

**Show:** a question list: who can deploy, who understands payments reconciliation, what happens when X is away.

**Check:** What is key-person risk? *(Critical knowledge or access held by too few people.)*

---

## STF-010-L05 · Risk severity and remediation cost (10 min)
**Goal:** separate deal-breakers from fixable debt and cost the fixes.

**Key points**
- Severity: likelihood, impact, and how soon it bites.
- Deal-breakers: unfixable or too costly problems, for example unlicensed core code or an architecture that cannot meet scale.
- Fixable debt: estimate effort in engineer-months with a range.
- State confidence in each estimate.

**Show:** a risk register: risk, severity, evidence, remediation, cost range, confidence.

**Check:** What makes a finding a deal-breaker? *(It cannot be fixed within acceptable cost or time, or it changes the value of the deal.)*

---

## STF-010-L06 · Writing the report (10 min)
**Goal:** write a report decision-makers can use.

**Key points**
- Start with a summary and a recommendation, then evidence.
- Rank risks and show costs and conditions.
- Mark what you could not verify.
- Keep it short; attach details as appendices.

**Show:** a report outline: summary, recommendation with conditions, top risks, remediation plan, unknowns, appendices.

**Check:** Why mark what you could not verify? *(Readers must know the limits of the evidence.)*

---

## STF-010-L07 · Demo: a two-week due diligence of an acquisition target (15 min)
**Goal:** plan and run a time-boxed assessment; prepares STF-010-LAB1.

**Steps**
1. Day 1: agree scope and questions with the deal team and request documents.
2. Days 2-5: review architecture, sample the repository, read incident history.
3. Days 6-9: interview engineers and check security and operations evidence.
4. **Planned mistake:** spending the whole time on code style. Fix: use the risk checklist and spend time on payments flow, data protection, and key people.
5. Days 10-12: build the risk register with costs; days 13-14: write the report.

---

## STF-010-L08 · Demo: presenting findings to a deal team (15 min)
**Goal:** present a due-diligence report and defend its conclusions; prepares STF-010-LAB1.

**Steps**
1. Lead with the recommendation and the top three risks.
2. Show cost ranges and conditions to proceed.
3. Anticipate challenges: how sure are you, what if you are wrong, what would change the answer.
4. **Planned mistake:** hiding uncertainty to sound confident. Fix: state confidence and unknowns, and say what extra access would reduce them.
5. Agree follow-ups: further checks, price or term adjustments, integration plan.
