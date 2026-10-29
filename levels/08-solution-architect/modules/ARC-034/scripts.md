# ARC-034 · Architecture deliverables — Lecture scripts

**Video:** 71 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-034-L01 · Deliverables and their readers (10 min)
**Goal:** match each architecture deliverable to the person who must act on it.

**Key points**
- HLD: read by sponsors, reviewers, and security; they need to approve direction and risk.
- LLD: read by delivery teams; they need to build and estimate without guessing.
- ADRs: read by future maintainers; they need to know why, not only what.
- Interface contracts and deployment diagrams: read by partner teams and operations.
- A deliverable with no named reader and no decision it supports should not be written.

**Show:** a table with columns deliverable, reader, decision it enables, and length target, filled for the Larkspur pack.

**Check:** Who is the primary reader of an LLD? *(The delivery team that builds and estimates from it.)*

---

## ARC-034-L02 · The high-level design (12 min)
**Goal:** write an HLD a reviewer can approve in one sitting.

**Key points**
- Sections: purpose and scope, requirements and constraints, context view, container view, key decisions, quality attributes, risks, open questions.
- Show the decisions and their reasons, not the code structure.
- Each quality attribute gets a target and the design element that meets it.
- Keep it to a length a reviewer will actually read; link detail instead of including it.

**Show:** an HLD outline for Larkspur with one-line contents per section, marking which sections reviewers sign off.

**Check:** What does an HLD avoid? *(Implementation detail such as class structures and framework configuration.)*

---

## ARC-034-L03 · The low-level design (12 min)
**Goal:** write an LLD a team can build from, including the unhappy paths.

**Key points**
- An LLD refines one HLD component: responsibilities, internal modules, data model, sequence flows, and configuration.
- Error and edge cases are first-class: timeouts, retries, duplicate messages, partial failures, and what the user sees.
- Include non-functional specifics: expected load, timeouts, retry limits, idempotency rules.
- Test: could a delivery lead estimate it without asking what is in scope?

**Show:** an LLD outline for order fulfillment with a sequence flow for "payment captured, ERP unavailable" and a table of failure cases with handling.

**Check:** What commonly goes missing in weak LLDs? *(Error handling and edge cases.)*

---

## ARC-034-L04 · Interface contracts and deployment diagrams (10 min)
**Goal:** specify interfaces for parallel delivery and draw deployment views operations can use.

**Key points**
- A contract states operations or events, payload schemas, error codes, authentication, rate limits, versioning, and who owns it.
- Specify with a machine-readable format such as an OpenAPI or event schema file so both sides can test against it.
- A deployment diagram shows runtime nodes, networks, zones, and which software runs where, with environments marked.
- Operations needs ports, dependencies, and failover paths, not only boxes.

**Show:** a Larkspur ERP order-posting contract excerpt (operation, required fields, error codes) and a deployment sketch with web zone, application zone, data zone, and the link to on-premises ERP.

**Check:** Why a machine-readable contract? *(Both sides can generate stubs and test against the same definition in parallel.)*

---

## ARC-034-L05 · Demo: writing Larkspur's HLD section by section (14 min)
**Goal:** write the platform HLD as a worked design session; prepares ARC-034-LAB1.

**Steps**
1. Start from the approved option and the requirements: write purpose, scope, and the three constraints that shape everything.
2. Draw the context view with stores, web, mobile, ERP, CRM, payments, carriers; write one line per external link.
3. Draw the container view and list the five biggest decisions, each with a reason and a link to an ADR.
4. **Planned mistake:** include table schemas and class names in the HLD "for completeness". Fix: move them to the LLD, leave a reference, and show how the HLD shrinks to a reviewable length.
5. Write the quality attribute table: target, design element, how it will be evidenced.
6. List risks and open questions with owners and read the finished HLD as a reviewer would.

---

## ARC-034-L06 · Demo: turning an HLD component into an LLD a team can build (13 min)
**Goal:** turn the order-fulfillment component into a buildable LLD; prepares ARC-034-LAB1.

**Steps**
1. Take the HLD component "Order fulfillment" and state its responsibilities and boundaries.
2. Define the internal modules and the order state model with allowed transitions.
3. Write the sequence flow for the happy path from payment captured to carrier booked.
4. **Planned mistake:** stop at the happy path. Fix: add failure cases (ERP down, carrier rejects, duplicate payment event) with retry limits, idempotency keys, and customer messages.
5. Add the interface contracts used and the non-functional specifics (volume at peak, timeouts).
6. Hand it to a role-played delivery lead and note every clarification asked; fix the LLD until none remain.
