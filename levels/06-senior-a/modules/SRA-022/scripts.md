# SRA-022 · Responsible AI and AI compliance — Lecture scripts

**Video:** 86 min · **Running case:** *Commerce 2030* — the group formed by Shop and FulfillCo has 25 engineering teams and plans a third-party seller marketplace, a five-country expansion, and doubled order volume each year for three years, while its earliest services approach end of life; you are the senior technical leader for the commerce product area.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRA-022-L01 · Responsible AI as engineering (10 min)
**Goal:** turn responsible-AI principles into concrete design controls.

**Key points**
- Principles: transparency, fairness, human oversight, accountability.
- A principle becomes engineering when it has a control, an owner, and a test.
- Examples: show users when AI is used, evaluate for unequal error rates, let people review and override, log decisions.
- Treat it like security: built in, reviewed, and measured, not a final checklist.

**Show:** a table mapping each principle to a design control, an owner, and the evidence it produces for the marketplace assistants.

**Check:** What turns a principle into engineering? *(A control, an owner, and a way to test it.)*

---

## SRA-022-L02 · Privacy and residency of model calls (12 min)
**Goal:** decide what data may go to which model, where, and for how long.

**Key points**
- Every call to a model sends data to a processor; check its terms, retention, location, and use of data for training.
- Classify data and allow only permitted classes for each model option.
- Minimize and redact: send only what the task needs, remove identifiers where possible.
- Residency rules may require regional endpoints or self-hosting; verify with legal.

**Show:** a data-flow diagram for the support assistant with country boundaries, the fields sent to the model, the provider's retention terms (verify), and a redaction step.

**Check:** What should you check before sending personal data to a hosted model? *(The provider's terms: retention, location, training use, and whether the data class is allowed.)*

---

## SRA-022-L03 · Risk-based classification of AI use cases (12 min)
**Goal:** classify use cases by risk following the risk-based approach of regulation such as the EU AI Act.

**Key points**
- Risk-based approach: obligations rise with the potential harm of a use (minimal, limited transparency duties, high, prohibited).
- Use cases that affect people's access to work, credit, or essential services get closer scrutiny.
- Classification decides required controls; do it early and keep records.
- Legal partners confirm the class and obligations; verify current regulation text before recording.

**Show:** a register: use case, affected people, risk class (proposed), obligations, controls, legal reviewer, review date.

**Check:** Who confirms the risk class and obligations? *(Legal and compliance partners; engineering proposes and implements the controls.)*

---

## SRA-022-L04 · Transparency, bias, and human oversight (12 min)
**Goal:** design controls for explainability, fairness, and human involvement.

**Key points**
- Transparency: tell people when they are dealing with AI and how decisions can be challenged.
- Bias: evaluate quality across groups and languages and monitor after launch.
- Human oversight: a trained person can review, override, and stop the system; avoid rubber stamping.
- An appeal path is needed wherever a decision affects people materially.

**Show:** a flow for an automated decision: model proposes, human reviews the cases above a risk threshold, decision logged, the affected party notified with an appeal route.

**Check:** What is the weakness of human oversight that only clicks "approve"? *(It is rubber stamping; the reviewer needs information, time, and authority to override.)*

---

## SRA-022-L05 · Auditability of AI decisions (10 min)
**Goal:** record enough to reconstruct and explain AI-assisted outcomes.

**Key points**
- Record inputs (with privacy care), outputs, model and prompt versions, retrieved sources, and the human decision.
- Version prompts, models, and evaluation sets like code.
- Keep logs tamper-resistant, with retention that matches the law and privacy rules.
- Use records for incident review, appeals, and regulator requests.

**Show:** an audit record: request id, time, model and version, prompt template version, input reference, output, confidence, reviewer, final decision.

**Check:** Why record the model and prompt version? *(Behavior changes with versions; reconstructing a past decision needs the exact versions used.)*

---

## SRA-022-L06 · Demo: risk-classifying the marketplace's AI features (15 min)
**Goal:** classify features and set required controls; prepares SRA-022-LAB1.

**Steps**
1. List features: listing assistant, support assistant, search ranking, fraud scoring, seller suspension recommendations.
2. For each, identify who is affected and what harm is possible.
3. Propose a risk class and obligations; take it to the role-played legal partner and adjust (verify regulation text).
4. Attach controls: notices, oversight, evaluation, logging.
5. **Planned mistake:** classify by technology ("it is just a chatbot") rather than by impact. Fix: classify by effect on people; the seller suspension feature moves to a higher class.
6. Record the register with review dates.

---

## SRA-022-L07 · Demo: designing human oversight for automated seller suspensions (15 min)
**Goal:** design a decision flow with oversight and an appeal path; prepares SRA-022-LAB1.

**Steps**
1. Define the decision: a fraud model flags sellers; a suspension stops income, so harm is real.
2. Set the rule: the model recommends; a trained reviewer decides; automatic action only for clear, low-harm temporary holds.
3. Give the reviewer the evidence: features, explanation, history, and a time budget.
4. Add notice and appeal: reasons given, appeal path, and a human decision within a stated period.
5. **Planned mistake:** fully automate suspensions to save reviewer cost. Fix: show harm and legal exposure, and keep review for high-impact actions while automating low-impact holds.
6. Add audit records and monitoring of appeal outcomes and error rates.
