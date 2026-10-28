# Assessment and Career-Readiness Framework

Every level is assessed on evidence, not attendance. The weights below are a course convention for practical assessments, not an industry certification standard.

## 1. Dimensions

| Code | Dimension | What it looks for |
| --- | --- | --- |
| IMP | Practical implementation | Working, readable, idiomatic code that meets the requirements |
| DES | Engineering reasoning and design | Sound structure, justified trade-offs, appropriate simplicity |
| TSO | Testing, security, and operations | Meaningful tests, secure defaults, operability (logs, config, health) |
| COM | Communication and documentation | README, diagrams, ADRs, clear explanation in the defense |
| IND | Independent problem-solving | Handles the unseen requirement or fault without step-by-step help |
| LEA | Leadership and outcomes | Influence, alignment, measurable organizational results (Senior and above) |

## 2. Weights by level

Weights shift from implementation toward design and leadership as scope grows.

| Level | IMP | DES | TSO | COM | IND | LEA |
| --- | --- | --- | --- | --- | --- | --- |
| BEG | 45% | 15% | 15% | 10% | 15% | — |
| JNR | 35% | 25% | 20% | 10% | 10% | — |
| MID | 30% | 25% | 25% | 10% | 10% | — |
| SRC | 20% | 30% | 25% | 15% | — | 10% |
| SRB | 10% | 30% | 20% | 20% | — | 20% |
| SRA | 5% | 30% | 15% | 25% | — | 25% |
| STF | 5% | 25% | 15% | 25% | — | 30% |
| ARC | — | 40% | 15% | 30% | — | 15% |

JNR matches the roadmap's illustrative 35/25/20/10/10 split; the other rows are proposals to validate with pilot learners.

## 3. Rubric scale

Each dimension is scored 1–4. A module or capstone passes when **every** dimension scores ≥ 3, not just the weighted average.

| Score | Label | Meaning |
| --- | --- | --- |
| 1 | Not yet | Missing or does not work; major misconceptions |
| 2 | Developing | Works partially or only with help; gaps in reasoning |
| 3 | Proficient | Meets every required criterion independently |
| 4 | Exemplary | Meets stretch criteria; explains alternatives and trade-offs unprompted |

### Example: BEG-CAP descriptors at score 3

- **IMP:** all required features work; rules enforced in domain classes; no SQL built by concatenation.
- **DES:** feature packages; each class has one clear responsibility; repository behind an interface.
- **TSO:** ≥ 25 tests covering every borrowing rule and boundary; credentials not in the repository.
- **COM:** README lets a stranger run the app in under 15 minutes; class diagram matches the code.
- **IND:** implements the unseen requirement with tests within the session.

## 4. Assessment instruments per level

| Instrument | Purpose | When |
| --- | --- | --- |
| Diagnostic test | Place learners and let experienced ones skip modules | Before the level |
| Module assessments | Check each module's outcomes (exercises, quizzes, labs) | After each module |
| Capstone | Integrate the level's skills in one product | End of level |
| Graduation gate | Live demonstration or defense of the capstone | After the capstone |
| Interview simulation | Job-readiness for the level's role, drawn from the level's `interview-prep.md` questions | End of level |

### Interview preparation guides

Each level has an `interview-prep.md` in its folder that closes the loop between **learning**, **practice**, and **the job market**:

1. **Market table** — skills employers list for the level → modules that teach them → labs or capstone parts that prove them.
2. **Questions** — the most common interview questions for the level, each with how to answer, common traps, and *Learned in* (modules) and *Practiced in* (labs, capstone) links.
3. **Show it** — which portfolio artifact (and, from Senior C, which workplace evidence) backs up the answer.
4. **Preparation plan** — a short schedule ending in mock interviews.

`tools/build.py` checks that every module, lab, and capstone a guide references exists, so the guides cannot drift from the curriculum.

For Senior and above, assessments are scenario-based: production outages, conflicting requirements, migrations, design reviews, and stakeholder negotiations. These cannot replace real work experience, and certificates for those levels state that explicitly.

## 5. Training vs experience

Each level's completion certificate distinguishes:

- **Demonstrated in training:** knowledge and skills shown through the course's assessments.
- **Requires professional experience:** capabilities that only production work can prove (e.g., owning an on-call rotation, leading a real multi-team migration).

## 6. Cross-cutting competencies

Assessed continuously, at increasing depth:

| Competency | BEG / JNR | MID / Senior | Staff / Architect |
| --- | --- | --- | --- |
| English for engineering | Read docs, write READMEs | Design proposals, incident comms | Lead architecture discussions, present strategy |
| Problem-solving | Debug, decompose | Ambiguous defects and trade-offs | Organization-wide problem framing |
| Documentation | README, API docs | ADRs, RFCs, runbooks | Standards and strategy |
| Testing | Unit, integration | Contract, load, resilience | Organization-wide quality strategy |
| Security | Secure coding, OWASP | Threat modeling, security reviews | Security architecture and governance |
| Collaboration | Git, PRs, agile | Cross-team coordination | Organization-wide alignment |
| AI-assisted development | Effective prompting; verify generated code | AI-assisted debugging and test generation | AI governance, evaluation, security |
| Professional growth | CV, GitHub, interviews | Mentoring, ownership, career planning | Influence, strategy, leadership |

Also integrated: accessibility awareness, licensing and IP, technical writing, ethical engineering, data privacy, and open-source dependency maintenance.
