# MID-058 · Infrastructure as Code — Lecture scripts

**Video:** 62 min · **Analogy used throughout:** architectural blueprints: you change the plan, review it, and the builders make the building match, instead of knocking walls down by hand. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-058-L01 · Why infrastructure as code (8 min)
**Goal:** see why infrastructure belongs in version control.

**Key points**
- Clicking in a console is slow, undocumented, and cannot be reproduced.
- Code gives review, history, repeatable environments, and disaster recovery.
- Declarative tools (Terraform, OpenTofu, Pulumi, Bicep, CloudFormation) describe the end state; the tool computes the steps.
- Treat infrastructure changes like application changes: pull request, review, pipeline.

**Show:** the MID-056 console steps versus the same environment as a short code file.

**Check:** What does "declarative" mean? *(You describe the desired end state; the tool works out how.)*

---

## MID-058-L02 · Terraform basics (12 min)
**Goal:** write, plan, and apply a simple configuration.

**Key points**
- Providers talk to a cloud API; resources are the things created; variables and outputs are inputs and results.
- Workflow: `terraform init`, `plan` (shows the diff), `apply`.
- Always read the plan; it shows what will be created, changed, or destroyed.
- Pin provider and Terraform versions; verify current versions before recording.

**Show**
```hcl
resource "aws_s3_bucket" "images" {
  bucket = "shop-images-${var.env}"
}
variable "env" { type = string }
```
(Use the equivalent resource for the chosen provider.)

**Check:** Which command shows what will change? *(`terraform plan`.)*

---

## MID-058-L03 · State and drift (10 min)
**Goal:** understand state, store it safely, and handle drift.

**Key points**
- State maps your code to real resources; losing it means losing control.
- Use remote state (object storage with a lock table or the provider's equivalent) so the team shares one state and runs do not collide (locking).
- State can contain secrets; encrypt it and restrict access.
- Drift: real infrastructure differs from code after manual changes. Detect it with `plan`, then fix the code or revert the change.

**Show:** backend block using remote storage with locking enabled; a plan showing drift on a changed security group.

**Check:** Why remote state? *(Shared, locked, backed-up state instead of a file on one laptop.)*

---

## MID-058-L04 · Modules and environments (10 min)
**Goal:** structure configuration for reuse.

**Key points**
- A module is a reusable group of resources with inputs and outputs (for example `network`, `database`).
- Separate environments (dev, staging, prod) with separate state; reuse the same modules with different variables.
- Avoid one giant root module; split by lifecycle and ownership.
- Version modules and keep their interfaces small.

**Show:** layout: `modules/network`, `modules/database`, `envs/dev`, `envs/prod`, each env calling the modules.

**Check:** Why separate state per environment? *(A mistake in dev cannot affect production, and blast radius stays small.)*

---

## MID-058-L05 · Terraform in CI (8 min)
**Goal:** run Terraform from a pipeline with reviewable plans.

**Key points**
- On a pull request: `fmt`, `validate`, `plan`, post the plan as a comment.
- On merge to main: `apply` the reviewed plan, with approval for production.
- Pipeline identity uses short-lived credentials with least privilege.
- Add policy checks and security scanning (for example tfsec or Checkov; verify tool before recording).
- Forbid console changes; any manual change is drift.

**Show:** pipeline stages: fmt/validate → plan (comment on PR) → approval → apply.

**Check:** Why post the plan on the pull request? *(Reviewers see exactly what will change before it happens.)*

---

## MID-058-L06 · Demo: rebuilding the clicked infrastructure as code (14 min)
**Goal:** recreate the MID-056 environment from code. Prepares MID-058-LAB1.

**Steps**
1. Create the remote state backend with locking.
2. Write `network`, `database`, and `storage` modules from the MID-056 design; call them from `envs/dev`.
3. **Planned mistake:** run `apply` without reading the plan and it tries to replace the database. Fix: read the plan, spot the `-/+` replacement, and adjust the change (or use a lifecycle rule) before applying.
4. Apply, then change a security group in the console and show the drift in the next plan.
5. Destroy and recreate everything from code alone; compare the result with the MID-056 environment.

**Check:** What in a plan warns of data loss? *(A resource marked for replacement or destroy, such as `-/+`.)*
