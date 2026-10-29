# ARC-035 · Architecture review boards — Lecture scripts

**Video:** 56 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-035-L01 · What review boards are for (10 min)
**Goal:** explain what an ARB is for, so you treat it as a partner and not an obstacle.

**Key points**
- An architecture review board (ARB) checks that a solution fits enterprise principles, standards, risk appetite, and other projects.
- It catches cross-project conflicts a single team cannot see, such as two teams buying overlapping tools.
- Possible outcomes: approved, approved with conditions, deferred, rejected.
- The board decides on evidence in the submission; it is not there to redesign your solution.

**Show:** a one-page flow: submission, pre-read, session, decision, conditions, closure, with the typical time each takes.

**Check:** Name the four typical ARB outcomes. *(Approved, approved with conditions, deferred, rejected.)*

---

## ARC-035-L02 · Preparing a submission (12 min)
**Goal:** prepare a submission that leads to a decision in one session.

**Key points**
- Start with the decision you ask for, then context, the options considered, the recommended solution, and risks.
- Pre-wire: talk to board members with likely concerns (security, data, infrastructure) before the session.
- Send the pre-read in time and keep it short; link the HLD and ADRs for those who want depth.
- Surprising the board is the main mistake; every concern they raise in the room should already be in the document.

**Show:** a submission outline with headings and a pre-wiring checklist listing each member, their likely concern, and the date you spoke.

**Check:** What is pre-wiring? *(Discussing the submission with board members beforehand so the session holds no surprises.)*

---

## ARC-035-L03 · Compliance checks (10 min)
**Goal:** show compliance with principles and standards in a way a board can verify.

**Key points**
- Map each architecture principle and standard to the design element that satisfies it, with a link to evidence.
- Mark each line: compliant, compliant with condition, or non-compliant (exception needed).
- Be honest: a self-assessment that is all green with no evidence loses credibility.
- Evidence can be an ADR, a diagram, a test result, or a policy reference.

**Show:** a compliance table with columns principle or standard, status, design element, evidence link, for Larkspur lines such as "prefer SaaS for non-differentiating capability" and "no direct database access between systems".

**Check:** What makes a compliance table credible? *(Evidence links for each line and honest statuses, not all green.)*

---

## ARC-035-L04 · Exceptions and conditions (10 min)
**Goal:** request design exceptions properly and track board conditions to closure.

**Key points**
- An exception states the standard, why the solution cannot comply, the risk, the mitigation, an owner, and an expiry date.
- No expiry date means a permanent exception by default; set a date or a trigger for revisiting.
- Conditions are commitments: record each with owner, due date, and evidence of closure.
- Report progress on conditions back to the board; ignoring them after approval costs trust.

**Show:** an exception record and a condition tracker, each with owner and date fields and a status column.

**Check:** Why must an exception have an expiry? *(Without one it becomes permanent and the risk is never revisited.)*

---

## ARC-035-L05 · Demo: a Larkspur ARB session with conditions (14 min)
**Goal:** run through a full ARB session with an exception and conditions; prepares ARC-035-LAB1.

**Steps**
1. Prepare the submission: the decision asked, the options considered, the recommended hybrid solution, and the risks.
2. Pre-wire the security and data representatives; record their concerns and add answers to the pre-read.
3. Build the compliance table; mark one honest non-compliance: Larkspur's ERP can only be reached through a legacy file transfer interface, against the "API-first integration" standard.
4. **Planned mistake:** present without an expiry date on the exception. Fix: add mitigation (monitored transfer, reconciliation check), owner, and a date aligned with the ERP upgrade in the roadmap.
5. Run the session; the board grants conditional approval with two conditions (a penetration test before go-live, a retention policy for the analytical copy).
6. Create the condition tracker with owners and dates and plan the progress report to the board.
