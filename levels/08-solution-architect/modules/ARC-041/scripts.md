# ARC-041 · Stakeholder management — Lecture scripts

**Video:** 56 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-041-L01 · Stakeholder mapping (10 min)
**Goal:** identify everyone who can shape or block the Larkspur solution and rank them by influence and interest.

**Key points**
- A stakeholder is anyone who decides, pays, builds, operates, secures, or lives with the result: business, engineering, security, operations, vendors, and store staff.
- Map each on two axes: influence (can they stop or change this?) and interest (how much does it affect them?).
- High influence and high interest: manage closely. High influence, low interest: keep satisfied. Low influence, high interest: keep informed.
- The sponsor is one stakeholder, not the map. Quiet, high-influence people (the ERP owner, the security lead) are the ones that surprise projects.
- A map is a working document: it changes when people change roles.

**Show:** a grid for Larkspur: CFO (sponsor), head of e-commerce, head of store operations, CISO, ERP team lead, payment vendor account manager, store managers; each placed in a quadrant with one line on what they want.

**Check:** Which quadrant holds a security lead who rarely attends meetings but can block go-live? *(High influence, lower interest: keep satisfied, and move toward closely managed.)*

---

## ARC-041-L02 · Engagement plans (10 min)
**Goal:** turn the map into a plan that says who gets what, how often, and from whom.

**Key points**
- For each stakeholder write: what they need to know, what we need from them, channel, frequency, and owner.
- Business leaders get outcomes and decisions needed; engineers get contracts and constraints; operations get run impact; vendors get dates and interface changes.
- Engage early on what a group cares about most, before the design is fixed, so feedback is cheap.
- Plan one-to-one time with high-influence skeptics; do not meet them first in a steering group.
- Review the plan monthly and drop engagements that no longer help.

**Show:** an engagement table with columns stakeholder, need from them, message, channel, frequency, owner, with three Larkspur rows filled in (CISO, store operations head, ERP lead).

**Check:** Why meet a skeptical high-influence stakeholder one-to-one before the steering group? *(So concerns surface privately and can be addressed without surprising or embarrassing anyone.)*

---

## ARC-041-L03 · Resolving conflicting requirements (12 min)
**Goal:** resolve conflicts between stakeholders with explicit trade-offs and a named decision owner.

**Key points**
- Conflicts are normal: e-commerce wants fast release, security wants controls, stores want stable tills.
- First restate each need as an underlying goal (speed to market, protect card data, keep stores trading), which often reveals room.
- Lay out options with what each stakeholder gains and gives up; quantify where possible.
- Name the decision owner. The architect facilitates and recommends; the person accountable decides.
- Record the decision, the trade-off accepted, and the review date, e.g. in an ADR.

**Show:** a conflict card: requirement A (release weekly), requirement B (security review per release); options: full review each release, automated checks plus review of risky changes, quarterly review; trade-offs and chosen option with owner.

**Check:** Who decides a stakeholder conflict? *(The accountable decision owner, with the architect facilitating and recording the trade-off.)*

---

## ARC-041-L04 · Keeping alignment over time (10 min)
**Goal:** keep stakeholders aligned as the solution and the organization change.

**Key points**
- Alignment decays: people rotate, priorities shift, and early agreements are forgotten.
- Keep a short decision log visible to all; reopen a decision only with new facts.
- Regular touchpoints (steering, design forums, one-to-ones) with a standing "what changed" item.
- Surface bad news early and with options; late surprises cost trust.
- At each phase boundary, re-check the map and the engagement plan.

**Show:** a monthly alignment cycle for Larkspur: refresh stakeholder map, review decision log, share a one-page status, hold one-to-ones with the three highest-risk stakeholders.

**Check:** When should a settled decision be reopened? *(When new facts or constraints materially change its basis, not because someone dislikes it.)*

---

## ARC-041-L05 · Demo: mediating between store operations and e-commerce (14 min)
**Goal:** work a live conflict session between store operations and e-commerce on the Larkspur case. This prepares ARC-041-LAB1.

**Steps**
1. Set the scene: e-commerce wants click-and-collect orders to reserve stock in store immediately; store operations says the tills and picking staff cannot absorb it before Christmas.
2. Restate goals: e-commerce wants conversion and promise accuracy; operations wants stable stores and fair workload.
3. **Planned mistake:** jump to a technical fix (a nightly stock feed) before agreeing the goals. Operations feels ignored and rejects it. Fix: return to goals and ask for each side's non-negotiables.
4. List options: reserve for all stores now, reserve for ten pilot stores, reserve only for stock above a safety threshold.
5. Compare trade-offs in a small table (conversion gain, store workload, risk, cost) and let the sponsor-named decision owner choose: pilot stores with a threshold.
6. Record the decision, accepted trade-off, owner, and review date in the decision log, and confirm in writing to both heads.

**Check:** What was the planned mistake? *(Proposing a solution before agreeing the underlying goals.)*
