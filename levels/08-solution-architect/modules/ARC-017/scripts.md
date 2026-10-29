# ARC-017 · Identity architecture — Lecture scripts

**Video:** 87 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-017-L01 · Identity as the new perimeter (8 min)
**Goal:** explain why identity is the main security boundary in cloud systems.

**Key points**
- Services are reachable from many places; the network no longer separates inside from outside.
- Every request should answer: who is calling, what may they do, from what context.
- Four identity populations: workforce, customers, partners, workloads (software).
- Strong identity with least privilege limits damage when something is compromised.
- Network controls remain useful but do not replace identity (ARC-018).

**Show:** a diagram of the four populations on the left and Larkspur resources on the right, with an access decision point in between.

**Check:** Name the four identity populations. *(Workforce, customers, partners, workloads.)*

---

## ARC-017-L02 · Workforce identity and SSO (12 min)
**Goal:** design single sign-on for employees with the corporate directory.

**Key points**
- One identity provider (IdP) holds employee identities; applications trust it for sign-in (SSO).
- Federate with the existing corporate directory instead of creating new accounts.
- Multi-factor authentication (MFA) everywhere, with stronger factors for admins.
- Joiner-mover-leaver processes: access removal on departure must be automatic.
- Provide emergency (break-glass) access, stored securely and monitored.

**Show:** flow: employee, IdP login with MFA, token, application; the corporate directory as the source of identities.

**Check:** Why automate leaver processing? *(So access is removed on time without relying on manual steps.)*

---

## ARC-017-L03 · Federation: SAML, OAuth 2.0, OIDC (14 min)
**Goal:** choose the right protocol per integration.

**Key points**
- SAML: XML-based sign-in standard, common for enterprise SaaS and older apps.
- OAuth 2.0: delegated authorization: an app gets limited access to an API on a user's behalf; it is not itself a sign-in protocol.
- OpenID Connect (OIDC): sign-in layer on top of OAuth 2.0, using JSON tokens; the default for new web and mobile apps.
- Choose by what the integration supports: SaaS that only speaks SAML gets SAML; new apps and APIs use OIDC and OAuth 2.0.
- Mobile apps use the authorization code flow with PKCE; no secrets in the app.

**Show:** a decision table: integration, protocol, reason (staff SSO to SaaS HR tool: SAML; mobile app login: OIDC; partner API access: OAuth 2.0 client credentials).

**Check:** Which protocol is built for sign-in on top of OAuth 2.0? *(OpenID Connect.)*

---

## ARC-017-L04 · Customer identity (12 min)
**Goal:** design customer identity (CIAM) without building it from scratch.

**Key points**
- Needs: registration, login, social login, password reset, account recovery, MFA options, consent and privacy controls.
- Buy or use a managed CIAM service before building; in-house login is a security and maintenance burden.
- Account recovery is the weak point attackers use; design it carefully.
- Privacy: collect minimal data, record consent, support deletion and export.
- Single customer identity across web, mobile, and in-store loyalty.

**Show:** diagram: web and mobile apps to the CIAM service, which federates social providers and issues tokens to the platform APIs.

**Check:** Why avoid building login in-house without a need? *(It adds security risk and maintenance for no differentiating value.)*

---

## ARC-017-L05 · Cloud IAM for people and workloads (12 min)
**Goal:** design least-privilege cloud IAM.

**Key points**
- People get roles through the IdP, with just-in-time elevation for admin tasks; no shared accounts.
- Workloads get identities (roles) with short-lived credentials from the platform; avoid long-lived access keys.
- Write policies with least privilege and review them regularly.
- Separate duties: those who deploy to prod differ from those who approve.
- Break-glass accounts: few, protected, alerting on use.

**Show:** a policy sketch for the order service: read the orders queue, write to one bucket path, nothing else.

**Check:** What replaces long-lived access keys for workloads? *(Platform-issued roles with short-lived credentials.)*

---

## ARC-017-L06 · Demo: Larkspur's identity architecture end to end (15 min)
**Goal:** assemble the identity design across all four populations for `ARC-017-LAB1`.

**Steps**
1. Workforce: corporate directory federated to a cloud IdP with MFA; SSO to the back office and cloud console.
2. Customers: a managed CIAM service with social login for web and mobile, using OIDC with PKCE.
3. Partners: supplier portal access through federation where the partner has an IdP, otherwise managed accounts with MFA; partner APIs through OAuth 2.0 client credentials.
4. Workloads: roles with least-privilege policies; no access keys.
5. **Planned mistake:** a shared "admin" account for the cloud console. Fix: named users with just-in-time admin roles and a monitored break-glass account.
6. Draw the end-to-end diagram and record each protocol choice with its reason.

---

## ARC-017-L07 · Demo: SSO for store staff into the new back office (14 min)
**Goal:** design SSO for store staff, including shared devices and turnover.

**Steps**
1. Context: 120 stores, shift workers on shared tills, high turnover, some without corporate email.
2. Choose: back office as an OIDC client of the workforce IdP; role claims mapped from directory groups (store manager, cashier, head office).
3. Handle shared devices: short sessions, per-user login, MFA suited to store use (badge or app); no shared logins.
4. **Planned mistake:** one shared login per store "for speed". Fix: individual accounts, fast badge-based sign-in, and audit trail per person.
5. Automate joiner and leaver from the HR system.
6. Define break-glass for IdP outage: how a store keeps operating (links to ARC-019).

---
