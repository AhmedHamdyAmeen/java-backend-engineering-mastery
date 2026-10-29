# ARC-027 · Identity and access — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-027-L01 · Authorization models: RBAC and ABAC (12 min)
**Goal:** choose between role-based and attribute-based access control, or combine them.

**Key points**
- RBAC: permissions attach to roles, people get roles; simple to explain and audit.
- ABAC: decisions use attributes of the user, resource, and context, such as "store manager of the same store".
- Pure RBAC leads to role explosion when rules depend on store, region, or time.
- A common design: coarse roles plus attribute rules for scope.

**Show:** a table comparing RBAC and ABAC with the Larkspur rule "a store manager sees returns only for their own store" implemented as role StoreManager plus attribute storeId equal.

**Check:** Why does role explosion happen? *(Every combination of scope and permission becomes its own role, such as "Manager-Store-014".)*

---

## ARC-027-L02 · Identity federation (12 min)
**Goal:** design how enterprise, partner, and customer identities trust each other.

**Key points**
- Federation: one system trusts another's login, using standards such as OpenID Connect or SAML.
- Workforce identity comes from the enterprise directory; partners federate their own directory or get managed accounts; customers use a customer identity service.
- Keep the three populations separate: different risk, volume, and lifecycle.
- Map external identities and claims to local roles through a clear, reviewed rule.

**Show:** a diagram with three identity sources (directory, partner IdPs, customer IdP) feeding one token service that issues tokens to the platform, with claim mapping at the arrows.

**Check:** Why keep customer and workforce identities separate? *(Different threats, scale, lifecycle, and rules; mixing them widens the attack surface.)*

---

## ARC-027-L03 · Privileged access (10 min)
**Goal:** control administrators and operators with the smallest powers for the shortest time.

**Key points**
- Privileged accounts are separate from daily accounts and never shared.
- Just-in-time access: elevated rights granted on request, approved, and expiring.
- Strong authentication and session recording for production and for secrets stores.
- Break-glass accounts for emergencies are sealed, monitored, and reviewed after use.

**Show:** a flow: engineer requests production access with a ticket, approver grants two hours, session logged, access expires, review next day.

**Check:** What is wrong with a shared admin account? *(Actions cannot be traced to a person, and removal of one person's access is impossible.)*

---

## ARC-027-L04 · Joiners, movers, leavers, and access reviews (10 min)
**Goal:** define the lifecycle processes that keep access correct over time.

**Key points**
- Joiner: access arrives with role, ideally automatic from the HR system.
- Mover: change of role removes old access, not just adds new.
- Leaver: all access removed on the last day; partner and contractor accounts expire by default.
- Access reviews: owners confirm periodically who still needs what; unreviewed access is revoked.

**Show:** a table of triggers (HR event, contract end) and actions per process, with review frequency by risk (verify frequency against company policy).

**Check:** What does the mover process most often miss? *(Removing the access of the old role.)*

---

## ARC-027-L05 · Demo: store managers, call-center agents, and partners in one access model (14 min)
**Goal:** build one access model for five user groups; prepares ARC-027-LAB1.

**Steps**
1. List user groups: head-office staff, store managers, customer-service agents, marketplace partners, customers.
2. Define coarse roles and the attributes that scope them: storeId, region, case ownership, partner ID.
3. Map federation: workforce from the directory, partners via their identity providers, customers via customer identity.
4. **Planned mistake:** create roles per store (120 manager roles). Fix: one StoreManager role with a storeId attribute check.
5. Design privileged access for platform operators with just-in-time rights and logged sessions.
6. Test with five representative users and show least privilege for each: what they can and cannot do.
