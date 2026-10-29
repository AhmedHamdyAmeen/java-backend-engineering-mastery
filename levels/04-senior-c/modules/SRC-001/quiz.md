# SRC-001 · Requirements engineering — Quiz

Outcomes: O1 eliciting requirements · O2 requirements, constraints, assumptions · O3 quality-attribute scenarios · O4 missing, conflicting, untestable requirements.

**Q01 (O1)** A stakeholder says "make it scalable". The best first move is to: A. Add Kubernetes B. Ask what load, by when, and what happens if it is missed C. Write it down as is D. Pick a database
**Q02 (O1)** Which interview question best surfaces a real need? A. "Do you want it fast?" B. "What happens if checkout is down for ten minutes at noon?" C. "Which framework?" D. "Is that all?"
**Q03 (O2)** "PostgreSQL remains the system of record" is a: A. Assumption B. Scenario C. Constraint D. Risk
**Q04 (O2)** "Peak traffic is about 6× the daily peak" not yet verified is a: A. Constraint B. Assumption C. Functional requirement D. Response measure
**Q05 (O2)** What should every recorded assumption have? A. A price B. A diagram C. A priority of one D. An owner and a way to verify it
**Q06 (O3)** Which part of a scenario makes it testable? A. Response measure B. Source C. Artifact D. Environment
**Q07 (O3)** Which is a well-formed measure? A. "Reasonably quick" B. "p99 under 800 ms at 600 req/s" C. "As fast as possible" D. "Good performance"
**Q08 (O4)** "99.95% availability" and "no budget for extra infrastructure" are: A. Compatible by definition B. A functional pair C. A conflict needing an accountable owner's decision D. An assumption
**Q09 (O4)** "The UI must be user friendly" is mainly: A. Untestable as written B. Conflicting C. A constraint D. Missing
**Q10 (O4)** Who should resolve a conflict between two stakeholders' requirements? A. The engineer silently in code B. The newest team member C. The accountable stakeholders, informed by options D. Nobody; pick the cheaper

## Answers
Q01 B · Q02 B · Q03 C · Q04 B · Q05 D · Q06 A · Q07 B · Q08 C · Q09 A · Q10 C

## Practical part
Six case exercises `SRC-001-EX01` to `EX06` plus the lab, with a recorded role-played interview. Pass: at least five of six exercises correct, quiz at least 8/10, and a requirements document passing the rubric (all scenarios measurable, conflicts with owners).
