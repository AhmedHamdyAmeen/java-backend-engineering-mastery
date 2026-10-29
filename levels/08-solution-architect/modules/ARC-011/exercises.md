# ARC-011 · Cloud service models — Exercises and lab

## Lab
### ARC-011-LAB1 · Service-model matrix
**Outcomes:** 1–3 · **Time:** ~2.5 h
1. List every Larkspur component (storefront, order service, search, payments, databases, media, email, identity, monitoring, ERP adapter, reporting).
2. Choose IaaS, PaaS, SaaS, or managed service for each, with a one-line reason.
3. Fill a "who operates what" table: provider, Larkspur team, vendor, per concern (patching, scaling, backup, security, incident response).
4. Add lock-in kind and exit consideration for each choice.
5. Highlight responsibility gaps and assign an owner to each.
**Acceptance:** responsibility gaps identified and assigned.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-011-EX01 | 1 | Larkspur proposes running its own database on VMs. List what its team would operate that a managed database removes. |
| ARC-011-EX02 | 1 | Classify five tools Larkspur uses (CRM, payment gateway, container platform, VM, managed queue) as IaaS, PaaS, SaaS, or managed service. |
| ARC-011-EX03 | 2 | For the SaaS CRM, write the shared-responsibility split for identity, data, availability, and incident response. |
| ARC-011-EX04 | 2 | A bucket of product invoices was exposed by a configuration error. Whose responsibility is that, and which controls prevent it? |
| ARC-011-EX05 | 3 | The platform lead wants "full control" with VMs for all services. Write a short note recommending a service model for the order service. |
| ARC-011-EX06 | 3 | Write an exit assessment for the managed search service: lock-in kind, exit effort, mitigation. |

## Solutions
- **EX01** OS and engine patching, backup jobs and restore tests, failover setup, replication, disk growth, monitoring agents; they would still own schema, access, and tuning.
- **EX02** CRM: SaaS; payment gateway: SaaS; container platform: PaaS (or managed service); VM: IaaS; managed queue: managed service.
- **EX03** Vendor: platform availability, infrastructure security. Larkspur: user accounts, SSO, roles, data classification and export rights, deciding the response to a data issue. Incident response is shared with a defined contact path.
- **EX04** Customer side: configuration is always the customer's. Controls: block public access by default, policy guardrails, access reviews, detective checks for public buckets.
- **EX05** Recommend managed containers or PaaS: the team is small, workload is standard, no OS-level need. Control gained from VMs is unused; operating burden and patch risk grow. State when VMs would be justified.
- **EX06** Lock-in: query API and index format. Exit: re-index from the source database in weeks. Mitigation: source of truth stays in the relational store; abstract search behind an internal interface only where cheap.

**Workplace evidence:** a service-model decision that reduced operational burden.

---
Outcome coverage: all outcomes covered by exercises and the lab matrix.
