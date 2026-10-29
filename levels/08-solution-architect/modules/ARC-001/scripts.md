# ARC-001 · Architecture roles — Lecture scripts

**Video:** 67 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-001-L01 · What architects actually do (10 min)
**Goal:** show that architecture work is mostly decisions, communication, and risk reduction, not drawing.

**Key points**
- An architect makes or guides the decisions that are expensive to change later.
- Most of the time goes to listening, explaining, and aligning people.
- Deliverables (diagrams, decision records) exist to carry decisions to others.
- The architect answers "is this the right thing, built in a workable way?", not "is the code right?".

**Show:** a week in the life on the Larkspur program: Monday sponsor meeting, Tuesday ERP interface workshop, Wednesday decision record on payments, Thursday design review with two delivery teams, Friday risk review. Count hours spent drawing: under six.

**Check:** Why are decisions the core architecture output? *(They are costly to reverse and shape what every team builds.)*

---

## ARC-001-L02 · Software, solution, enterprise, cloud, and data architects (12 min)
**Goal:** tell the five common architect roles apart by scope, horizon, and deliverables.

**Key points**
- Software architect: one system or product; structure and quality of the code base; months.
- Solution architect: one business solution spanning several systems; options, design, integration; the life of a program.
- Enterprise architect: the whole organization; capabilities, standards, roadmaps; years.
- Cloud architect: platform, landing zones, cost and security of hosting. Data architect: models, ownership, flows, governance.
- Titles vary by company; judge by scope, not title.

**Show:** a table with columns scope, horizon, typical deliverables, and Larkspur examples (web shop internals, the whole commerce solution, the retail capability roadmap, the cloud landing zone, the customer data model).

**Check:** Who would own the three-year capability roadmap across all Larkspur business units? *(The enterprise architect.)*

---

## ARC-001-L03 · The solution architect in a program (12 min)
**Goal:** place the solution architect among sponsors, enterprise architecture, delivery teams, and vendors.

**Key points**
- Business side: sponsor and product owners state outcomes; the architect translates them into a solution.
- Enterprise architecture sets principles and standards; the architect applies them and proposes exceptions.
- Delivery teams build; the architect guides and unblocks, and keeps the design coherent across teams.
- Vendors supply products; the architect holds them to the architecture.

**Show:** a hub diagram with the solution architect in the middle and four arrows labeled with what flows each way (outcomes and budget in, options and designs out; standards in, exceptions out; guidance out, feedback in; requirements out, product constraints in).

**Check:** Who sets enterprise-wide standards the program must follow? *(Enterprise architecture, not the solution architect.)*

---

## ARC-001-L04 · Accountabilities and boundaries (10 min)
**Goal:** be explicit about what the architect owns and what they do not.

**Key points**
- Accountable for: the solution design's fitness, options and recommendations, decision log, architectural risks, quality attribute coverage.
- Not accountable for: business priorities and budget (sponsor), enterprise standards (EA), delivery schedule (project manager), code quality inside a team (tech lead).
- Write decision rights down: who recommends, who decides, who is consulted.
- Boundaries prevent both gaps and turf wars.

**Show:** a short decision-rights table (RACI style) for three Larkspur decisions: choose the commerce platform, choose the payment provider, approve a one-off exception to the API standard.

**Check:** Who decides the program budget? *(The sponsor or business owner; the architect advises on cost implications.)*

---

## ARC-001-L05 · From senior engineer to architect (10 min)
**Goal:** give a realistic path and the skill shifts involved.

**Key points**
- Shifts: from depth in one stack to breadth across many; from building to influencing; from code to documents and conversations.
- Keep hands-on skills current enough to be credible: prototypes, code reviews, reading.
- Build evidence: lead a design, write decision records, present to non-engineers.
- Solution architect and Staff engineer are parallel tracks, not rungs of one ladder.

**Show:** a personal gap table: skill, current level, evidence needed, next step, date (for example "facilitate a workshop: never done; run one for a non-technical group; next quarter").

**Check:** Is the solution architect the next step after Staff engineer? *(No; they are related, parallel tracks.)*

---

## ARC-001-L06 · Demo: mapping the architecture roles on the Larkspur program (13 min)
**Goal:** assign every architecture concern on the Larkspur program to the right role. Prepares `ARC-001-LAB1`.

**Steps**
1. List the program's concerns: commerce platform choice, cloud landing zone, customer data model, ERP interface design, coding standards inside the web team, capability roadmap.
2. Place each concern on the five-role table (software, solution, enterprise, cloud, data).
3. Draw the interface list: who the solution architect talks to weekly, and what each party gives and expects.
4. Write decision rights for the three biggest decisions.
5. **Planned mistake:** assign the coding standards and the capability roadmap to the solution architect "because it is architecture". Fix: coding standards go to the team's software architect or tech lead; the roadmap to enterprise architecture.
6. Review the result with a role-played sponsor for gaps and overlaps.

**Check:** What test quickly shows a concern is not yours? *(It sits outside the solution's scope, or the decision right is written as someone else's.)*
