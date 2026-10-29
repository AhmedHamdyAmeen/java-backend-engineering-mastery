# SRA-004 · Data ownership strategy — Lecture scripts

**Video:** 84 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-004-L01 · Who owns the data (10 min)
**Goal:** show why unclear data ownership causes the slowest, costliest problems at scale.

**Key points**
- Owner: the team accountable for a data set's meaning, quality, access, and lifecycle.
- Without an owner, copies drift, definitions fork, and nobody fixes errors.
- Ownership differs from storage: a platform may host data owned by a domain team.
- Operational data (serving the product) and analytical data (reporting, models) both need owners.

**Show:** a table of "customer address" copies in five systems, each with a different format and no owner, and the three incidents that came from the mismatch.

**Check:** Does hosting a data set make a team its owner? *(No; the owner is accountable for meaning, quality, and access.)*

---

## SRA-004-L02 · Federated ownership (12 min)
**Goal:** design ownership that scales by giving each domain its data without losing coherence.

**Key points**
- Federated: domain teams own their data; shared standards and a platform keep it consistent.
- Each data set has one owner, a described meaning, and named consumers.
- Authoritative source versus copy: copies are labeled and refreshed from the source.
- A central team supplies tools and standards, not all the data work.

**Show:** an ownership map for Commerce 2030: Orders team owns orders, Seller team owns seller profiles, Finance owns ledger, each with consumers listed beside it.

**Check:** What does a central data platform team provide in a federated model? *(Tools, standards, and shared infrastructure, not ownership of every data set.)*

---

## SRA-004-L03 · Data contracts (12 min)
**Goal:** make the agreement between a producer and its consumers explicit and checkable.

**Key points**
- A data contract states schema, semantics (what each field means), quality rules, and service levels.
- Semantics matter most: "order_total" including tax or not is the usual dispute.
- Version contracts and give notice before breaking changes.
- Check contracts automatically at the producer's pipeline, not after consumers break.

**Show:** a contract outline for `OrderPlaced`: fields and types, meaning of each amount, completeness rule, freshness SLA (verify target with consumers), owner, change policy.

**Check:** Which part of a contract do teams most often omit, causing disputes? *(Semantics: what the fields mean.)*

---

## SRA-004-L04 · Federated governance (10 min)
**Goal:** govern sensitive data without turning governance into a bottleneck.

**Key points**
- Central policy, local decisions: classify data once, apply rules by classification.
- Access decisions sit with the data owner within policy; exceptions escalate.
- Automate controls: tagging, masking, access logging.
- Measure governance by time to grant legitimate access and by incidents.

**Show:** a table: classification (public, internal, personal, payment), allowed uses, default access path, and who approves exceptions.

**Check:** Why not have one central board approve every access request? *(It becomes a bottleneck and the owners closest to the data lose accountability.)*

---

## SRA-004-L05 · Data mesh: ideas and limits (10 min)
**Goal:** judge data mesh ideas against what the organization can support.

**Key points**
- Ideas: domain ownership, data as a product, self-serve platform, federated governance.
- It needs mature domain teams, a data platform, and product thinking about data.
- Risks: duplicated effort, inconsistent standards, and hard cross-domain analytics if underfunded.
- Adopt in steps: start with ownership and contracts, add platform features later.

**Show:** a maturity checklist: Do domains have stable teams? Is there a catalog? Do consumers exist for the data products? Is there a platform team? Score and choose a step.

**Check:** Is data mesh a tool you install? *(No; it is an organizational and architectural approach that needs maturity.)*

---

## SRA-004-L06 · Demo: writing a data contract for order events used by finance (15 min)
**Goal:** write and agree a contract between the Orders team and Finance; prepares SRA-004-LAB1.

**Steps**
1. Interview the producer and consumer: what Finance needs (revenue recognition, refunds, tax) and how fresh.
2. Draft the schema and write semantics for each money field: gross, discount, tax, shipping, currency.
3. Add quality rules (no missing currency, totals reconcile) and freshness and delivery guarantees.
4. Agree versioning and a deprecation notice period; add automated checks in the producer pipeline.
5. **Planned mistake:** publish only a schema and field names. Fix: add semantics and reconciliation rules after a test shows Finance and Orders compute revenue differently.
6. Sign off: both teams record the contract and name owners.

---

## SRA-004-L07 · Demo: resolving a dispute over who owns "customer" (15 min)
**Goal:** facilitate a leadership session that settles an ownership conflict; prepares SRA-004-LAB1.

**Steps**
1. Gather the parties: Accounts, Marketing, Support, and the marketplace team all claim or avoid "customer".
2. List what each needs: identity, consent, preferences, history. Notice they are different things.
3. Split the concept: Identity owned by the Accounts team, consent by Privacy, marketing segments by Marketing, support history by Support.
4. Define the authoritative source and how copies are refreshed, with contracts between teams.
5. **Planned mistake:** declare one "customer" team that owns everything. Fix: show it will become a bottleneck and own only identity, then apply the split.
6. Record the decision and a review date.
