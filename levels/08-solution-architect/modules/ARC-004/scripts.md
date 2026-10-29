# ARC-004 · Architecture frameworks — Lecture scripts

**Video:** 67 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-004-L01 · Why architecture frameworks exist (8 min)
**Goal:** explain what a framework gives and what it does not.

**Key points**
- A framework offers shared vocabulary, a repeatable method, and a checklist of things not to forget.
- It is a toolbox to adapt, not a law to obey.
- Frameworks help large, multi-team organizations stay consistent; small programs need a fraction.
- Value is measured by better decisions, not by documents produced.

**Show:** two Larkspur approaches: "produce all 40 framework artifacts" versus "produce six artifacts that each have a named reader". Compare effort and usefulness.

**Check:** How should success of a framework be judged? *(By the quality of decisions and communication, not artifact count.)*

---

## ARC-004-L02 · TOGAF concepts and the ADM (14 min)
**Goal:** describe TOGAF's purpose and the Architecture Development Method without treating it as a checklist.

**Key points**
- TOGAF is an enterprise architecture framework from The Open Group; verify the current edition before recording.
- The ADM is an iterative cycle: Preliminary, Architecture Vision, Business, Information Systems, Technology, Opportunities and Solutions, Migration Planning, Implementation Governance, Architecture Change Management, with Requirements Management at the center.
- Phases are iterated and scaled; you may revisit or skip depth.
- Other parts: content metamodel, enterprise continuum, architecture repository, guidance for tailoring.

**Show:** the ADM as a circle with requirements in the center. Annotate which phases Larkspur's solution work touches heavily (Vision, Business, Information Systems, Technology, Opportunities, Migration) and which belong mostly to enterprise architecture.

**Check:** Is the ADM a strict waterfall? *(No; it is iterative and meant to be tailored.)*

---

## ARC-004-L03 · Architecture domains and building blocks (10 min)
**Goal:** use the common domains and the idea of building blocks.

**Key points**
- Domains: business, data, application, technology (TOGAF groups data and application as information systems).
- Architecture building blocks (ABBs) describe required capabilities; solution building blocks (SBBs) describe the products or components chosen.
- Baseline (today), target (future), and gap analysis between them.
- The repository stores approved artifacts so others can reuse them.

**Show:** a Larkspur gap table: domain, baseline, target, gap. Example: application, on-premises web shop, commerce platform, replace; data, customer records in CRM and shop, unified customer profile, consolidate.

**Check:** What is the difference between an ABB and an SBB? *(ABB is the required capability; SBB is the chosen implementation.)*

---

## ARC-004-L04 · Viewpoints, views, and concerns (12 min)
**Goal:** tailor diagrams to stakeholder concerns using ISO/IEC/IEEE 42010 ideas.

**Key points**
- A stakeholder has concerns; a viewpoint defines how to address a class of concerns; a view is the result for one system.
- Each view should answer specific questions for specific readers.
- Several views together, kept consistent, describe the architecture (an architecture description).
- Check the current standard text before quoting details.

**Show:** concern-to-view table: CFO (cost and ownership) gets a capability and cost view; store managers (daily work) get a process and device view; security gets a data flow and trust boundary view; engineers get a component view.

**Check:** What is a viewpoint? *(A convention for building views that address a set of stakeholder concerns.)*

---

## ARC-004-L05 · Governance and tailoring (10 min)
**Goal:** place reviews in the delivery process and size the method to the program.

**Key points**
- Governance: who reviews, when, against which principles, with what authority.
- Compliance reviews at defined checkpoints (options, design, pre-go-live) keep rework low.
- Tailor by program size, risk, regulation, and team maturity.
- Rule: no artifact without a named consumer and a decision it supports.

**Show:** a small, medium, large program table showing artifacts and reviews. Larkspur sits at medium-large: context, capability map, options paper, target architecture, decision log, three checkpoints.

**Check:** Why avoid artifacts without consumers? *(They cost effort and go stale without informing any decision.)*

---

## ARC-004-L06 · Demo: tailoring a lightweight framework for the Larkspur program (13 min)
**Goal:** build a tailored method on one page. Prepares `ARC-004-LAB1`.

**Steps**
1. List candidate framework phases and artifacts for the program.
2. For each, name the consumer and the decision it supports; drop those with none.
3. Map stakeholders to views (CFO, stores, security, delivery teams).
4. Place three governance checkpoints with decision-makers.
5. **Planned mistake:** the draft says "produce the full ADM catalog, matrix, and diagram set" and uses TOGAF terms in the sponsor deck. Fix: cut to the six useful artifacts and use plain business language with the sponsor.
6. Record tailoring rationale: size, risk, regulatory context.

**Check:** Who is the audience for framework vocabulary? *(Mainly architects; business stakeholders get plain language.)*
