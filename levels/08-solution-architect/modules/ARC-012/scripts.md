# ARC-012 · Cloud architecture — Lecture scripts

**Video:** 75 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.
Provider note: lectures teach the provider-neutral principle first; provider service names, regions, and limits are marked "verify before recording".

---

## ARC-012-L01 · Regions, zones, and edge locations (10 min)
**Goal:** choose geography for latency, resilience, and data residency.

**Key points**
- A region is a geographic area; an availability zone (AZ) is an isolated data center group inside it; edge locations cache content near users.
- Spreading across AZs protects against a data center failure; spreading across regions protects against a regional one, at higher cost.
- Pick the region by user location, data-residency law, service availability, and price (verify before recording).
- Data residency decides where personal data may be stored and processed, not only where users are.
- Latency to the nearest region matters less once a content delivery network (CDN) serves static content.

**Show:** a map sketch: stores in one country, one primary region with three zones, a CDN at the edge, and a second region greyed out as the DR option.

**Check:** What does a second AZ protect against? *(Failure of one data center group, not a whole region.)*

---

## ARC-012-L02 · Reading reference architectures critically (12 min)
**Goal:** use provider reference architectures as starting points, not blueprints.

**Key points**
- Reference architectures show good patterns for generic workloads; they know nothing about your constraints.
- Ask of each component: which requirement does this serve? If none, remove it.
- Look for what is missing: your ERP, your compliance, your team's skills.
- Watch for scale and cost assumptions built into the diagram.
- Record what you adopted, adapted, and rejected, with reasons.

**Show:** a three-column sheet: Component | Requirement served | Adopt / Adapt / Reject.

**Check:** Why not copy a reference architecture wholesale? *(It was drawn for a generic workload and carries components and costs you may not need.)*

---

## ARC-012-L03 · Accounts, subscriptions, and environments (12 min)
**Goal:** structure accounts or subscriptions for isolation and blast-radius control.

**Key points**
- An account (or subscription) is a hard boundary for identity, billing, and quota.
- One account per environment (dev, test, prod) limits mistakes; separate accounts for security logging and shared networking.
- Blast radius: how far a mistake or compromise spreads; smaller boundaries mean smaller radius.
- Too many accounts without automation becomes burden; start with a small, clear split.
- Organization-level policies apply across all accounts (detail in ARC-020).

**Show:** a tree: organization, then folders for workloads, with accounts prod, non-prod, shared-network, security-logging, and a sandbox.

**Check:** Why separate prod from non-prod accounts? *(A mistake or leaked credential in test cannot touch production.)*

---

## ARC-012-L04 · A reference web/mobile commerce architecture (12 min)
**Goal:** read a typical commerce reference architecture end to end.

**Key points**
- Edge: DNS, CDN, WAF in front of web and mobile entry points.
- Application tier: stateless services behind a load balancer across zones.
- Data tier: managed relational store, cache, search, object storage for media.
- Asynchronous work: queues and events for orders, emails, and integrations.
- Cross-cutting: identity, secrets, logging, monitoring (verify service names before recording).

**Show:** a layered diagram with a dashed line marking the trust boundary between the internet and the platform, and another around the data tier.

**Check:** Where do trust boundaries belong on the diagram? *(Between the internet and the edge, and between the application and data tiers.)*

---

## ARC-012-L05 · Demo: Larkspur's target cloud architecture (15 min)
**Goal:** build the Larkspur target architecture diagram traced to requirements from `ARC-003-LAB1`.

**Steps**
1. Pull the requirements: availability target, data residency, peak season load, ERP integration, store connectivity.
2. Choose region and zones from residency and store locations; name the DR region as a later decision (ARC-019).
3. Draw the account structure: prod, non-prod, shared-network, security-logging.
4. Draw edge, application, data, and integration tiers with trust boundaries.
5. **Planned mistake:** place the ERP connector in the public subnet "for simplicity". Fix: it moves to a private tier with a controlled path to the data center.
6. Tag every element with the requirement ID it serves.

---

## ARC-012-L06 · Demo: adapting a reference architecture to Larkspur's constraints (14 min)
**Goal:** take a generic reference and adapt it, preparing the written part of `ARC-012-LAB1`.

**Steps**
1. Start from the provider's commerce reference diagram.
2. Remove: a global multi-region database (no requirement), a custom recommendation pipeline (out of scope).
3. Add: an ERP integration path, store-offline considerations, and a stock-sync queue.
4. Adapt: a single-region, three-zone footprint instead of multi-region, because the sponsor accepted a longer recovery time.
5. **Planned mistake:** keeping every reference component "in case". Fix: each box must name its requirement or go.
6. Write the adopt/adapt/reject log as a short decision record.

---
