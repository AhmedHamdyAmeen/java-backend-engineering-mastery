# SRC-018 · Security reviews — Lecture scripts

**Video:** 67 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-018-L01 · Security reviews engineers run themselves (10 min)
**Goal:** lead a security review of your own subsystem before the security team sees it.

**Key points**
- A review is a structured look at the design for ways it can be abused, done early when changes are cheap.
- Engineers know the data flows best; security teams add specialist depth and cross-system view.
- Scope the whole subsystem: APIs, internal calls, data stores, queues, admin tools, build pipeline, and secrets, not only the public API.
- Output: findings with severity, owners, and dates; not a pass or fail stamp.

**Show** Review agenda: system overview, assets and trust boundaries, threats, authorization, data protection, operations (logging, secrets), findings and actions.

**Check:** Why review before the security team does? *(Cheaper changes, better-prepared discussion, and shared ownership of risk.)*

---

## SRC-018-L02 · Threat modeling at subsystem scale (12 min)
**Goal:** model threats in a way that fits a real subsystem.

**Key points**
- Four questions: what are we building, what can go wrong, what will we do about it, did we do a good job.
- Draw a data flow diagram with trust boundaries; walk each flow and store with a prompt list such as STRIDE (spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege).
- Adapt a checklist to the system: payments, personal data, multi-tenant data, messages, AI components.
- Keep the model alive: update on design changes.

**Show** Data flow description: client to gateway to orders service to database and payment provider, with Kafka between services; trust boundaries at the gateway and at the provider; table of threats per boundary.

**Check:** What does STRIDE give you? *(A set of prompts for categories of threats to look for.)*

---

## SRC-018-L03 · Authorization boundaries end to end (12 min)
**Goal:** verify that every path to data checks who may do what.

**Key points**
- Authentication says who; authorization says what they may do on which object.
- Check each path: public API, internal service calls (do not trust a call merely because it is internal), message consumers, batch jobs, admin tools, direct database access.
- Common failures: object-level access (change an ID and see another customer's order), missing checks on internal endpoints, over-broad service credentials, confused deputy.
- Propagate identity and enforce at the data layer; test negative cases.

**Show** Matrix: path | caller identity | check performed | where enforced | test. Example row: *GET /orders/{id} | customer token | order.customerId equals subject | orders service | cross-customer test.*

**Check:** Why test by changing an object ID? *(To detect missing object-level authorization.)*

---

## SRC-018-L04 · Risk rating and acceptance (10 min)
**Goal:** rate findings and agree what to do about each.

**Key points**
- Risk is likelihood times impact; rate each on a small scale with a stated rationale.
- Responses: mitigate, transfer, avoid, or accept; acceptance is a decision by someone with authority, not silence.
- Every finding gets an owner, a due date, and a tracked item; accepted risks get an expiry for re-review.
- Be consistent so ratings are comparable across reviews.

**Show** Findings table: ID | description | likelihood | impact | rating | response | owner | due. Example: missing rate limit on login; likelihood high, impact medium; mitigate.

**Check:** What must an accepted risk have? *(A named owner with authority, a rationale, and a review date.)*

---

## SRC-018-L05 · Working with security teams (8 min)
**Goal:** collaborate as peers rather than treat security as a gate.

**Key points**
- Bring a prepared package: diagrams, data classification, what you already found.
- Ask for their threat knowledge and standards early; agree the review process up front.
- Disagree with evidence; escalate with options, not ultimatums.
- Make secure paths easy: shared libraries, templates, automated checks.
- Share outcomes so patterns improve across teams.

**Show** Pre-review package list and a short working agreement: response times, severity definitions, escalation path.

**Check:** What is better than waiting for a gate at the end? *(Engaging early with a prepared package and shared checklist.)*

---

## SRC-018-L06 · Demo: reviewing the redesigned order subsystem (15 min)
**Goal:** run a design review end to end on the running case; prepares SRC-018-LAB1.

**Steps**
1. Draw the redesigned data flow with trust boundaries: gateway, orders, payments adapter, Kafka, database, admin tool.
2. Walk each flow with STRIDE prompts and record threats.
3. Build the authorization matrix and test cross-customer access on internal endpoints.
4. **Planned mistake:** review only the public API. Fix: include internal calls, consumers, and the admin tool, where a missing check is found.
5. Rate each finding, assign owners and dates, and mark one accepted risk with an expiry.
6. Write the summary and agree actions with the role-played security lead.

**Check:** Where was the missing check found? *(On a path other than the public API, such as an internal or admin path.)*
