# Java Backend Engineering Mastery — Curriculum Specification

The source of truth for a career-oriented curriculum that takes a learner from zero programming knowledge to Solution Architect.

This repository turns the roadmap (Curriculum Architecture v1.0) into a maintainable specification: every module has a stable ID, prerequisites, measurable outcomes, lectures, labs, and assessment criteria. Videos, slides, code samples, and course listings (YouTube, Udemy) are all produced *from* this repository, never the other way round.

## Repository layout

| Path | What it holds |
| --- | --- |
| [`CONVENTIONS.md`](CONVENTIONS.md) | ID scheme, module template, definition of done, technology baseline, change process |
| [`catalog/modules.yaml`](catalog/modules.yaml) | **Machine-readable source of truth**: levels, phases, all 321 modules (the roadmap's 298, plus BEG-055 and 22 AI modules added in v2.0), prerequisites |
| [`catalog/INDEX.md`](catalog/INDEX.md) | Generated index of every module, grouped by level and phase |
| [`levels/`](levels/) | One folder per level. `README.md` is generated from the catalog; phase files hold detailed module specs; `interview-prep.md` holds that level's most common interview questions, how to answer them, and where each was learned and practiced |
| [`projects/ladder.md`](projects/ladder.md) | The evolving-domain project ladder and capstone briefs |
| [`assessment/framework.md`](assessment/framework.md) | Assessment dimensions, weights per level, rubric scale, completion gates |
| [`tools/build.py`](tools/build.py) | Validates the catalog and regenerates the generated files |

## Levels and specification status

| Level | Code | Modules | Status |
| --- | --- | --- | --- |
| 1. Beginner — Foundations | `BEG` | 57 | **Detailed** — full module specs in [`levels/01-beginner/`](levels/01-beginner/) |
| 2. Junior Backend Engineer | `JNR` | 57 | **Detailed** — full module specs in [`levels/02-junior/`](levels/02-junior/) |
| 3. Mid-Level Backend Engineer | `MID` | 72 | **Detailed** — full module specs in [`levels/03-mid/`](levels/03-mid/) |
| 4. Senior Backend Engineer — Grade C | `SRC` | 22 | **Detailed** — full module specs in [`levels/04-senior-c/`](levels/04-senior-c/) |
| 5. Senior Backend Engineer — Grade B | `SRB` | 22 | **Detailed** — full module specs in [`levels/05-senior-b/`](levels/05-senior-b/) |
| 6. Senior Backend Engineer — Grade A | `SRA` | 22 | **Detailed** — full module specs in [`levels/06-senior-a/`](levels/06-senior-a/) |
| 7. Staff Software Engineer | `STF` | 22 | **Detailed** — full module specs in [`levels/07-staff/`](levels/07-staff/) |
| 8. Solution Architect | `ARC` | 47 | **Detailed** — full module specs in [`levels/08-solution-architect/`](levels/08-solution-architect/) |

*Outline* means the module exists in the catalog with its ID, title, and topics; *Detailed* means every module also has prerequisites, outcomes, lectures, a lab, and an assessment (see the status ladder in `CONVENTIONS.md`).

**AI is woven through every level**, at the depth of that level: using AI assistants responsibly (Beginner, Junior), building LLM features in Spring and then RAG, tools, and evaluation (Junior, Mid), operating AI reliably (Senior C), AI platforms, strategy, and responsible AI (Senior B, Senior A), AI governance (Staff), and AI solution architecture (Architect). Every capstone has AI requirements and every interview guide has AI questions.

Senior grades run C → B → A, with A the most advanced. This is a course convention, not an industry standard. Staff Engineer and Solution Architect are related advanced tracks, not a mandatory linear sequence, and real progression into Senior, Staff, and Architect roles requires production experience that no course can substitute for.

## Working with the catalog

Requires Python 3.10+ and PyYAML (`pip install pyyaml`).

```bash
py tools/build.py
```

This validates the catalog (unique IDs, valid phases, prerequisites that exist and come earlier in the sequence) and regenerates `catalog/INDEX.md` and every `levels/*/README.md`. Run it after any catalog change; a failing validation must be fixed before committing.

## Release plan

1. **Release 1 — Beginner Foundations** (Level 1 + capstone). Specs: done. Next: lecture scripts and exercises.
2. **Release 2 — Junior Backend Engineer.** Specs: done. Next: lecture scripts and exercises.
3. **Release 3 — Mid-Level Engineer.** Specs: done. Next: lecture scripts and exercises.
4. **Release 4 — Senior, Staff, and Architect tracks**, as case studies and workshops. Specs: done for all Senior grades, Staff, and Solution Architect. Next: lecture scripts and exercises.

Optional specializations after the Mid level (high-scale systems, platform engineering, cloud architecture, security engineering, enterprise integration) are planned but not yet catalogued.
