# SRB-010 · Platform engineering — Lecture scripts

**Video:** 84 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-010-L01 · Why platform teams exist (10 min)
**Goal:** recognize the repeated toil that justifies a platform team.

**Key points**
- Product teams repeat the same setup: pipelines, observability, security, deployment.
- A platform team removes repeated work and lowers cognitive load.
- A platform is justified by multiple teams with the same need.
- Signs of need: slow onboarding, inconsistent services, copy-pasted scripts.

**Show:** a toil inventory table: task, teams doing it, hours per quarter, candidate for platform.

**Check:** What justifies a platform capability? *(Several teams repeat the same work.)*

---

## SRB-010-L02 · Platform as a product (12 min)
**Goal:** treat teams as customers.

**Key points**
- Know your users: interview, observe, and measure.
- Have a roadmap, support, and documentation like a product.
- Adoption is earned by value, not mandated.
- Say no to custom requests that serve one team only.

**Show:** a product canvas: users (four FulfillCo teams), jobs to be done, first capability, success metrics, support model.

**Check:** How is adoption earned? *(By solving real problems better than the alternative.)*

---

## SRB-010-L03 · Golden paths (10 min)
**Goal:** offer a supported, easy default route.

**Key points**
- A golden path is the paved road: template, pipeline, defaults, docs.
- Teams may leave it but then own more.
- It encodes good practice, such as telemetry and security scans.
- Keep it small and kept up to date.

**Show:** a golden path checklist: repo template, CI, deploy, dashboards, SLO file, runbook skeleton.

**Check:** What if a team leaves the golden path? *(It may, but takes on more responsibility.)*

---

## SRB-010-L04 · Self-service with guardrails (12 min)
**Goal:** let teams act without tickets, safely.

**Key points**
- Self-service via templates, portals, or APIs; no waiting for a person.
- Guardrails: policy checks, quotas, and defaults rather than approvals.
- Escape hatches for unusual needs with clear ownership.
- Automate the common 80% first.

**Show:** an example flow: a team requests a database through a form; the platform applies sizing defaults, backups, and encryption; a policy blocks public access.

**Check:** What do guardrails replace? *(Manual approvals.)*

---

## SRB-010-L05 · Measuring a platform (10 min)
**Goal:** measure whether the platform helps.

**Key points**
- Adoption: share of services on the golden path.
- Developer experience: surveys and time to first deploy.
- Delivery metrics: lead time and deployment frequency.
- Avoid vanity metrics; pair numbers with interviews.

**Show:** a scorecard: adoption %, time to staging for a new service, survey score, tickets avoided.

**Check:** Name one platform metric. *(Time for a new service to reach staging, or adoption rate.)*

---

## SRB-010-L06 · Demo: a service template that ships with CI, telemetry, and SLOs (15 min)
**Goal:** build the template for new FulfillCo services.

**Steps**
1. Create a repo template with build, tests, and container image.
2. Add pipeline steps: scan, deploy to staging, and smoke test.
3. Pre-wire telemetry and a default SLO and dashboard.
4. **Planned mistake:** hard-code Shop-specific settings into the template; fix by using parameters and defaults.
5. Time a new service from template to staging.

Prepares SRB-010-LAB1.

---

## SRB-010-L07 · Demo: interviewing teams to find the platform's first capability (15 min)
**Goal:** discover the first platform capability from user evidence.

**Steps**
1. Prepare questions about the last time each team shipped a service.
2. Interview the four teams (role-played) and record pain points.
3. Cluster the pain points and count teams affected.
4. **Planned mistake:** build the capability the loudest team requested; fix by ranking on teams affected and hours saved.
5. Write a one-page capability proposal.

Prepares SRB-010-LAB1.

---
