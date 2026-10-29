# ARC-025 · API management — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-025-L01 · APIs as products (10 min)
**Goal:** explain what changes when an API is treated as a product.

**Key points**
- A product has an owner, consumers, documentation, a roadmap, and support.
- Consumers are customers: partners, the mobile team, other internal teams; their needs shape the API.
- Measure use: active consumers, errors, time to first successful call.
- Breaking a consumer without notice is a product failure, not just a technical one.

**Show:** an API product card for Larkspur's Catalog API: owner, consumers, support channel, SLA, version, deprecation policy.

**Check:** What does a product owner do that a service owner may not? *(Manages consumers, roadmap, documentation, and change communication.)*

---

## ARC-025-L02 · What API management platforms provide (12 min)
**Goal:** list the capabilities of API management and decide whether a solution needs it.

**Key points**
- Gateway: single entry, authentication, rate limits, routing, and logging.
- Developer portal: documentation, self-service sign-up, and keys.
- Keys, quotas, and plans: who may call what and how much.
- Analytics: traffic, errors, and usage per consumer.
- A small internal system with few consumers may not need it; many consumers or external partners usually do.

**Show:** a table of capabilities against Larkspur consumers (mobile app, marketplace partners, store systems) with "needed now / later / not needed".

**Check:** When is API management probably unnecessary? *(One internal consumer and low risk; a plain gateway or none may do.)*

---

## ARC-025-L03 · API governance and lifecycle (12 min)
**Goal:** design governance that guides teams without blocking them.

**Key points**
- Style guide: naming, errors, pagination, and security defaults so APIs feel alike.
- Review: a light design review before publishing, with automated linting where possible.
- Versioning: define what counts as breaking and how long old versions live.
- Lifecycle: draft, active, deprecated, retired, with dates and notice periods.
- A gateway without governance only centralizes inconsistency.

**Show:** a lifecycle diagram with notice periods (verify with partner contracts) and a checklist the review board uses.

**Check:** What is a breaking change? *(One that makes a correct existing consumer fail, such as removing a field or changing its meaning.)*

---

## ARC-025-L04 · Quotas, keys, and consumer tiers (10 min)
**Goal:** set access tiers and limits by consumer type.

**Key points**
- Internal, partner, and public consumers differ in trust, volume, and support.
- Quotas protect shared systems; set them from capacity and contract, and monitor.
- Separate keys per consumer allow revocation and usage reports.
- Tiers can differ in rate, data fields, and support level.

**Show:** a tier table: internal (high limits, service identity), partner (contracted limit, key plus OAuth client), public (low limit, read-only catalog, no personal data).

**Check:** Why not one quota for everyone? *(A small client would be overserved and a large partner starved, and abuse is hard to isolate.)*

---

## ARC-025-L05 · Demo: designing Larkspur's partner API program (14 min)
**Goal:** design the program for marketplace partners and the mobile app; prepares ARC-025-LAB1.

**Steps**
1. Identify consumers: mobile app, three marketplace partners, a price-comparison site.
2. Define APIs as products: Catalog, Stock availability, Order submission; each with an owner and SLA.
3. Create tiers and quotas from backend capacity, with burst limits and a clear error for exceeded limits.
4. **Planned mistake:** launch with one quota for all and no deprecation policy. Fix: separate tiers and a written policy with a notice period and sunset dates.
5. Design onboarding through a developer portal: sign-up, sandbox, keys, first-call guide, and approval for production.
6. Review with a role-played partner manager and security lead; record their objections.
