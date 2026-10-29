# STF-006 · Cross-domain systems — Lecture scripts

**Video:** 90 min · **Running case:** *Platform 2.0* — the Commerce group (Shop + FulfillCo) now has about 20 product teams; delivery has slowed, every team runs its own pipelines, the same incidents repeat, and onboarding takes weeks; you are a Staff engineer with no team of your own and a mandate to make the whole organization faster and safer.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## STF-006-L01 · Systems everyone depends on (12 min)
**Goal:** identify the systems that many domains rely on and the coupling they create.

**Key points**
- Cross-domain systems: identity, billing, commerce core, data, integration.
- Their failures or changes affect many teams at once.
- Duplication appears when teams cannot wait for the shared system.
- Map dependencies with real call and data flows, not org charts.

**Show:** a dependency graph with five shared systems at the center and 20 teams around them, lines weighted by use.

**Check:** Why do cross-domain systems create duplication? *(Teams that cannot rely on a slow shared system build their own.)*

---

## STF-006-L02 · Identity, billing, and data as cross-domain capabilities (14 min)
**Goal:** understand the typical shape and risks of the three biggest shared capabilities.

**Key points**
- Identity: who the customer or user is, shared by checkout, support, and marketing; duplicates cause security and experience problems.
- Billing: money rules need one source of truth and strong audit.
- Data: shared analytics and operational data need ownership and quality rules.
- Each has regulatory and security weight, so ownership matters.

**Show:** a table of the three capabilities with consumers, typical duplication, and risk if inconsistent.

**Check:** Why is duplicated customer identity risky? *(Records diverge, security rules differ, and customers get inconsistent experiences.)*

---

## STF-006-L03 · Shared platform or domain-owned? (12 min)
**Goal:** decide where a capability should live.

**Key points**
- Share when many domains need the same stable behavior and consistency matters.
- Keep in a domain when needs differ or change fast with that domain.
- A shared system needs an owner, an API, and service levels, or it becomes a trap.
- Avoid both extremes: everything shared or nothing shared.

**Show:** a decision tree: stable and common? consistency required? change rate? team able to own? leading to shared platform, domain-owned, or shared library.

**Check:** When keep a capability in a domain? *(When needs differ across domains or change quickly with the domain.)*

---

## STF-006-L04 · Ownership and funding of shared systems (10 min)
**Goal:** give shared systems a durable owner and funding.

**Key points**
- Every shared system has one accountable team with on-call and a roadmap.
- Funding options: central budget, chargeback, or consumer contributions; pick one and explain why.
- Define the service level and how consumers request changes.
- Without funding, shared systems decay.

**Show:** a table of three funding models with benefits, risks, and when each fits.

**Check:** What is the risk of a shared system with no owner? *(It decays, nobody fixes incidents, and consumers build workarounds.)*

---

## STF-006-L05 · Evolving a shared system safely (12 min)
**Goal:** change a shared system without stalling consumers.

**Key points**
- Version interfaces and run old and new side by side.
- Migrate consumers in steps, starting with willing ones.
- Publish a deprecation timeline and offer help.
- Keep consumer roadmaps in view; align timing to their windows.

**Show:** a migration timeline: new API in parallel, three consumers migrated per month, old API retired after all have moved.

**Check:** Why run old and new side by side? *(Consumers can move at their own pace without a big-bang cutover.)*

---

## STF-006-L06 · Demo: untangling three competing customer-identity systems (15 min)
**Goal:** map three identity systems and plan consolidation; prepares STF-006-LAB1.

**Steps**
1. Inventory the three systems: owners, data held, consumers, login flows.
2. Compare fields, formats, security controls, and failure history.
3. Pick a target (one of them or a new one) with criteria.
4. **Planned mistake:** decreeing "use system A by June". Fix: interview consumers and plan stepwise migration with compatibility mapping.
5. Draft the step plan with the first consumers and the checkpoint to keep all working.

---

## STF-006-L07 · Demo: a funding model for the shared integration platform (15 min)
**Goal:** design ownership and funding for a shared system; prepares STF-006-LAB1.

**Steps**
1. Describe the integration platform, its consumers, and current cost.
2. Compare central funding, chargeback by usage, and mixed.
3. Test each with a finance partner for fairness and incentives.
4. **Planned mistake:** choosing chargeback so teams avoid using the platform. Fix: fund the core centrally and charge only for heavy optional usage.
5. Write the ownership statement: owner, service level, change process, funding, review date.
