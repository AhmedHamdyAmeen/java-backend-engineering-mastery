# ARC-028 · Security architecture — Lecture scripts

**Video:** 71 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-028-L01 · Security architecture for whole solutions (10 min)
**Goal:** explain what security architecture adds beyond securing each component.

**Key points**
- Component security asks "is this service hardened?"; solution security asks "can an attacker or a mistake cross from one part to another?"
- The architect owns the seams: integrations, identity, data flows, third parties, operations.
- Security is a set of properties (confidentiality, integrity, availability, accountability) the design must show, not a product list.
- The output is a view that a security team can review and approve.

**Show:** a Larkspur system context with trust boundaries drawn: internet, store network, platform, on-premises ERP, payment provider, CRM SaaS.

**Check:** Why is "we bought a WAF and an EDR" not a security architecture? *(It lists products; it does not show threats, boundaries, or which control covers which risk.)*

---

## ARC-028-L02 · Zero trust and defense in depth (12 min)
**Goal:** apply zero trust and layered defense across application, data, network, and identity.

**Key points**
- Zero trust: never trust a request because of where it comes from; verify identity, device, and context every time, and grant least privilege.
- Defense in depth: several independent layers so one failure does not mean a breach.
- Layers: identity (strong authentication, short-lived tokens), application (input validation, authorization), data (encryption, tokenization), network (segmentation, private endpoints).
- Assume breach: limit the blast radius and detect movement.

**Show:** a table with the four layers as rows and columns "control", "what it stops", "what happens if it fails". Fill it for the store-to-platform path.

**Check:** A store till is on the corporate network. Under zero trust, does that alone allow it to call the ERP API? *(No. It must authenticate and be authorized for that specific call.)*

---

## ARC-028-L03 · Solution-level threat modeling (12 min)
**Goal:** threat-model a whole solution and rank threats by risk.

**Key points**
- Start from a data-flow view with trust boundaries; ask what can go wrong at each boundary (a method such as STRIDE helps; verify the method wording before recording).
- Look at the whole: integrations, admin paths, third parties, and people processes.
- Rate each threat by likelihood and impact; threats are not equal.
- Every top threat gets a control, an owner, and a way to check the control works.

**Show:** a threat table: ID, boundary, threat, likelihood, impact, control, owner, evidence.

**Check:** Why rank threats before choosing controls? *(Budget and effort are limited; controls should follow risk, not habit.)*

---

## ARC-028-L04 · Controls and security requirements (10 min)
**Goal:** connect controls to business security requirements and standards.

**Key points**
- Requirements come from the business (fraud tolerance, customer trust), regulation, and company standards; frameworks such as ISO 27001 or NIST are common references (verify current versions before recording).
- Control types: preventive, detective, corrective.
- A traceability map links requirement, threat, control, and owner.
- A control with no threat behind it is cost without benefit; a threat with no control is an open risk to accept formally.

**Show:** a map row: "Protect payment data" → threat "card-skimming script on checkout page" → control "hosted payment fields plus content security policy" → owner: web platform lead.

**Check:** What do you do with a top threat you decide not to fix now? *(Record it as an accepted risk with an owner and a review date.)*

---

## ARC-028-L05 · Demo: threat-modeling Larkspur's checkout and payment flow (14 min)
**Goal:** run a worked threat-modeling session on checkout; prepares ARC-028-LAB1.

**Steps**
1. Draw the checkout data flow: browser, web app, basket service, payment provider's hosted page, order service, ERP.
2. Mark trust boundaries: browser/internet, platform/provider, platform/ERP.
3. Walk each boundary: skimming script, price tampering, replayed payment callback, stolen session, insider refund abuse.
4. **Planned mistake:** jump straight to controls (a WAF, more logging) before ranking. Fix: score each threat first; the replayed callback and price tampering outrank a generic WAF rule.
5. Assign controls and owners to the top threats and record accepted risks.

---

## ARC-028-L06 · Demo: walking a security team through the security architecture view (13 min)
**Goal:** present the security view so a CISO team can approve it; prepares ARC-028-LAB1.

**Steps**
1. Open with scope, assets, and the three risks that matter most to Larkspur.
2. Show the trust-boundary diagram, then the layered control map.
3. Walk the top ten threats with control and owner; point to evidence for each.
4. **Planned mistake:** present every control equally for 40 minutes. Fix: lead with the top risks, keep the full map as an appendix, and ask the CISO for decisions.
5. Capture review comments as actions and agree the approval path.
