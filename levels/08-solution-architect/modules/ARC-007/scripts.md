# ARC-007 · Architecture principles — Lecture scripts

**Video:** 56 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-007-L01 · What makes a principle useful (10 min)
**Goal:** tell real principles from slogans.

**Key points**
- A principle is a durable rule of choice that guides decisions across projects.
- Useful: it is specific enough to change a decision and can be disagreed with.
- Useless: "use best practices"; nobody can choose the opposite.
- Principles come from business strategy and constraints, not from technology fashion.

**Show:** two lines side by side: "Be secure" (platitude) and "Customer data is accessed only through owned APIs, never by direct database reads from other systems" (usable).

**Check:** What test shows a principle is not a platitude? *(A sensible person could argue for the opposite, and it changes some decision.)*

---

## ARC-007-L02 · Statement, rationale, implications (10 min)
**Goal:** write principles in a complete three-part form.

**Key points**
- Statement: one clear sentence.
- Rationale: why the business benefits.
- Implications: what we must do or give up as a result; this is the part that bites.
- Add owner and how exceptions are requested.

**Show:** Larkspur principle: Statement "Buy commodity capabilities; build only where we differentiate." Rationale: focus scarce engineering on customer experience. Implications: vendor assessment needed, integration effort accepted, exit plans required.

**Check:** Which part of a principle states the cost? *(The implications.)*

---

## ARC-007-L03 · Common principle sets (12 min)
**Goal:** know typical principle families and apply them to design.

**Key points**
- Standardization: reuse approved platforms and patterns to cut cost and risk.
- Interoperability: integrate through published interfaces and open standards.
- Security: protect data by design, least privilege, defense in depth.
- Evolvability: change parts without changing everything; loose coupling at boundaries.
- Others: data as an asset, business continuity, simplicity.

**Show:** table mapping each family to a Larkspur decision: standardization → one API style; interoperability → carriers integrate via standard APIs; security → tokenized card data only; evolvability → ERP access behind an anti-corruption layer.

**Check:** Which family would justify putting the ERP behind an interface layer? *(Evolvability, supported by interoperability.)*

---

## ARC-007-L04 · When principles conflict (10 min)
**Goal:** resolve conflicts openly instead of silently.

**Key points**
- Principles conflict in real cases: standardization versus fit for purpose; speed versus security.
- Rank or weigh them for the context and record the reasoning.
- An exception is allowed, time-limited, owned, and recorded with an exit date.
- Repeated exceptions signal that the principle needs revision.

**Show:** a conflict record: standardize on one messaging platform versus a store system that supports only file transfer; decision: exception for stores, review in 12 months, owner IT director.

**Check:** What should accompany an exception? *(An owner, a rationale, and a review or expiry date.)*

---

## ARC-007-L05 · Demo: drafting Larkspur's principles with the CIO (14 min)
**Goal:** run a drafting session and produce principles that change decisions. Prepares `ARC-007-LAB1`.

**Steps**
1. Collect strategy inputs: growth plan, cost targets, existing standards, risk appetite.
2. Brainstorm candidate principles and cut to eight to ten.
3. Write statement, rationale, implications for each; test with "who would disagree?".
4. Apply each to a real decision, such as choosing SaaS commerce or keeping ERP as master for finance.
5. **Planned mistake:** the draft includes "use best practices" and "be cloud native". Fix: replace with testable statements, add implications, and remove any principle that cannot change a decision.
6. Resolve one conflict (standardization versus speed) on record and get CIO sign-off.

**Check:** Why apply each principle to a real decision? *(To prove it changes something and to reveal missing implications.)*
