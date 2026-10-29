# MID-058 · Infrastructure as Code — Exercises and lab

## Lab
### MID-058-LAB1 · Shop infrastructure
**Outcomes:** 1–4 · **Time:** ~3 h
Rebuild the MID-056 environment in Terraform: modules for network, database, and storage; separate dev and staging environments; remote state with locking; a pipeline that runs `fmt`, `validate`, and `plan` on pull requests and posts the plan.
**Acceptance:** destroy and recreate the environment from code alone.

## Exercises (assessment: plan review exercise)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-058-EX01 | 1 | Write a Terraform resource for a private object-storage bucket and run `plan`. |
| MID-058-EX02 | 1 | Review a given plan: identify the destructive change and propose a safer path. |
| MID-058-EX03 | 2 | Configure a remote backend with locking and explain what drift is with an example. |
| MID-058-EX04 | 3 | Refactor one root module into `network` and `database` modules with inputs and outputs. |
| MID-058-EX05 | 3 | Design the folder layout for dev, staging, and prod with separate state. |
| MID-058-EX06 | 4 | Write the pipeline stages for pull requests and for merge, including approval for prod. |

## Solutions
- **EX01** Bucket resource with a private ACL or block-public-access setting; `init`, then `plan` shows one resource to add.
- **EX02** A resource with `-/+` (forced replacement) on the database means data loss; change the argument that forces replacement, or use a migration or `lifecycle { prevent_destroy = true }`.
- **EX03** Backend block pointing to remote storage with a lock table or equivalent; drift: someone widens a security group in the console, and the next `plan` shows the difference.
- **EX04** Move resources into `modules/network` and `modules/database`, expose outputs such as `private_subnet_ids`, and wire them in the environment root.
- **EX05** `modules/*`, `envs/dev`, `envs/staging`, `envs/prod`, each with its own backend key.
- **EX06** PR: fmt, validate, security scan, plan posted as a comment. Merge: apply the saved plan; production requires approval.

**Outcome 4** is also covered by the lab criterion (plans on PRs) and quiz Q09–Q10.
