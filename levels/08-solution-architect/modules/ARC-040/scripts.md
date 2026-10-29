# ARC-040 · Vendor and procurement — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-040-L01 · The procurement process (10 min)
**Goal:** understand procurement stages and the architect's role in each.

**Key points**
- Typical stages: need and requirements, market scan (RFI), formal request (RFP), evaluation, negotiation, contract, onboarding.
- Procurement owns the commercial process and fairness; legal owns contract terms; the architect advises on technical needs and risk.
- Fairness rules matter: the same information and criteria for all vendors, documented decisions.
- Involve the architect before the RFP is written, not after.

**Show:** a swimlane of stages with lanes for business, procurement, legal, architect, vendor; mark architect inputs.

**Check:** What is the architect's role in procurement? *(Technical advisor: requirements, evaluation, and architectural risk in terms.)*

---

## ARC-040-L02 · RFIs and RFPs (12 min)
**Goal:** write the technical sections of an RFI and an RFP.

**Key points**
- RFI: explore the market and ask what exists; RFP: ask vendors to commit to meeting stated needs with prices.
- Describe needs and outcomes, not a product: "support 120 stores offline for four hours", not "must use product X".
- Sections: context, functional needs, non-functional needs (availability, security, data), integration, exit, support, pricing structure.
- Mark requirements mandatory or desirable and say how they are scored.
- Ask for evidence: references, certifications, architecture documents (verify the certification names relevant to the case).

**Show:** a requirement table: ID, need, mandatory or desirable, weight, evidence requested, link to the business case.

**Check:** What is wrong with "must be built on product X"? *(It describes a product, narrows the market, and hides the real need.)*

---

## ARC-040-L03 · Technical evaluation (12 min)
**Goal:** design a technical evaluation with coverage, demos, proof of concept, and references.

**Key points**
- Fix the scorecard and weights before reading responses.
- Layers: written coverage of requirements, scripted demos against Larkspur scenarios, proof of concept for the riskiest unknowns, reference calls.
- Scripted demos stop vendors from showing only their strengths.
- Evidence beats claims: score what was shown, not what was promised.
- Record scores with notes so the decision can be explained and defended.

**Show:** a scorecard: requirement, weight, vendor A score, vendor B score, evidence, notes; plus a demo script of five Larkspur scenarios.

**Check:** Why set weights before reading responses? *(Otherwise criteria drift toward a favorite.)*

---

## ARC-040-L04 · SLAs and contracts from an architect's view (10 min)
**Goal:** review SLAs and contract terms for architectural risk.

**Key points**
- Availability: what is measured, how, exclusions, credits versus real remedy.
- Data: ownership, return format and time on exit, deletion, location, sub-processors.
- Exit: termination rights, transition support, escrow or portability where relevant.
- Support: response and resolution times, hours, escalation; limits and caps on liability are for legal but the architect flags impact.
- Roadmap and change: notice for deprecations, price uplifts, API changes.

**Show:** a contract review table: clause, risk, effect on architecture, ask to procurement or legal.

**Check:** What does a 99.9 percent SLA with service credits not give you? *(Your revenue back; credits are usually small compared with business loss.)*

---

## ARC-040-L05 · Demo: scoring two vendor RFP responses (14 min)
**Goal:** worked scoring of two commerce-platform responses; prepares ARC-040-LAB1.

**Steps**
1. Start from the agreed scorecard with mandatory and weighted requirements.
2. Score vendor A and vendor B per requirement from the written answers, citing the evidence.
3. Flag claims without evidence for demo or proof of concept; note exit and data-return terms.
4. **Planned mistake:** score the glossy demo impression and let the incumbent's relationship colour the marks. Fix: score only against stated evidence, have two scorers, and discuss differences.
5. Total with weights, run sensitivity on the top two weights, and write the recommendation with open risks.
