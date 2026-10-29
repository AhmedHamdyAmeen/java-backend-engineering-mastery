# SRA-001 · Architecture at scale — Lecture scripts

**Video:** 86 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-001-L01 · From system architecture to organizational architecture (12 min)
**Goal:** show that at 25 teams the architecture you manage is the system plus the teams that own it.

**Key points**
- Conway's law: systems tend to mirror the communication paths of the organization that builds them.
- Past a certain size, most delay comes from coordination between teams, not from code.
- Architecture decisions now include ownership, interfaces between teams, and who pays for shared parts.
- You steer by changing boundaries and incentives, not by reviewing every design.

**Show:** a diagram of Commerce 2030 with two layers: services (checkout, inventory, pricing, shipping) and the teams owning them, with arrows where a feature needs three teams to change together.

**Check:** Why does a feature that needs five teams to change often point to an architecture problem? *(Boundaries cut across the change; coordination cost is a design signal.)*

---

## SRA-001-L02 · Platforms, domains, and shared capabilities (12 min)
**Goal:** separate three things people loosely call "platform".

**Key points**
- Product domain: a business area with its own goals (checkout, seller onboarding, fulfillment).
- Shared capability: something several domains need (notifications, identity, search).
- Platform: a shared capability offered as a product, with users, a roadmap, and support, so product teams self-serve.
- A shared library or a shared database is not a platform; it is shared coupling.

**Show:** a three-column table for Commerce 2030 listing each item as domain, shared capability, or platform, with the question "who is the customer and how do they get it without a ticket?".

**Check:** What turns a shared capability into a platform? *(It is run as a product with self-service use, clear ownership, and customers.)*

---

## SRA-001-L03 · Drawing platform boundaries (10 min)
**Goal:** place boundaries so product teams wait less on each other.

**Key points**
- A good boundary has a stable interface and a team that can change the inside alone.
- Extract a platform when several teams repeat the same work and the need is stable.
- Keep volatile, differentiating logic in product domains.
- Watch cognitive load: a platform should lower what a product team must know.

**Show:** a before/after sketch of the "payments" capability: three teams each integrating a provider, versus one payments platform with a self-service API and a service-level objective.

**Check:** Which should become a platform first: a stable repeated need or a fast-changing differentiator? *(The stable repeated need.)*

---

## SRA-001-L04 · Evolutionary architecture (12 min)
**Goal:** apply principles for architecture that can change safely over years.

**Key points**
- Incremental change: many small, reversible steps beat one big redesign.
- Fitness functions: automated checks that an important quality (coupling, latency, cost) still holds.
- Last responsible moment: delay a decision until delaying costs more than deciding, without ignoring lead time.
- Prefer options that keep choices open when change is likely, such as the marketplace design.

**Show:** a list of three decisions for the marketplace (seller identity model, payout provider, listing search) each tagged "decide now", "decide at last responsible moment", or "keep open", with a reason.

**Check:** What does "last responsible moment" not mean? *(Not "as late as possible"; waiting must not cost more than deciding.)*

---

## SRA-001-L05 · Reading misalignment between teams and systems (10 min)
**Goal:** spot where the org chart and the architecture fight each other.

**Key points**
- Signals: one service changed by many teams, one team owning many unrelated services, constant cross-team tickets.
- Check ownership gaps: a system with no clear owner decays first.
- Compare change history to team boundaries; the data shows the real coupling.
- Fix with the smaller change: move a boundary, an owner, or an interface before restructuring.

**Show:** a heat map of Commerce 2030 pull requests per service, colored by how many distinct teams touched it in the last quarter, with the top five highlighted.

**Check:** What is better evidence of misalignment than opinions? *(Change history: which teams change which services, and how often they wait on each other.)*

---

## SRA-001-L06 · Demo: mapping the Commerce 2030 landscape (15 min)
**Goal:** build a landscape map of systems, teams, platforms, and capabilities; prepares SRA-001-LAB1.

**Steps**
1. Collect inputs: service catalog, team list, on-call rotas, and a quarter of pull-request history.
2. Draw systems grouped by product domain, with the owning team on each, and mark shared capabilities.
3. Add dependency arrows from change history, not from memory.
4. Mark coordination hot spots: services touched by many teams, ownership gaps, repeated cross-team tickets.
5. **Planned mistake:** draw only systems and skip teams, then label every shared thing "platform". Fix: add team names and apply the test "customer, self-service, roadmap", relabeling most items as shared capabilities or shared coupling.
6. Rank the hot spots with team leads and keep the five worst.

---

## SRA-001-L07 · Demo: moving one capability from product teams into a platform (15 min)
**Goal:** run a worked leadership session that extracts one capability into a platform without stopping delivery; prepares SRA-001-LAB1.

**Steps**
1. Pick the candidate from the hot spots: for example, notifications implemented separately by four teams.
2. Write the case: duplicated effort, incident count, and what the platform promises (interface, SLO, support).
3. Role-play the conversation with the four team leads: what they lose (control), gain (time), and what they need first.
4. Plan the transition: platform team staffed from existing teams, a thin interface first, migration one team at a time, with a fitness check for new direct provider calls.
5. **Planned mistake:** announce the platform and mandate migration by a date. Fix: start with one willing team, publish adoption metrics, and make the platform the easiest path rather than the only one.
6. Define success: fewer cross-team tickets and faster feature lead time within two quarters.
