# SRB-016 · Security architecture — Lecture scripts

**Video:** 86 min · **Running case:** *The FulfillCo integration* — the engineer leads the four-team program planned in SRB-P1 through delivery; role-players act as team leads, product, finance, and security.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-016-L01 · Security architecture vs security features (10 min)
**Goal:** separate structural security decisions from individual controls.

**Key points**
- Features are controls added to one service (input validation, a login page); architecture decides where trust boundaries sit and how identity flows.
- Architecture decisions are costly to change later, so they need design attention early.
- Merging two organizations brings two identity systems, two trust models, and unknown assumptions.
- Start from assets and threats: what must be protected, from whom, and what happens if one component is breached.

**Show** A diagram description: two organizations (Shop, FulfillCo) with their own user stores, services, and a partner path; circle the trust boundaries and mark where the two models meet.

**Check:** Why is security architecture decided early? *(It fixes boundaries and identity flows that are expensive to change later.)*

---

## SRB-016-L02 · Identity boundaries (12 min)
**Goal:** define identity for users, services, and partners across the merged organizations.

**Key points**
- Three identity types: people (customers, staff), workloads (services), and partners (external systems); each has its own lifecycle and credentials.
- Decide the authority for each type: one identity provider for staff, a workload identity system for services, a partner onboarding process.
- Federation lets one provider trust another without merging user stores; plan it before consolidation.
- Separate authentication (who) from authorization (what they may do).

**Show** Table: identity type | authority | credential form | lifecycle | who can revoke. Example: *service | workload identity issuer | short-lived token | tied to deployment | platform team.*

**Check:** Why separate authentication from authorization? *(Knowing who a caller is does not decide what they may do.)*

---

## SRB-016-L03 · Zero trust in practice (12 min)
**Goal:** apply zero-trust principles to a real system.

**Key points**
- Do not trust network location; authenticate and authorize every request, including internal ones.
- Assume breach: limit what a compromised service can reach, and make activity visible.
- Use least privilege, short-lived credentials, and segmentation.
- Zero trust is a direction applied in steps, not a product to buy; start with the highest-value paths.

**Show** Before and after table: *internal call with no authentication, trusted by subnet* versus *call with workload identity, scoped token, audit log.* Prioritize paths by data sensitivity.

**Check:** What does "assume breach" change in design? *(You limit blast radius and add detection instead of relying on a perimeter.)*

---

## SRB-016-L04 · Service-to-service authorization (12 min)
**Goal:** choose mechanisms for service identity and authorization.

**Key points**
- Workload identity: each service gets its own identity issued by the platform (for example SPIFFE-style identities); verify which standard and tooling you use before recording.
- mTLS authenticates both ends and encrypts traffic; a service mesh can automate certificate rotation.
- Scoped tokens carry what a caller may do (audience, scopes), kept short-lived.
- Authorization decides at the callee: allow-lists of caller identities per endpoint, with business rules in a policy layer.
- Avoid shared credentials between teams; one service, one identity.

**Show** An authorization matrix: caller identity | endpoint or event topic | action allowed. Example: *fulfillment-service may read Shop order events; may not read payment data.*

**Check:** Why avoid shared credentials between teams? *(You cannot tell who did what, and a leak exposes every user of the credential.)*

---

## SRB-016-L05 · Policy as code (10 min)
**Goal:** express access rules as versioned, tested code.

**Key points**
- Policy engines evaluate rules (who may do what) separately from application code.
- Policies live in version control, are reviewed like code, and are tested with allow and deny cases.
- Central policies give consistency; local enforcement gives speed; decide which decisions are centralized.
- Make decisions auditable: log the input, decision, and policy version.
- Verify engine and syntax before recording.

**Show** A policy in words and a test table: *allow if caller role = fulfillment and action = read and resource type = order-event; deny otherwise.* Test rows with expected decisions.

**Check:** Why test policies with deny cases? *(To prove they block what they should, not only allow what they should.)*

---

## SRB-016-L06 · Demo: authorizing FulfillCo services to Shop events and APIs (15 min)
**Goal:** design access for FulfillCo services to consume Shop events and call Shop APIs with least privilege; prepares SRB-016-LAB1.

**Steps**
1. List the FulfillCo services and the Shop data and endpoints each needs.
2. Assign each service a workload identity and define the allowed topics and endpoints in a matrix.
3. Issue scoped, short-lived tokens or mTLS identities; define audiences and scopes.
4. **Planned mistake:** grant a broad read scope because "they might need it later". Fix: grant exactly what is used and add a request process for more.
5. Write policy tests for allow and deny cases and enable audit logging.
6. Walk the review with the role-played security architect and record findings.

**Check:** What is the rule for scope design? *(Grant only what is needed now, with a documented route to ask for more.)*

---

## SRB-016-L07 · Demo: replacing network-based trust with workload identity (15 min)
**Goal:** remove a rule that trusts anything inside the network and replace it with identity checks; prepares SRB-016-LAB1.

**Steps**
1. Find the rule: the stock service accepts any call from the internal subnet.
2. Inventory callers using traffic logs, so you know who relies on it.
3. Issue workload identities to the callers and add authentication in report-only mode.
4. **Planned mistake:** switch to enforce mode at once and break an unlisted caller. Fix: watch the report-only results, fix gaps, then enforce with a rollback path.
5. Remove the network allow rule and verify an unauthenticated call is denied.
6. Record the change and monitor denials.

**Check:** Why start in report-only mode? *(It shows unknown callers before enforcement breaks them.)*
