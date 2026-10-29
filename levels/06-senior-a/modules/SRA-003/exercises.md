# SRA-003 · Complex domain modeling — Exercises and lab

## Lab
### SRA-003-LAB1 · Marketplace domains
**Outcomes:** 1–4 · **Time:** ~2 h
1. Plan and run an event-storming session on the seller marketplace with role-played domain experts (seller operations, finance, support, trust and safety).
2. Produce the event wall: events, commands, actors, policies, and hot spots.
3. Classify subdomains as core, supporting, or generic and note build/buy implications for each.
4. Draw the context map with named relationship patterns, marking where an anti-corruption layer is needed.
5. Compare the map with the current team structure and note mismatches.
**Acceptance:** build/buy implications noted per subdomain.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-003-EX01 | 1 | Classify eight Commerce 2030 subdomains as core, supporting, or generic with one-line reasoning each. |
| SRA-003-EX02 | 1 | Argue why tax calculation should not get the best engineers; state when your answer would change. |
| SRA-003-EX03 | 2 | Given a description of six contexts and their interactions, draw the context map and name each relationship pattern. |
| SRA-003-EX04 | 2 | Find a context map that copies the org chart; show two places where the real domain boundary differs and what you would change. |
| SRA-003-EX05 | 3 | Design an anti-corruption layer for a legacy inventory system: interface, translation, error handling, and tests. |
| SRA-003-EX06 | 4 | Write a facilitation plan for an event storm with twenty participants: invitees, scope, agenda, output, and how disagreements are handled. |

## Solutions
- **EX01** Example: seller trust scoring and marketplace ranking are core; onboarding workflow, returns handling supporting; payments, tax, email, identity generic. Justify by "what do customers choose us for".
- **EX02** Tax is generic and well covered by specialist vendors; building it diverts the best engineers from the core. It changes if the group operates in a jurisdiction no vendor serves or tax is the differentiator.
- **EX03** Name each pair: partnership, customer–supplier, conformist, open host service with published language; include direction of influence.
- **EX04** Look for contexts split by team where the vocabulary is the same, or contexts merged where it differs; propose a boundary change or a team interaction change.
- **EX05** A domain-facing interface; an adapter translating legacy codes and units; timeouts, retries, and a fallback for unknown values; contract tests with recorded legacy responses.
- **EX06** Invite experts and each touching team; scope one process end to end; agenda: events, order, commands, hot spots, boundaries; output: wall photo, open-questions list with owners; disagreements recorded as hot spots, not settled by volume.

Outcome 2 is also covered by the lab context map; outcome 4 by EX06 and the lab session.

**Workplace evidence:** a context map or modeling session that changed team or service boundaries.
