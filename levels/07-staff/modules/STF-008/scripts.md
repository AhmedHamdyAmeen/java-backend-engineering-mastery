# STF-008 · Security architecture strategy — Lecture scripts

**Video:** 98 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-008-L01 · Security strategy vs security reviews (10 min)
**Goal:** show why per-project reviews do not scale and what a strategy adds.

**Key points**
- Reviews find issues one project at a time; the same issues return.
- A strategy removes classes of issues by changing defaults and structure.
- Security is a shared responsibility: the security team sets direction and tooling; teams build safely.
- Measure reduction in recurring findings, not only the count of reviews.

**Show:** a chart sketch: audit findings per quarter by category, with three categories recurring in most teams.

**Check:** Why do recurring findings call for strategy, not more reviews? *(Reviews fix instances; strategy removes the cause for every team.)*

---

## STF-008-L02 · Threat landscape for a commerce organization (12 min)
**Goal:** list the main threats and the assets they target.

**Key points**
- Assets: customer data, payment flows, accounts, partner integrations, internal tools.
- Threats: credential stuffing, account takeover, fraud, injection, supply-chain attacks, insider misuse.
- Use threat modeling at organization level to rank by likelihood and impact.
- Update when the business changes, for example a marketplace or new countries.

**Show:** a table of five assets with top threats, current controls, and gaps.

**Check:** Why rank threats? *(Effort is limited; ranking directs it to the largest risks.)*

---

## STF-008-L03 · Organization-wide trust boundaries (12 min)
**Goal:** define where trust changes across people, services, and partners.

**Key points**
- Trust boundaries sit between the internet, internal services, partners, and sensitive stores.
- Use one identity strategy for people, services, and partners, with least privilege.
- Prefer authenticating every call between services rather than trusting the network.
- Document the map so teams place new systems correctly.

**Show:** a zone diagram: public edge, internal services, payment zone, data zone, partner connections, with the controls at each crossing.

**Check:** Why authenticate service-to-service calls? *(Network position is not proof of identity; attackers can land inside.)*

---

## STF-008-L04 · Secure defaults in the platform (14 min)
**Goal:** build safe behavior into the golden path so teams get it by default.

**Key points**
- Examples: encrypted storage and transport, secrets managed outside code, dependency scanning in pipelines, least-privilege service identities.
- A default that removes a class of findings beats a checklist.
- Make the secure way the easy way; make exceptions explicit and logged.
- Measure coverage: share of services on the golden path.

**Show:** a table of five defaults with the finding class each removes and how the platform enforces it.

**Check:** Why prefer a default to a checklist? *(Defaults work without effort or memory; checklists get skipped.)*

---

## STF-008-L05 · Supply-chain security at scale (10 min)
**Goal:** protect what teams build from and ship.

**Key points**
- Risks: vulnerable or malicious dependencies, tampered build steps, untrusted images.
- Controls: dependency pinning and scanning, software bill of materials, signed artifacts, protected build pipelines.
- Centralize in the shared pipeline so every team inherits it.
- Verify tool and standard versions before recording them.

**Show:** a pipeline diagram marking where scanning, signing, and provenance checks run.

**Check:** Why centralize supply-chain controls in the shared pipeline? *(Every team inherits them without separate work.)*

---

## STF-008-L06 · A joint roadmap with security (10 min)
**Goal:** agree a multi-year plan with the security team.

**Key points**
- Split roles: security owns policy, monitoring, and response; platform owns defaults and enforcement.
- Sequence by risk reduction and platform readiness.
- Share metrics: recurring findings, time to patch, coverage of defaults.
- Meet regularly; a joint roadmap fails if it is a one-time document.

**Show:** a three-year roadmap table: year, goal, owner, measure.

**Check:** Who owns default enforcement in the platform? *(The platform team, in partnership with security.)*

---

## STF-008-L07 · Demo: turning five recurring audit findings into platform defaults (15 min)
**Goal:** convert repeated findings into platform changes; prepares STF-008-LAB1.

**Steps**
1. Collect two years of audit findings across 20 teams and group by class.
2. Pick the five largest classes, such as secrets in code, outdated dependencies, missing service authentication.
3. For each, design a platform default and the check that proves it.
4. **Planned mistake:** writing five new policy pages. Fix: implement each as a template, pipeline gate, or platform setting.
5. Estimate findings removed per class and the rollout order.

---

## STF-008-L08 · Demo: a trust-boundary map for the whole organization (15 min)
**Goal:** draw the organization-wide trust boundaries; prepares STF-008-LAB1.

**Steps**
1. Gather system inventories and network, identity, and data-flow diagrams.
2. Draw zones and the flows that cross them, including partners.
3. Mark controls at each crossing and flag gaps.
4. **Planned mistake:** drawing the intended design only. Fix: verify with real traffic data and configurations.
5. Review with the security team and agree the first three gaps to close.
