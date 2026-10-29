# ARC-018 · Network security — Lecture scripts

**Video:** 64 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-018-L01 · Defense in depth for networks (10 min)
**Goal:** layer network controls so one failure does not expose everything.

**Key points**
- Layers: edge protection, perimeter filtering, segmentation, host-level rules, and identity checks inside.
- Assume any single layer will eventually fail or be misconfigured.
- Deny by default; open only what is needed, for as few sources as possible.
- Log at each layer to detect and investigate.
- Network controls complement identity-based controls; they do not replace them.

**Show:** concentric rings: CDN and DDoS protection, WAF, load balancer, service firewall, data tier rules, with identity checks across all of them.

**Check:** Can the network perimeter alone protect the platform? *(No; identity and per-service controls are also needed.)*

---

## ARC-018-L02 · Security groups, firewalls, and WAF (12 min)
**Goal:** know what each control does and where it sits.

**Key points**
- Security groups / network security groups (NSGs): stateful allow rules per resource or subnet; the first line of in-network control.
- Network firewalls: central inspection for egress filtering and east-west rules; costs money and is a choke point.
- Web application firewall (WAF): inspects HTTP for common attacks and abusive clients; sits in front of public endpoints.
- Reference security groups by other groups rather than raw IPs where supported.
- Egress control: limit outbound traffic to what is needed to reduce data exfiltration paths.

**Show:** a rule table for the order service: inbound only from the load balancer on one port; outbound only to the database and the ERP adapter.

**Check:** Which control inspects HTTP traffic for attack patterns? *(The WAF.)*

---

## ARC-018-L03 · Segmentation (10 min)
**Goal:** separate networks by sensitivity and environment.

**Key points**
- Segment by environment (prod, non-prod), by tier (web, app, data), and by sensitivity (payment components).
- Flat networks let an attacker move anywhere after one foothold.
- Segmentation also reduces compliance scope: smaller sensitive zone, smaller audit.
- Define allowed flows between segments; everything else is denied.
- Test segmentation as an assumption, not a belief.

**Show:** a flow matrix: rows are source segments, columns are destinations, cells are allowed ports or "deny".

**Check:** Why do flat networks increase risk? *(One compromised host can reach everything.)*

---

## ARC-018-L04 · DDoS and edge protection (10 min)
**Goal:** protect public endpoints from volumetric and application-layer attacks.

**Key points**
- Use the provider's DDoS protection and a CDN to absorb volume at the edge.
- WAF rate limiting and bot controls handle application-layer floods and scraping.
- Hide origins: accept traffic to the origin only from the CDN or load balancer.
- Plan capacity and autoscaling limits so an attack does not become a cost attack.
- Have an incident playbook with contacts; verify tiers and features before recording.

**Show:** a chain: DNS, CDN with DDoS protection, WAF with rate limits, load balancer, application, with the origin locked to the CDN.

**Check:** Why restrict the origin to the CDN? *(So attackers cannot bypass edge protection.)*

---

## ARC-018-L05 · Private connectivity to SaaS and partners (8 min)
**Goal:** connect to SaaS and partners without exposing data to the open internet.

**Key points**
- Options: private endpoint to a provider-hosted service, dedicated link or VPN to a partner, allow-listed source addresses.
- Prefer private connectivity for sensitive flows (payments, ERP, partner data).
- When only the internet is available, combine TLS, mutual authentication, and IP allow-lists.
- Agree who runs and monitors each link, and what happens on failure.
- Document each external connection in an inventory.

**Show:** a table: external party, data exchanged, connection type, authentication, owner, failure behavior.

**Check:** What do you do if only an internet path to a partner exists? *(Use TLS, strong authentication, and allow-lists.)*

---

## ARC-018-L06 · Demo: protecting Larkspur's storefront and payment paths (14 min)
**Goal:** apply layered controls to the storefront and isolate payment flows, preparing `ARC-018-LAB1`.

**Steps**
1. List public endpoints: web storefront, mobile API, back-office portal, webhook receiver for the payment provider.
2. Edge: CDN with DDoS protection, WAF with managed rules and rate limits on login and checkout; origin restricted to the edge.
3. Segment: payment-related components in their own segment with tight flows and egress only to the payment provider.
4. Back office: reachable only through SSO and restricted source networks, not open to the internet.
5. **Planned mistake:** the webhook receiver left unprotected "because the provider calls it". Fix: allow-list provider sources, verify signatures, and route through the WAF.
6. Record the flow matrix and the list of protected endpoints.

---
