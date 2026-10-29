# ARC-006 · Solution architecture lifecycle — Lecture scripts

**Video:** 64 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-006-L01 · The lifecycle at a glance (8 min)
**Goal:** see the whole path from idea to handover and why each stage exists.

**Key points**
- Stages: discovery, options, design, review, delivery support, transition, handover.
- Each stage ends with a decision and a deliverable; no stage is just "work".
- The stages overlap with delivery: design can iterate with build feedback.
- The architect's involvement changes shape, but never ends at design approval.

**Show:** a horizontal chevron diagram of the seven stages with a decision marker at the end of each and a line showing architect effort rising in design and staying moderate through delivery.

**Check:** Where does the architect's work end? *(At handover to owning and operating teams, not at design approval.)*

---

## ARC-006-L02 · Discovery and options (10 min)
**Goal:** define the first two stages and their exit criteria.

**Key points**
- Discovery exit: requirements baseline, constraints, stakeholders, risks, signed off.
- Options: two or three realistic solution shapes compared against requirements and principles.
- Deliverables: options paper with criteria, trade-offs, and a recommendation.
- Exit: sponsor or design authority chooses an option.

**Show:** exit checklist table for Larkspur: baseline signed, principles agreed, three options compared, recommendation, decision recorded with owner and date.

**Check:** What does the options stage deliver? *(A comparison of realistic alternatives with a recommendation for a decision.)*

---

## ARC-006-L03 · Design and review (10 min)
**Goal:** produce enough design to guide delivery and review it effectively.

**Key points**
- Design to the depth the risk requires: high-risk areas in detail, low-risk left to teams.
- Deliverables: target architecture, integration design, data design, security, deployment, decision records.
- Review against requirements, principles, and risks; the reviewer has a name.
- Exit: approved design with recorded conditions.

**Show:** a design review pack contents list and a review outcome sheet: approve, approve with conditions, reject, each with owner and due date.

**Check:** Why design high-risk areas in more depth? *(Mistakes there are costly; low-risk areas can be decided by teams.)*

---

## ARC-006-L04 · Supporting delivery (12 min)
**Goal:** guide teams during build without becoming a bottleneck.

**Key points**
- Design authority: a small group with clear criteria deciding which changes need architect approval.
- Decision log: short records with context, decision, consequences, owner.
- Office hours and embedded time with teams to answer questions fast.
- Track architectural drift and risks; adjust the design with delivery feedback.

**Show:** a two-line policy: teams decide within the guardrails; changes touching an interface, data ownership, or a quality target go to the design authority within two working days.

**Check:** How do you avoid being a bottleneck? *(Set clear guardrails, delegate within them, and keep fast, scheduled access.)*

---

## ARC-006-L05 · Transition and handover (10 min)
**Goal:** move the solution into operation and hand it to its owners.

**Key points**
- Transition: cutover plan, data migration, parallel running, rollback, training.
- Handover pack: architecture overview, runbooks, monitoring, known risks, decision log, contacts.
- Operations and owning teams accept explicitly against agreed criteria.
- Run a short post-go-live review for lessons and open technical debt.

**Show:** handover checklist: documentation, dashboards and alerts, on-call ownership, support model, access, open risks, signed acceptance.

**Check:** What shows a handover is complete? *(Explicit acceptance by the operating teams against agreed criteria.)*

---

## ARC-006-L06 · Demo: planning Larkspur's architecture lifecycle and checkpoints (14 min)
**Goal:** build an architecture work plan with stages, exit criteria, and reviews. Prepares `ARC-006-LAB1`.

**Steps**
1. Take the program plan: phases, milestones, teams, dates.
2. Overlay the seven stages with deliverables and exit criteria per stage.
3. Place reviews and name the decision-maker for each.
4. Define the delivery-support model: design authority, decision log, weekly office hours.
5. **Planned mistake:** the plan puts all design before any build, with the architect leaving after approval. Fix: design the first release in depth, plan feedback loops after release one, and schedule support and handover.
6. Check alignment with the program plan and with the sponsor's dates.

**Check:** What is wrong with designing everything first? *(No delivery feedback; later learning invalidates parts of the design.)*
