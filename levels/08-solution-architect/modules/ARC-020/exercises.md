# ARC-020 · Infrastructure governance — Exercises and lab

## Lab
### ARC-020-LAB1 · Larkspur landing zone
**Outcomes:** 1–4 · **Time:** ~3 h (one provider; verify service names before recording)
1. Design the account/subscription hierarchy.
2. Define baseline networking, central logging, and security services.
3. Write guardrail policies, marking each preventive or detective.
4. Define the tagging standard and its enforcement.
5. Define the IaC workflow with review and policy checks.
6. Walk through a non-compliant resource being blocked or detected.
**Acceptance:** a non-compliant resource is blocked or detected in a walkthrough.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-020-EX01 | 1 | Explain to a delivery manager why the landing zone is built before the first workload. |
| ARC-020-EX02 | 1 | Draw a hierarchy for Larkspur with five groups and state which policy applies at each level. |
| ARC-020-EX03 | 2 | Write six guardrails and classify them as preventive or detective. |
| ARC-020-EX04 | 3 | Define the mandatory tag set and how each tag is enforced. |
| ARC-020-EX05 | 4 | Describe the IaC workflow for a networking change in prod. |
| ARC-020-EX06 | 4 | A team requests console access to fix prod quickly. Write the policy response with an exception path. |

## Solutions
- **EX01** Guardrails retrofitted onto live workloads cost more and carry risk; teams start faster in a prepared structure; inconsistent setups multiply security and cost problems.
- **EX02** Root; Security (log archive, tooling); Shared network; Workloads with Prod and Non-prod; Sandbox with budget limits. Policies: region and logging at root; production strictness at Prod; spending limit at Sandbox.
- **EX03** Preventive: deny unapproved regions, deny public data stores, require encryption, block disabling of logging. Detective: untagged resources, drift from IaC, overly broad roles.
- **EX04** Owner, cost center, environment, application, data classification; require at creation by policy or pipeline check, detect missing tags with weekly report and owner follow-up.
- **EX05** Pull request, peer review, static policy checks, plan output reviewed, approval, pipeline apply with a deploy role, drift check afterwards.
- **EX06** Default is no write access; fixes go through the pipeline with an expedited review path; break-glass role with logging, approval, and expiry; follow-up to codify the fix.

**Workplace evidence:** a landing zone or guardrail set you designed.

---
Outcome coverage: all outcomes covered by exercises and the lab.
