# SRA-001 · Architecture at scale — Exercises and lab

## Lab
### SRA-001-LAB1 · Landscape map
**Outcomes:** 1–4 · **Time:** ~2 h
1. Gather the service catalog, team list, on-call rotas, and a quarter of change history for Commerce 2030 (use the case materials).
2. Draw the map: systems grouped by product domain, owning teams, platforms, and shared capabilities; classify each shared item honestly.
3. Overlay dependencies and cross-team change from the history.
4. Mark the five worst coordination hot spots, each with evidence and a proposed boundary or ownership change.
5. Review with role-played team leads and revise.
**Acceptance:** reviewed by role-played team leads who agree the hot spots are real.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| SRA-001-EX01 | 1 | Given a list of twelve Commerce 2030 components, classify each as product domain, shared capability, or platform and justify the three hardest calls. |
| SRA-001-EX02 | 2 | Three teams each integrate a carrier API. Decide whether to build a platform; write a one-page case with interface, owner, and service level. |
| SRA-001-EX03 | 2 | Redraw a boundary: a shared "common" library edited by eight teams. Propose where the boundary should go and how teams would cope during transition. |
| SRA-001-EX04 | 3 | For three marketplace decisions, decide now, at the last responsible moment, or keep open; name the trigger for each deferred one. |
| SRA-001-EX05 | 3 | Write two fitness functions (one for coupling, one for platform adoption) and state how each runs in CI or reporting. |
| SRA-001-EX06 | 4 | Given a pull-request heat map and team list, identify three misalignments and the smallest change that would reduce each. |

## Solutions
- **EX01** Examples: checkout and seller onboarding are domains; identity and notifications are platforms if run as products, otherwise shared capabilities; a shared utility library is shared coupling. Check each against "customer, self-service, roadmap, owner".
- **EX02** Yes if the need is stable and repeated: one carrier platform team, a versioned API, an SLO, a support channel, and a migration plan one team at a time. Record the risk of a bottleneck and how self-service reduces it.
- **EX03** Split the library: stable pieces move to an owned platform with versioning; domain-specific code returns to its domain. Transition: freeze new features, deprecate gradually, keep a compatibility layer.
- **EX04** Example: seller identity model decide now (hard to change, many dependents); payout provider decide at last responsible moment when volume and countries are known; search engine keep open behind an interface. Triggers: first seller contract signed, second-country launch, listing volume threshold.
- **EX05** Coupling: a build-time check that fails if a service imports another domain's internals (ArchUnit-style or dependency rules). Adoption: a weekly report of teams still calling the provider directly versus the platform API.
- **EX06** Typical: a service touched by many teams (split by capability), a team owning unrelated systems (rebalance ownership), a system with no owner (assign one). Smallest change first: owner or interface before reorganization.

Outcome 1 is also covered by the lab map and quiz; outcome 4 by the lab hot-spot review.

**Workplace evidence:** an architecture landscape you produced that leadership used for planning.
