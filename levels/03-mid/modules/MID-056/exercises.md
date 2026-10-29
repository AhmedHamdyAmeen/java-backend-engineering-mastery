# MID-056 · Cloud fundamentals — Exercises and lab

## Lab
### MID-056-LAB1 · Shop in the cloud
**Outcomes:** 1–4 · **Time:** ~3 h
In the console, create a VPC with public and private subnets across two AZs, a managed PostgreSQL in the private tier, an object storage bucket for product images, a load balancer, and a least-privilege role for `orders`. Write a monthly cost estimate. Tear the environment down afterwards; it is rebuilt with Terraform in MID-058.
**Acceptance:** database has no public endpoint; monthly cost estimate written.

## Exercises (assessment: architecture diagram review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-056-EX01 | 1 | Divide responsibilities between provider and you for a managed database and for a VM. |
| MID-056-EX02 | 1 | Choose a region and AZ layout for Shop with 99.9% availability; justify. |
| MID-056-EX03 | 2 | Draw the VPC with subnets, route tables, and security-group rules for Shop. |
| MID-056-EX04 | 3 | Write a least-privilege policy for `orders` to read and write one bucket prefix. |
| MID-056-EX05 | 4 | Estimate monthly cost for the lab environment and name the three largest items. |
| MID-056-EX06 | 4 | Review a diagram with a public database and an admin key in the app; list fixes. |

## Solutions
- **EX01** Managed database: the provider handles the hardware, OS, patching, and failover; you handle access rules, data, queries, and backups policy. VM: you also handle the OS and patches.
- **EX02** One region near users and allowed by data law, services spread across at least two AZs, database with a standby in another AZ.
- **EX03** Public subnets: load balancer, NAT. Private: apps and database. Database rule: allow 5432 from the app group only.
- **EX04** Allow `s3:GetObject`/`PutObject` (or the provider equivalent) on `arn:...:shop-images/orders/*` only; no wildcards.
- **EX05** Typically the database, compute, and NAT or load balancer dominate; verify against the provider's calculator.
- **EX06** Move the database to a private subnet, restrict security groups, replace the key with a workload role, and add audit logging.

**Outcome 1** is also covered by quiz Q01–Q03; outcome 3 by the lab (least-privilege role).
