# ARC-012 · Cloud architecture — Quiz

Outcomes: O1 regions and zones · O2 reference architectures · O3 accounts and environments · O4 diagram and trust boundaries.

**Q01 (O1)** Deploying across multiple availability zones in one region protects against: A. A regional outage B. Failure of one data center group C. A bad deployment D. Data-residency law
**Q02 (O1)** Which factor most directly limits region choice for personal data? A. Data residency rules B. Brand colors C. Number of zones D. Editor choice
**Q03 (O1)** A CDN mainly helps with: A. Database writes B. Latency for static and cacheable content C. Account billing D. Identity federation
**Q04 (O2)** The best use of a provider reference architecture is: A. Copy it unchanged B. Use it as a starting point and adopt, adapt, reject with reasons C. Ignore it D. Use it only for diagrams
**Q05 (O2)** A reference component that serves no Larkspur requirement should be: A. Kept for safety B. Removed or rejected C. Doubled D. Hidden
**Q06 (O3)** Why use separate accounts per environment? A. To limit blast radius and isolate identity and billing B. To increase latency C. To avoid IaC D. To remove logging
**Q07 (O3)** Which extra account is typically worthwhile early? A. One per developer B. A security-logging account C. One per microservice D. One per database table
**Q08 (O3)** "Blast radius" means: A. Network bandwidth B. How far a mistake or compromise can spread C. The size of the data center D. The billing period
**Q09 (O4)** Where should a trust boundary be drawn? A. Between the internet and the platform edge B. Around the title block C. Only around the database D. Nowhere on the diagram
**Q10 (O4)** A good target diagram lets a reviewer: A. Count the icons B. Trace each element to a requirement C. Skip the requirements D. Avoid asking questions

## Answers
Q01 B · Q02 A · Q03 B · Q04 B · Q05 B · Q06 A · Q07 B · Q08 B · Q09 A · Q10 B

## Practical part
Architecture review of the `ARC-012-LAB1` diagram and traceability table plus exercises `ARC-012-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and every diagram element traceable to a requirement.
