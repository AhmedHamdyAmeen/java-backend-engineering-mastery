# STF-012 · Technical proposals — Exercises and lab

## Lab
### STF-012-LAB1 · Golden-path RFC
**Outcomes:** 1–4 · **Time:** ~4 h
1. Write the problem statement for the Platform 2.0 golden path using the STF-009 baseline; test it with two skeptical readers.
2. Write the RFC: goals and non-goals, proposal, at least three alternatives including "do nothing", costs, risks, rollout, open questions, decision needed.
3. Add the layered reading paths for executives, managers, and engineers.
4. Pre-circulate, then publish with a review window and a named decision maker.
5. Run the review with role-played reviewers; respond to every comment and close with a recorded decision.
**Acceptance:** decision recorded within the review window; major objections answered in the document.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| STF-012-EX01 | 1 | Rewrite the opening of a solution-first RFC ("We should adopt Backstage") as a problem statement with who is hurt, how much, and what happens if nothing is done. |
| STF-012-EX02 | 2 | Given a draft with no alternatives, write a comparison of three options plus "do nothing" on cost, time, risk, and team effort. |
| STF-012-EX03 | 2 | List the costs and risks an RFC for the golden path must state openly and the mitigation for each. |
| STF-012-EX04 | 3 | Plan the review: reviewers to pre-brief, review window, decision maker, and what you do with a late blocking comment. |
| STF-012-EX05 | 3 | Sort 12 sample comments into blocking and non-blocking and write responses to three. |
| STF-012-EX06 | 4 | Write the same proposal summary three times: for an engineer, a manager, and the CFO. |

## Solutions
- **EX01** "Twenty teams run separate pipelines; a new service takes three weeks to reach production and pipeline drift caused four audit findings. Without change, both grow with the team count." Solution comes later.
- **EX02** Table with do nothing (no cost, problem grows), extend current pipelines (medium cost, still fragmented), golden path (higher upfront, lowest ongoing), vendor tool (license cost, less fit). Recommend with explicit reasons.
- **EX03** Costs: migration effort per team, platform team capacity, reduced local freedom. Risks: low adoption, single point of failure, slow platform releases. Mitigations: pilot, escape hatch, SLOs and a support model.
- **EX04** Pre-brief the two toughest tech leads and security; two-week window; named decision maker; late blockers are logged and answered if new, otherwise recorded as dissent.
- **EX05** Blocking: security gap, missing rollback, data residency. Non-blocking: naming, doc style. Respond with a change, a reasoned rejection, or an owner and date.
- **EX06** Engineer: design and trade-offs; manager: effort per team, timeline, support; CFO: cost, expected saving, risk, decision needed by date.

Outcome 3 is also covered by the lab review; outcome 4 by the lab layered paths.

**Workplace evidence:** an RFC you wrote that changed how several teams work.
