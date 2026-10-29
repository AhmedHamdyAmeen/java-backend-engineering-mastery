# ARC-028 · Security architecture — Exercises and lab

## Lab
### ARC-028-LAB1 · Larkspur security architecture
**Outcomes:** 1–4 · **Time:** ~4 h
1. Draw the platform context with trust boundaries (internet, stores, platform, ERP, CRM, payment provider).
2. Build the threat model: list threats per boundary, rate likelihood and impact, rank them.
3. Build a control map by layer (identity, application, data, network, operations); mark each control preventive, detective, or corrective.
4. Trace each control to a business requirement or standard.
5. Assemble the security architecture view and present it to a role-played CISO.
**Acceptance:** top ten threats each have a control and an owner; reviewed by a role-played CISO.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-028-EX01 | 1 | Larkspur's store tills sit on a trusted store network. Redesign the till-to-platform path using zero-trust principles. |
| ARC-028-EX02 | 1 | Fill a defense-in-depth table (identity, application, data, network) for customer account data and state what happens if each layer fails. |
| ARC-028-EX03 | 2 | Threat-model the gift-card balance check feature; list five threats and rank them. |
| ARC-028-EX04 | 2 | Two threats have equal impact; one is far more likely. Explain how you prioritize and what you tell the sponsor about the other. |
| ARC-028-EX05 | 3 | Map "customers must trust our checkout" and "meet the company password standard" to threats and controls in a traceability table. |
| ARC-028-EX06 | 4 | Review a draft security view that is a list of eight products. Write the review comments that turn it into an architecture a security team can approve. |

## Solutions
- **EX01** Each till has its own device identity and short-lived credentials; calls go through the gateway with authorization per till and store; segment the store network; monitor till behavior; network location grants nothing by itself.
- **EX02** Identity: MFA for staff, short-lived tokens (if stolen: limit scope and expiry). Application: authorization per record (if bypassed: field-level rules and logging). Data: encryption at rest, tokenized payment data (if a key leaks: rotation and separate keys). Network: private endpoints, segmentation (if breached: internal authentication and detection).
- **EX03** Threats: card-number enumeration, brute force, bot abuse, balance leaks through error messages, insider lookups. Rank by likelihood and impact; enumeration and bots first; controls: rate limiting, generic errors, step-up checks, audit of lookups.
- **EX04** Prioritize the more likely threat; record the other as a monitored or accepted risk with owner and review date; the sponsor or risk owner accepts it, not the architect alone.
- **EX05** Trust → threats: skimming script, session theft → controls: hosted payment fields, content security policy, secure cookies. Password standard → threat: credential stuffing → controls: MFA for staff, breached-password check, rate limiting.
- **EX06** Comments: name assets and threats first; show trust boundaries; map each product to the threat it addresses and drop those with none; add owners, evidence, detection and response; list accepted risks.

**Workplace evidence:** a security architecture you designed that passed a formal review.
