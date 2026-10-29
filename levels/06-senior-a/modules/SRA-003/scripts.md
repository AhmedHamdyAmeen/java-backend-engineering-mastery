# SRA-003 · Complex domain modeling — Lecture scripts

**Video:** 88 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-003-L01 · Strategic DDD (12 min)
**Goal:** use strategic domain-driven design to decide where models and team boundaries belong.

**Key points**
- A bounded context is a boundary inside which a model and its words mean one thing.
- "Customer" means different things to billing, support, and marketing; separate contexts keep each model clean.
- Ubiquitous language: the team and domain experts use the same words in talk and code.
- Strategic design is about boundaries and relationships between contexts, not class diagrams.

**Show:** three boxes for the marketplace (Listings, Orders, Seller Payouts) each defining "seller" differently, with the words each context uses.

**Check:** Why keep separate models of "customer" in separate contexts? *(Each context needs its own meaning; one shared model grows contradictory and couples teams.)*

---

## SRA-003-L02 · Core, supporting, and generic subdomains (10 min)
**Goal:** classify subdomains so investment goes where it differentiates.

**Key points**
- Core: gives the business its edge; invest the best people and build in-house.
- Supporting: needed but not differentiating; build simply or buy and adapt.
- Generic: solved elsewhere (identity, payments, email); buy or use open source.
- Classification changes over time and by company: ask what customers choose us for.

**Show:** a table for Commerce 2030 with subdomain, class, and build/buy note: seller trust and ranking (core), onboarding workflow (supporting), tax calculation and payments (generic).

**Check:** What is the usual strategy for a generic subdomain? *(Buy or adopt an existing solution rather than build.)*

---

## SRA-003-L03 · Context mapping patterns (14 min)
**Goal:** describe relationships between contexts using standard patterns.

**Key points**
- Partnership: two teams succeed or fail together and coordinate changes.
- Customer–supplier: the downstream team's needs influence the upstream plan.
- Conformist: downstream accepts the upstream model as is, with no influence.
- Open host service and published language: upstream offers a stable, documented interface and shared format.
- A context map shows the real relationships, including the uncomfortable ones.

**Show:** a context map sketch: Marketplace Listings customer of Catalog, conformist to a carrier API, publishing an order-events language used by Finance.

**Check:** What does a conformist relationship mean? *(Downstream adopts the upstream model without influence.)*

---

## SRA-003-L04 · Anti-corruption layers (10 min)
**Goal:** protect a clean model from a legacy or third-party model.

**Key points**
- An anti-corruption layer (ACL) translates between the foreign model and your own at the boundary.
- It isolates vendor naming, quirks, and failures so they do not spread.
- Use it when the external model is poor, volatile, or hard to replace.
- It costs code and a team's attention; skip it when the external model fits well.

**Show:** a layout: domain code calls a `CarrierGateway` interface; an adapter maps carrier statuses to the domain's `ShipmentStatus` and handles errors and retries.

**Check:** When is an ACL not worth building? *(When the external model already fits your domain and is stable.)*

---

## SRA-003-L05 · Event storming at scale (12 min)
**Goal:** run collaborative modeling with many teams and domain experts.

**Key points**
- Event storming maps a process as domain events on a timeline with commands, actors, and policies.
- Invite people with real knowledge: domain experts, product, engineers from every touching team.
- Start wide (big picture), then zoom into hot spots; boundaries appear where language changes.
- Capture unresolved questions and conflicts; do not argue them away in the room.

**Show:** a wall layout: orange events in time order, blue commands, yellow actors, pink hot spots, with lines drawn where the vocabulary changes.

**Check:** Where do candidate context boundaries often appear in an event storm? *(Where the meaning of words changes or ownership shifts.)*

---

## SRA-003-L06 · Demo: event storming the seller marketplace (15 min)
**Goal:** facilitate a big-picture session and derive candidate contexts; prepares SRA-003-LAB1.

**Steps**
1. Prepare: invite seller operations, finance, support, and engineers from five teams; set a wide wall and a clear scope from "seller applies" to "seller is paid".
2. Collect events silently, then merge and order them in time.
3. Add commands, actors, and policies; mark hot spots such as "who approves a seller".
4. Draw candidate boundaries where language and ownership change.
5. **Planned mistake:** let engineers fill the wall with technical events (message published, row inserted). Fix: restart at the business level; use "Seller Approved", "Payout Released".
6. Record open questions and agree who resolves each.

---

## SRA-003-L07 · Demo: an anti-corruption layer around a carrier API (15 min)
**Goal:** decide whether and how to isolate a carrier integration; prepares SRA-003-LAB1.

**Steps**
1. Review the carrier API: statuses, error codes, rate limits, and its change history.
2. Name the domain concepts we own: shipment, delivery attempt, delivery exception.
3. Design the ACL: a domain-facing interface, a translator, and contract tests against the carrier sandbox.
4. Decide the ownership and cost: who maintains it and how a second carrier would plug in.
5. **Planned mistake:** pass carrier status strings straight into domain code. Fix: translate at the boundary and test the mapping, including unknown statuses.
6. Record the decision in the context map as a conformist relationship softened by an ACL.
