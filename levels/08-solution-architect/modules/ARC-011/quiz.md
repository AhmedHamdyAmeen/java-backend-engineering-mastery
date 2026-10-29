# ARC-011 · Cloud service models — Quiz

Outcomes: O1 distinguish models · O2 shared responsibility · O3 choose per component.

**Q01 (O1)** Larkspur rents virtual machines and installs its own runtime. Which model is this? A. IaaS B. PaaS C. SaaS D. Function-as-a-service only
**Q02 (O1)** A team deploys a container image and the provider patches the OS and runtime. This is closest to: A. IaaS B. SaaS C. On-premises D. PaaS
**Q03 (O1)** With a managed database, which task is still the customer's? A. Patching the engine B. Designing schema and access C. Replacing failed hardware D. Hypervisor security
**Q04 (O2)** In every service model, who always owns the data and its access settings? A. The provider B. The customer C. The auditor D. The network carrier
**Q05 (O2)** An exposed storage bucket caused by a misconfiguration is usually: A. A customer-side failure B. A provider hardware fault C. A DNS issue D. An ISP issue
**Q06 (O2)** Moving up from IaaS to SaaS, the customer's operational duties generally: A. Grow B. Stay identical C. Shrink but never vanish D. Become zero
**Q07 (O3)** A small team with a standard web workload should default to: A. The lowest-level service for control B. The highest-level service that meets requirements C. Self-built everything D. Whatever is newest
**Q08 (O3)** Which is a hidden cost of IaaS by default? A. Owning patching and on-call for the OS B. Lower flexibility than SaaS C. No network control D. Provider lock-in is impossible
**Q09 (O3)** The most honest way to treat lock-in is to: A. Avoid it at all costs B. Ignore it C. Estimate exit cost and accept it knowingly where benefit is high D. Only use open-source software
**Q10 (O3)** "Managed means no operations" is wrong because: A. Managed services need no monitoring B. The team still sizes, secures, monitors, and tests recovery C. Providers do not patch D. It applies only to SaaS

## Answers
Q01 A · Q02 D · Q03 B · Q04 B · Q05 A · Q06 C · Q07 B · Q08 A · Q09 C · Q10 B

## Practical part
Matrix review of the `ARC-011-LAB1` service-model matrix plus exercises `ARC-011-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and every responsibility gap in the matrix assigned to an owner.
