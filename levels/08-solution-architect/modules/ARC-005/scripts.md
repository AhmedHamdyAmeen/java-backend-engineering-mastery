# ARC-005 · Architecture modeling — Lecture scripts

**Video:** 66 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-005-L01 · Models answer questions (8 min)
**Goal:** treat every diagram as an answer to one question for one audience.

**Key points**
- Before drawing, write the question ("which systems touch customer data?") and the reader.
- A model abstracts; it leaves things out on purpose.
- Every diagram needs a title, legend, audience, and scope.
- Throw away diagrams that nobody asks questions of.

**Show:** a Larkspur diagram header block: Title, Question, Audience, Scope, Legend, Owner, Date.

**Check:** What three things should accompany a diagram? *(A question it answers, an audience, and a legend.)*

---

## ARC-005-L02 · C4 for solution architects (10 min)
**Goal:** use C4 levels to show structure at the right depth.

**Key points**
- Levels: system context, containers, components, code. Solution architects mostly use the first two.
- Context shows the system, people, and neighbouring systems.
- Containers show deployable parts (apps, services, databases) and their protocols.
- C4 is a set of abstractions, not a strict notation; keep the legend explicit.

**Show:** Larkspur context diagram: customers, store staff, new commerce platform, ERP, CRM, payment provider, carriers. Then containers: web app, mobile app, API gateway, order service, inventory service, database.

**Check:** Which two C4 levels do solution architects use most? *(System context and containers.)*

---

## ARC-005-L03 · The useful parts of UML (10 min)
**Goal:** pick the few UML diagrams that earn their place.

**Key points**
- Sequence diagrams: who calls whom, in what order, including failures.
- State diagrams: lifecycle of an object, such as an order.
- Activity diagrams: flow with decisions; use sparingly.
- Skip class-diagram detail at architect level; leave it to teams.

**Show:** sequence for payment authorization: web app, order service, payment provider, with timeout and retry. State diagram of an order: placed, paid, picked, shipped, delivered, returned.

**Check:** Which diagram best shows an order's lifecycle? *(A state diagram.)*

---

## ARC-005-L04 · ArchiMate introduction (12 min)
**Goal:** read and draw layered business, application, and technology models.

**Key points**
- ArchiMate is an Open Group modeling language for enterprise architecture; verify the current version before recording.
- Layers: business, application, technology, plus motivation, strategy, and implementation elements.
- Relationships link layers: business processes are supported by applications, which run on technology.
- Use viewpoints to show a subset; do not model everything.

**Show:** a layered view of Larkspur today: business (store sale, online order), application (POS, web shop, ERP, CRM), technology (store servers, hosted data center). Arrows from process to application to node.

**Check:** What does a layered view reveal? *(Which applications and technology support each business process.)*

---

## ARC-005-L05 · Integration and deployment diagrams (12 min)
**Goal:** show how systems connect and where they run.

**Key points**
- Integration diagram: systems, interface names, protocol, direction, data, owner.
- Mark synchronous versus asynchronous and batch flows differently.
- Deployment diagram: environments, networks, zones, and trust boundaries.
- Show where data crosses a boundary; security reviewers look there first.

**Show:** Larkspur interfaces: web shop to ERP nightly file over SFTP; POS to ERP daily sales batch; shop to payment provider HTTPS API; CRM sync. Deployment: store LAN, data center zone, cloud zone, boundary lines.

**Check:** What should an integration arrow carry as a label? *(Protocol, direction, data, and ideally owner.)*

---

## ARC-005-L06 · Demo: one Larkspur model, three audiences (14 min)
**Goal:** derive three views from one model for different readers. Prepares `ARC-005-LAB1`.

**Steps**
1. Keep one source: elements and relationships for Larkspur's current landscape (ideally as text or a modeling tool).
2. Generate a business view for the sponsor: capabilities and the systems supporting them.
3. Generate an integration view for engineers: interfaces with protocol and volume.
4. Generate a trust-boundary view for security.
5. **Planned mistake:** the engineers' integration diagram is sent to the sponsor. Fix: replace with the business view and keep detail on an appendix page.
6. Check consistency: the same element names and IDs in all views; keep model files in version control where practical.

**Check:** Why derive views from one model? *(It keeps names and relations consistent across audiences.)*
