# ARC-020 · Infrastructure governance — Lecture scripts

**Video:** 66 min · **Running case:** *Larkspur Retail* — a fictional 120-store retailer replacing its dated on-premises web shop with a web and mobile platform (inventory, payments, fulfillment, customer service, reporting) integrated with the existing ERP and CRM. You are the solution architect.
Format: **Goal** · **Key points** · **Show** · **Check**.
Provider note: landing-zone products and policy services differ by provider; verify names and features before recording.

---

## ARC-020-L01 · Why landing zones exist (10 min)
**Goal:** explain why a landing zone should exist before workloads arrive.

**Key points**
- A landing zone is the prepared foundation: account structure, networking, identity, logging, security baseline, and guardrails.
- Without it, each team builds its own, producing inconsistent security and cost.
- Retrofitting guardrails onto live workloads is slow and risky.
- It gives teams a safe, fast way to start: self-service within boundaries.
- Keep it small and evolve it; it is a product with an owner.

**Show:** a diagram: organization root, baseline services (logging, security, network), and workload accounts created from a template.

**Check:** When should guardrails be added? *(Before workloads go live, not after.)*

---

## ARC-020-L02 · Account and subscription hierarchies (12 min)
**Goal:** design the hierarchy that policy and billing follow.

**Key points**
- Group accounts into folders or management groups by purpose (workloads, shared, security, sandbox).
- Policies and permissions inherit down the tree; design the tree for the policy you need.
- Dedicated accounts for central logging, security tooling, and shared network.
- Separate prod from non-prod; give each team a boundary with a budget.
- Keep the tree shallow; deep hierarchies are hard to reason about.

**Show:** a tree diagram: root, Security, Shared services, Workloads (Prod, Non-prod), Sandbox, with policies noted at each level.

**Check:** Why design the hierarchy around policy? *(Policies inherit down the tree, so structure decides where they apply.)*

---

## ARC-020-L03 · Policy guardrails (12 min)
**Goal:** enforce rules with preventive and detective controls.

**Key points**
- Preventive guardrails block non-compliant actions (deny public buckets, deny unapproved regions, require encryption).
- Detective guardrails find drift after the fact and alert or remediate.
- Use preventive for clear rules, detective where blocking would be too disruptive.
- Provide an exception process with an owner and an expiry.
- Treat policies as code: versioned, reviewed, and tested.

**Show:** a table: rule, type (preventive or detective), scope, exception path (for example: deny resources outside approved regions, preventive, organization-wide).

**Check:** What is the difference between preventive and detective guardrails? *(Preventive blocks the action; detective finds and reports it afterwards.)*

---

## ARC-020-L04 · Tagging standards (8 min)
**Goal:** define tags for ownership, cost, and data classification, and enforce them.

**Key points**
- Mandatory tags: owner, cost center, environment, application, data classification.
- Tags drive cost reports, access decisions, and incident response.
- Tags without enforcement decay; require them at creation or detect missing tags.
- Keep the set small and the values controlled.
- Verify tag support per service before recording.

**Show:** a tag table: key, allowed values, who sets it, enforcement method.

**Check:** Why enforce tags? *(Unenforced tags become incomplete and cost and ownership reports become unreliable.)*

---

## ARC-020-L05 · Infrastructure as code as governance (10 min)
**Goal:** require reviewed infrastructure as code (IaC) for every environment.

**Key points**
- Infrastructure defined as code is versioned, reviewable, and repeatable.
- Changes go through pull request, review, automated checks, and a pipeline; manual console changes are blocked or detected.
- Policy checks run in the pipeline before deployment.
- Drift detection compares reality to code.
- Separate roles: pipeline deploys to prod; people have read access by default.

**Show:** a pipeline: pull request, review, static policy checks, plan, approval, apply, drift check.

**Check:** Why restrict console changes in prod? *(They bypass review and cannot be reproduced or audited easily.)*

---

## ARC-020-L06 · Demo: Larkspur's landing zone design (14 min)
**Goal:** design Larkspur's landing zone and show a non-compliant resource being stopped, preparing `ARC-020-LAB1`.

**Steps**
1. Draw the hierarchy: Security, Shared network, Workloads (prod, non-prod), Sandbox with budget.
2. Define guardrails: approved regions only, no public data stores, encryption required, mandatory tags, logging cannot be disabled.
3. Define the tag standard and central logging to the security account.
4. Define the IaC workflow with review and policy checks.
5. **Planned mistake:** a developer creates an unencrypted public bucket in the console during the walkthrough. Show the preventive policy deny it, and the detective rule flag an existing one.
6. Record exceptions process and the owner of the landing zone.

---
