# Curriculum Conventions

Rules every contributor follows so the specification stays consistent as it grows.

## 1. Identifiers

IDs are **stable**: once published, an ID is never reused or renumbered, even if a module is moved, merged, or retired.

| Kind | Format | Example |
| --- | --- | --- |
| Level | 3-letter code | `BEG`, `JNR`, `MID`, `SRC`, `SRB`, `SRA`, `STF`, `ARC` |
| Phase | `<LEVEL>-P<n>` | `BEG-P2` |
| Module | `<LEVEL>-<nnn>` | `BEG-014` |
| Lecture | `<MODULE>-L<nn>` | `BEG-014-L03` |
| Lab | `<MODULE>-LAB<n>` | `BEG-014-LAB1` |
| Exercise | `<MODULE>-EX<nn>` | `BEG-014-EX07` |
| Quiz question | `<MODULE>-Q<nn>` | `BEG-014-Q05` |
| Capstone | `<LEVEL>-CAP` | `JNR-CAP` |

Module numbers restart at `001` in each level. Every module also carries `n`, its number in the original 1–298 roadmap, for cross-referencing.

New modules take the next free number in their level, even if they are placed earlier in the teaching order. Teaching order is defined by the catalog's list order, not by the number.

Retired modules stay in the catalog with `status: retired` and a `replaced_by` field.

## 2. Module template

Each detailed module is a section in its phase file, in this order:

```markdown
### BEG-030 · Collections
`n: 30` · **Est. video:** 90 min · **Est. practice:** 6 h

**Prerequisites:** BEG-015, BEG-031 (concurrent)
**Learning outcomes** — the learner can:
1. <observable, assessable verb> …

**Lectures**
| ID | Title | Min |

**Lab** — `BEG-030-LAB1` <title>: <task and acceptance criteria>
**Common mistakes:** …
**Assessment:** <what the learner must produce or demonstrate to pass>
**Workplace evidence:** <Senior levels and above: what to show from real work>
**Career relevance:** <which level uses this and how>
```

From Level 4 (Senior C) onward, every module also has a **Workplace evidence** line naming what the engineer should be able to show from real work. Training demonstrates knowledge; workplace evidence demonstrates the role (see `assessment/framework.md`, section 5).

Outcomes use observable verbs (*write, explain, trace, debug, choose, compare*), never *understand* or *know*. Each outcome must be checked by at least one exercise, quiz question, or lab criterion.

Lecture durations target 8–12 minutes; anything over 15 is split.

**Demo lectures.** Every module ends with at least one live-coding demo lecture, titled `Demo: …`, in which the instructor builds or debugs the module's subject on the running project — the phase's running exercise in Level 1 (Bank Accounts, Contacts & Events, Library), *Shop* from Level 2 onward. Demos follow the same 8–15 minute limit; a longer demo is split into two. Concept lectures explain *why*; demos show *how*, including mistakes and their fixes. Heavy modules have two demos (in Level 1: methods, arrays and strings, classes, inheritance, exceptions, collections, streams, Git, SQL, JDBC; in Level 2: Spring core, persistence, security, testing, delivery; in Level 3: concurrency, profiling, query optimization, locking and transactions, Kafka, reliable messaging, sagas, resilience, Redis, observability, Kubernetes; in Level 4: trade-offs, capacity, database scaling, decomposition, failure modes, readiness, SLOs, disaster recovery, data integrity, troubleshooting, performance; in Levels 5–7: every module, because their multi-team role-plays need both a design session and a leadership session; in Level 8: the heaviest solution-design, integration, cloud, security, and delivery modules). From Level 4 onward demos are worked design or operations sessions on the running case rather than mostly live coding.

A module's **Video** estimate must equal the sum of its lecture durations; `tools/build.py` enforces this.

## 3. Prerequisites

- A prerequisite is a module whose content is **used**, not merely related.
- Prerequisites must come earlier in teaching order. `tools/build.py` enforces this.
- Mark a deliberately parallel dependency `(concurrent)`; the catalog records it in `co_requisites` and the order check skips it.
- Prerequisites from an earlier level are allowed and expected.

## 4. Specification status ladder

| Status | Meaning |
| --- | --- |
| `outline` | ID, title, topics in the catalog |
| `detailed` | Full module spec (template above) written and prerequisites set in the catalog |
| `scripted` | Lecture scripts, diagrams, and code samples written |
| `recorded` | Videos recorded and edited |
| `published` | Live on at least one platform, with exercises and solutions |

A level is **release-ready** when every module is `published`, its capstone brief and rubric exist, and its diagnostic test and interview simulation are written.

## 5. Definition of done for a level

A learner completes a level when they:

1. Pass every module assessment (rubric score ≥ 3 of 4, see `assessment/framework.md`).
2. Deliver the capstone, meeting every *required* acceptance criterion.
3. Pass the level's graduation gate (live demonstration or defense).
4. Pass the technical interview simulation for that level, prepared with the level's `interview-prep.md`.

## 6. Technology baseline

Separate durable principles from version-specific details. Version-specific lectures carry a `version:` note so they can be found and re-recorded.

| Area | Baseline (verify before recording) |
| --- | --- |
| Java | Current LTS (Java 25 at time of writing); a dedicated module covers newer releases |
| Framework | Spring Boot (current major) |
| Build | Maven (Gradle mentioned, not taught) |
| Database | PostgreSQL (current supported major) |
| IDE | IntelliJ IDEA Community; VS Code as alternative |
| Testing | JUnit 5, Mockito, AssertJ, Testcontainers |
| Delivery | Git, GitHub, GitHub Actions, Docker, Kubernetes, Terraform |
| Observability | OpenTelemetry, Prometheus, Grafana |
| Cloud | One provider in depth (AWS or Azure — decision pending), principles provider-neutral |
| AI | Spring AI as the primary Java framework (LangChain4j mentioned); PostgreSQL with pgvector for vector search; provider-neutral model access through an interface; model names, prices, and framework APIs verified before recording |

Review the baseline at the start of every release and log changes in the change history below.

## 7. Architecture philosophy

Modular monoliths before microservices. Distributed complexity is introduced only when a concrete requirement justifies it, and every lesson that introduces a new technology states the problem it solves.

## 8. Change process

1. Edit `catalog/modules.yaml` and/or the phase files.
2. Run `py tools/build.py`; fix any validation errors.
3. Record the change in the change history below (or in the module's own history once modules have their own folders).

## Change history

| Date | Change |
| --- | --- |
| 2026-10-28 | v1.0 specification: catalog of 299 modules (added BEG-055 JDBC essentials, a prerequisite of the Beginner capstone), Level 1 detailed, conventions, project ladder, assessment framework |
| 2026-10-28 | v1.1: Level 2 (Junior) detailed — prerequisites for JNR-001…054; JNR-048/049/050 (Linux, Docker, Compose) moved before JNR-045 because Testcontainers needs Docker; full JNR-CAP brief |
| 2026-10-28 | v1.2: added 72 live-coding demo lectures to Level 2 (one per module, two for 18 heavy modules; +13.2 h), bringing Level 2 video from ~42.5 h to ~55.7 h, inside the 50–70 h estimate; demo-lecture convention added |
| 2026-10-28 | v1.3: added 65 demo lectures to Level 1 (one per module, two for 10 heavy modules; +8.7 h), bringing Level 1 video from ~42.5 h to ~51 h, inside the 40–55 h estimate; corrected BEG-012/014/015 video estimates to their lecture sums; validator now checks video estimates against lecture totals |
| 2026-10-28 | v1.4: Level 3 (Mid) detailed — prerequisites for MID-001…066, 66 demo lectures plus a second demo in 13 heavy modules (~70 h video); MID-059/060/061 (architectural styles, DDD, microservices intro) moved from MID-P6 to the start of MID-P3 because services are split there; MID-P6 renamed to API Evolution and Professional Ownership; full MID-CAP brief |
| 2026-10-28 | v1.5: Level 4 (Senior C) detailed — prerequisites for SRC-001…020, demo sessions in every module plus a second in 11 (~28 h video); *Workplace evidence* field added to the module template from Level 4 onward; full SRC-CAP brief |
| 2026-10-28 | v1.6: Level 5 (Senior B) detailed — prerequisites for SRB-001…020, two worked sessions per module (~29 h video), new running case *The FulfillCo integration* (acquired legacy monolith, four teams); full SRB-CAP brief |
| 2026-10-28 | v1.7: Level 6 (Senior A) detailed — prerequisites for SRA-001…020, two worked sessions per module (~28 h video), new running case *Commerce 2030* (25 teams, marketplace, five countries); full SRA-CAP brief |
| 2026-10-28 | v1.8: interview preparation guide per level (`levels/*/interview-prep.md`) linking each common interview question to the modules, labs, and capstone that teach and prove it, plus a market-skills table per level; validator checks every referenced ID |
| 2026-10-28 | v1.9: Levels 7 (Staff) and 8 (Solution Architect) detailed — all 299 modules now detailed; new running cases *Platform 2.0* (Staff) and *Larkspur Retail* (Architect); full STF-CAP and ARC-CAP briefs; Staff and Architect interview guides now point to their own labs |
| 2026-10-28 | v2.0: AI added to every level — 22 new modules (BEG-056/057, JNR-055…057, MID-067…072, SRC-021/022, SRB-021/022, SRA-021/022, STF-021/022, ARC-045…047) covering AI-assisted development, building AI features in Java, and AI architecture and governance; AI requirements in all eight capstones; AI questions in every interview guide; AI-use policy for assessments; AI technology baseline |
