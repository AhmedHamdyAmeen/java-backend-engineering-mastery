# ARC-002 · Business architecture — Lecture scripts

**Video:** 79 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-002-L01 · Why architects start with the business (8 min)
**Goal:** show that a design without a business anchor optimizes the wrong thing.

**Key points**
- Technology exists to enable capabilities the business needs; start there.
- Business architecture gives a stable vocabulary shared with non-technical people.
- It shows where investment matters most and where "good enough" is fine.
- Org charts and system lists change often; capabilities and value streams change slowly.

**Show:** two pitches for Larkspur: "move to microservices" versus "improve click-and-collect so store pickups succeed first time". Ask which the CFO can fund.

**Check:** Why start from capabilities rather than systems? *(They are stable and in business language, so they anchor scope and priorities.)*

---

## ARC-002-L02 · Business capabilities (12 min)
**Goal:** define a capability and write good capability names.

**Key points**
- A capability is what the business can do ("Manage Inventory"), independent of who does it or which system supports it.
- Name it noun-plus-verb or verb-plus-noun, consistently, at a stable level (not "SAP stock module").
- Levels: L1 domains (Sell, Fulfill, Serve), L2 capabilities, L3 sub-capabilities. Two or three levels is enough.
- A capability has owner, people, process, information, and technology supporting it.

**Show:** a Larkspur L1 list: Customer Engagement, Merchandising, Order Management, Inventory and Fulfillment, Payments and Finance, Store Operations, Customer Service, Insight and Reporting.

**Check:** Is "Finance Department" a capability? *(No, it is an org unit; "Manage Financial Accounting" is a capability.)*

---

## ARC-002-L03 · Capability maps and heat maps (10 min)
**Goal:** assess capabilities and show where change matters.

**Key points**
- A capability map is a one-page grid of capabilities grouped by domain.
- Heat map: color by an attribute, for example maturity, strategic importance, or pain.
- Two attributes together (importance high, maturity low) reveal investment targets.
- Evidence comes from interviews and data, then is validated with business owners.

**Show:** Larkspur grid with each capability colored by maturity (1-5) and a star for strategic importance. Click-and-collect: high importance, low maturity; Merchandising: medium importance, high maturity.

**Check:** Which capabilities deserve first investment? *(High strategic importance combined with low maturity.)*

---

## ARC-002-L04 · Value streams and processes (12 min)
**Goal:** model how value reaches the customer end to end, then place processes inside it.

**Key points**
- A value stream is the sequence of stages that delivers a result to a stakeholder, named from their view ("Order to Delivery").
- Each stage lists the capabilities it uses and the value it adds.
- Processes are the detailed how, modeled later and only where needed.
- Agree the stream first; modeling processes before that wastes effort.

**Show:** Order-to-Delivery stages: Browse, Order, Pay, Pick, Ship, Deliver, Support. Under each, the capabilities involved. Return-to-Refund as a second stream sharing several of the same capabilities.

**Check:** Which comes first, value stream or detailed process? *(The value stream; processes follow where detail is needed.)*

---

## ARC-002-L05 · Stakeholder mapping (8 min)
**Goal:** identify who matters, what they want, and how to engage them.

**Key points**
- Plot stakeholders by influence and interest: manage closely, keep satisfied, keep informed, monitor.
- For each, record goals, concerns, and what they must decide or approve.
- Include quiet stakeholders: store managers, customer service, security, finance.
- Update the map as the program moves.

**Show:** a 2x2 grid with Larkspur's CFO (high influence), store operations director, head of e-commerce, IT security, store managers, customer service, carriers.

**Check:** Someone with high influence and low interest is handled how? *(Keep satisfied: brief them and avoid surprises.)*

---

## ARC-002-L06 · Demo: Larkspur's capability map, built live (15 min)
**Goal:** build a capability map and heat map from interviews. Prepares `ARC-002-LAB1`.

**Steps**
1. Collect source material: annual report extract, org chart, three interview notes.
2. Draft L1 domains and L2 capabilities on a whiteboard; reconcile names.
3. Rate maturity and strategic importance per capability with evidence.
4. Color the heat map and highlight three hot spots (click-and-collect, stock accuracy, returns).
5. **Planned mistake:** the first draft mirrors the org chart (one box per department). Fix: regroup by what the business does and merge duplicated capabilities.
6. Validate with role-played business owners; note disagreements.

**Check:** What signals a map is really an org chart? *(Boxes named after departments or teams.)*

---

## ARC-002-L07 · Demo: tracing "buy online, pick up in store" across capabilities (14 min)
**Goal:** show how a concrete scenario is traced to capabilities, value stream stages, and solution components.

**Steps**
1. Write the scenario: customer orders online, pays, collects at store within two hours.
2. Walk the Order-to-Delivery stream and tag each stage with capabilities (Inventory Visibility, Order Orchestration, Payments, Store Fulfillment).
3. Add solution components that serve each capability (web and mobile front ends, inventory service, ERP, store handheld app).
4. Build the traceability table: capability, stream stage, component.
5. **Planned mistake:** a proposed "recommendation engine" component maps to no capability. Fix: either link it to Customer Engagement with a stated need, or remove it from scope.
6. Note capability gaps: store pickup scheduling has no system today.

**Check:** What does a component with no traceable capability tell you? *(It may be unnecessary, or a need was missed; resolve one way or the other.)*
