# ARC-028 · Security architecture — Quiz

Outcomes: O1 zero trust and defense in depth · O2 solution threat modeling · O3 mapping controls to requirements · O4 reviewable security view.

**Q01 (O1)** Zero trust means: A. Trusting the internal network B. Blocking all traffic C. Verifying identity and context on every request D. Using one strong firewall
**Q02 (O1)** Defense in depth is best described as: A. One very strong control B. Several independent layers so one failure is not a breach C. Duplicating the same control D. Hiding the design
**Q03 (O1)** A store till is on the corporate network and calls the ERP API. Under zero trust: A. It is allowed because it is internal B. It is allowed after a firewall rule C. It must still authenticate and be authorized for that call D. It must use email approval
**Q04 (O2)** Threat modeling a whole solution should start from: A. A product shortlist B. A penetration test report C. The budget D. A data-flow view with trust boundaries
**Q05 (O2)** After listing threats you should next: A. Rank them by likelihood and impact B. Buy tools C. Delete the low ones silently D. Wait for an audit
**Q06 (O2)** A top threat that will not be fixed now should be: A. Ignored B. Hidden from the sponsor C. Recorded as an accepted risk with owner and review date D. Renamed as a feature
**Q07 (O3)** A control with no threat behind it is: A. Free of cost B. Cost without clear benefit C. Always required D. A detective control
**Q08 (O3)** A hosted payment field with a content security policy mainly addresses: A. Skimming scripts on the checkout page B. Slow queries C. ERP outages D. Joiner-mover-leaver
**Q09 (O4)** A security team can approve a view that: A. Lists products B. Is verbal only C. Covers only the network D. Shows boundaries, threats, controls, owners, and evidence
**Q10 (O4)** In a CISO walkthrough you should lead with: A. Every control equally B. The top risks and the decisions you need C. Vendor logos D. The appendix

## Answers
Q01 C · Q02 B · Q03 C · Q04 D · Q05 A · Q06 C · Q07 B · Q08 A · Q09 D · Q10 B

## Practical part
Security architecture defense of the lab view and threat model plus exercises `ARC-028-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a lab where the top ten threats each have a control and an owner.
