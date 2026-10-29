# ARC-042 · Architecture assurance — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-042-L01 · Assurance during delivery (10 min)
**Goal:** explain why architecture work continues after design approval and how to plan assurance checkpoints.

**Key points**
- Approval says the design is sound on paper; assurance checks that what is built matches it and works.
- Place checkpoints at natural points: after the first vertical slice, before each integration goes live, before pilot, before go-live.
- Keep reviews light and regular, aimed at the riskiest decisions (ERP integration, payments, stock accuracy), not every class.
- Review findings are tracked to closure with owners, like ARB conditions.
- The architect is a partner to the delivery team, not an auditor arriving at the end.

**Show:** a delivery timeline for Larkspur phase one with five assurance checkpoints marked, each with its focus and the evidence expected.

**Check:** Why keep reviewing after the design is approved? *(To catch drift and confirm the built system meets the approved design and requirements.)*

---

## ARC-042-L02 · Architecture drift (10 min)
**Goal:** recognise drift from the approved architecture and decide what to do about it.

**Key points**
- Drift is the gap between the approved design and what teams actually build, usually through reasonable local shortcuts.
- Common signs: a service calling the ERP database directly, a new data copy no one approved, a skipped authentication step.
- Detect it with design reviews, code and configuration inspection, dependency checks, and asking teams to show, not tell.
- Not all drift is bad: either bring the build back to the design, or update the design and record a decision.
- Never ignore it: unrecorded drift becomes surprise at go-live.

**Show:** a drift log entry: what was approved (all ERP access via the stock API), what was found (batch job reads ERP tables directly), impact (bypasses validation and rate limits), decision (fix before pilot), owner and date.

**Check:** What are the two valid responses to drift? *(Bring the build back to the design, or consciously change the design and record the decision.)*

---

## ARC-042-L03 · Non-functional testing evidence (12 min)
**Goal:** define what evidence proves each non-functional requirement (NFR) is met.

**Key points**
- Every NFR needs a measurable target and a test that produces evidence: performance, security, resilience, recoverability.
- Performance: load test at peak volume with realistic data, reporting response times against the target.
- Security: penetration test, dependency and configuration scans, and results of fixes.
- Resilience: fail a dependency (ERP down, payment provider slow) and show the system degrades as designed; recovery tested against the RTO/RPO.
- Evidence must be reproducible and tied to a requirement ID, not a verbal "it was fine".

**Show:** an evidence table for Larkspur: requirement (checkout p95 under agreed limit at peak), test (load test with Black Friday volume), evidence (report), owner, status.

**Check:** What makes NFR evidence acceptable? *(It is measured against a stated target, reproducible, and traceable to a requirement.)*

---

## ARC-042-L04 · Operational acceptance and go-live readiness (12 min)
**Goal:** verify the solution can be run, and decide go-live readiness from evidence.

**Key points**
- Operational acceptance checks monitoring, alerting, runbooks, backup and restore, support rota, access, and escalation paths with vendors.
- Verify by doing: restore a backup, trigger an alert, run an incident drill, not by reading a checklist.
- Readiness combines functional results, NFR evidence, operational acceptance, migration and rollback readiness, and open risks.
- Recommend go, conditional go (with named conditions and dates), or no-go; trace each to evidence.
- The business accepts residual risk explicitly; the architect does not hide it.

**Show:** a go-live readiness table: criterion, evidence, status (met, partly, not met), residual risk, owner; with a final recommendation line.

**Check:** What is a conditional go? *(Go-live approved only if named conditions are met by given dates, with an accountable owner.)*

---

## ARC-042-L05 · Demo: finding drift in a delivery team's design (14 min)
**Goal:** review a delivery team's design against the approved Larkspur architecture and report drift. This prepares ARC-042-LAB1.

**Steps**
1. Collect the approved HLD, the relevant ADRs, and the team's current design for order fulfilment.
2. Walk the three risky decisions: ERP access only through the integration layer, payment data never stored by Larkspur, events published for stock changes.
3. **Planned mistake:** review only the team's slide summary and conclude "no drift". Fix: ask for the actual configuration and a sequence trace; the batch job and a cached card-token table appear.
4. Classify each finding: bring back to design (batch job), or change the design with an ADR (cache to speed lookups, with token-only storage).
5. Write the drift log entries with impact, decision, owner, and date; agree timing with the team lead.
6. Feed unresolved items into the go-live readiness view as risks.

**Check:** What was the planned mistake? *(Trusting a summary instead of inspecting actual configuration and flows.)*
