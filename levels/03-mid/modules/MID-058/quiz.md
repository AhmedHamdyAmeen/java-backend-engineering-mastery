# MID-058 · Infrastructure as Code — Quiz

Outcomes: O1 declarative IaC and plan · O2 state and drift · O3 modules and environments · O4 Terraform in CI.

**Q01 (O1)** The main benefit of infrastructure as code is: A. Faster consoles B. Fewer cloud providers C. Reviewable, repeatable, versioned infrastructure D. Free hosting
**Q02 (O1)** `terraform plan` does: A. Deletes resources B. Shows the changes that `apply` would make C. Creates state D. Formats code
**Q03 (O1)** A resource shown with `-/+` in a plan means: A. It is unchanged B. It is new C. It is hidden D. It will be destroyed and recreated
**Q04 (O2)** Why use remote state with locking? A. Faster plans B. Smaller code C. Shared state without concurrent runs colliding D. No credentials needed
**Q05 (O2)** Drift is: A. A slow apply B. A module version C. A syntax error D. Real infrastructure that differs from the code
**Q06 (O2)** State files may contain: A. Secrets, so encrypt and restrict access B. Only comments C. Nothing sensitive D. Source code
**Q07 (O3)** A module is: A. A cloud region B. A reusable group of resources with inputs and outputs C. A state file D. A provider
**Q08 (O3)** Separate state per environment gives: A. Slower builds B. More code C. A smaller blast radius for mistakes D. Public access
**Q09 (O4)** In CI, the plan should be: A. Hidden B. Posted on the pull request for review C. Skipped D. Applied before review
**Q10 (O4)** Manual console changes should be: A. Encouraged B. Used in production only C. Always documented in chat D. Forbidden or treated as drift to fix

## Answers
Q01 C · Q02 B · Q03 D · Q04 C · Q05 D · Q06 A · Q07 B · Q08 C · Q09 B · Q10 D

## Practical part
Plan review (`MID-058-EX02`) plus lab `MID-058-LAB1`. Pass: quiz at least 8/10, remote state with locking, plans posted on PRs, and a full destroy and recreate from code alone.
