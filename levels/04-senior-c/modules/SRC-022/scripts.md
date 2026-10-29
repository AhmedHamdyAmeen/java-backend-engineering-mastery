# SRC-022 · Operating AI in production — Lecture scripts

**Video:** 86 min · **Running case:** *Order Processing at 10×* — Shop Platform's order subsystem must handle a 10× growth forecast, a 99.95% availability commitment, and a 15-minute recovery objective. Here the order-support assistant is the AI feature in that subsystem.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRC-022-L01 · AI changes are deployments too (10 min)
**Goal:** treat prompt, model, and retrieval changes with the same discipline as code.

**Key points**
- A prompt edit, a model version bump, or a retrieval setting can change behavior as much as a code change.
- Hidden changes: the provider updates a hosted model, the knowledge base is re-indexed, a tool description changes.
- Output is probabilistic, so "it worked once" proves little; you need evaluation over a set of cases.
- Editing a prompt in production by hand has no review, no test, and no rollback.

**Show** A table of change types (prompt, model, retrieval config, tool schema, knowledge data) against what could break and how you would detect it.

**Check:** Why is a prompt edit a deployment? *(It changes production behavior and so needs review, testing, and rollback.)*

---

## SRC-022-L02 · Versioning prompts, models, and retrieval (12 min)
**Goal:** make AI behavior reproducible as versioned configuration.

**Key points**
- Store prompts, model identifiers (pinned, not "latest"), parameters, and retrieval settings in version control as one configuration bundle with an ID.
- Deploy configuration like any release: reviewed, promoted through environments, reversible.
- Log the bundle ID, model version, and retrieved document IDs with every answer, so any answer can be traced.
- Keep the evaluation set versioned alongside it.

**Show**
```yaml
assistant-config: v42
model: <pinned model id; verify provider naming before recording>
temperature: 0.2
prompt: prompts/order-support@v42.md
retrieval: { index: orders-faq@2026-10, top_k: 5 }
eval-set: evals/order-support@v17
```

**Check:** What must be logged with each answer to trace it later? *(Config bundle ID, model version, and retrieved sources.)*

---

## SRC-022-L03 · Evaluation-gated and progressive releases (12 min)
**Goal:** block regressions before users see them and limit exposure when releasing.

**Key points**
- An evaluation gate runs the candidate configuration over a fixed case set and compares scores to the current version; failing blocks the release.
- Include safety cases (leaking data, refusing unsafe requests) as hard gates, not averages.
- Then release progressively: shadow mode, small canary share, widen, with online signals compared to baseline.
- Online signals: thumbs-down rate, escalation to human, refund-policy violations found by sampling.

**Show** Pipeline: change PR | offline eval gate | shadow run | 5% canary | 50% | 100%, each with promote and abort rules.

**Check:** Why make safety cases hard gates rather than part of an average? *(A single leak must not be hidden by high scores elsewhere.)*

---

## SRC-022-L04 · Detecting drift (10 min)
**Goal:** notice quality decay when nothing in your code changed.

**Key points**
- Sources of drift: provider model updates, changes in the knowledge data, new kinds of user questions, seasonality.
- Run the evaluation set on a schedule against production configuration; alert on score drops.
- Sample live conversations for human or automated grading and watch distributions of topics and refusal rates.
- Pinning model versions where possible reduces surprise; verify what your provider guarantees about deprecation.

**Show** A dashboard sketch: nightly eval score line, live sampled-grade line, escalation rate, new-topic cluster count, with alert thresholds.

**Check:** Name two causes of drift with no code change. *(For example a model update and changes in the data or user questions.)*

---

## SRC-022-L05 · Bad-output incidents, kill switches, and human review (12 min)
**Goal:** run a proper incident when AI output is wrong, unsafe, or leaking.

**Key points**
- Treat unsafe output as an incident: severity, commander, comms, postmortem; not "just a bug".
- Kill switch: a flag that disables the feature or falls back to a safe path within a minute, tested regularly.
- Human review queue: low-confidence or sensitive answers go to a person; use it also to gather labeled cases.
- Leaks of personal data may carry legal notice duties; involve security and privacy owners early.
- Preserve evidence: the logged prompt, config ID, and retrieved sources.

**Show** Runbook outline: detect | trigger kill switch | contain | assess affected users | notify | root cause | add eval case | postmortem.

**Check:** What should every bad-output incident add to the evaluation set? *(A case reproducing it, so it cannot return silently.)*

---

## SRC-022-L06 · Demo: rolling back a prompt change that broke refund answers (15 min)
**Goal:** detect and roll back a regressing prompt; prepares SRC-022-LAB1.

**Steps**
1. Show config v42 and the change in v43: a shorter prompt that drops refund-window wording.
2. Run the eval gate: refund cases fail; compare with v42 scores.
3. **Planned mistake:** ship v43 to a canary without the gate because the average score looked fine. Fix: add per-category thresholds so refund cases gate alone.
4. Watch the canary's escalation rate rise; abort the rollout.
5. Roll back to v42 by changing the config pointer; confirm via logged bundle IDs.
6. Add the failing cases to the eval set and write up the change.

**Check:** How was the rollback performed? *(By pointing back to the previous versioned configuration.)*

---

## SRC-022-L07 · Demo: an incident where the assistant revealed another customer's order (15 min)
**Goal:** run the incident end to end on the order-support assistant; prepares SRC-022-LAB1.

**Steps**
1. A customer reports seeing someone else's order details; declare the incident and a commander.
2. Trigger the kill switch; time it and confirm the feature is off.
3. Use logged config IDs and retrieved document IDs to find the cause: retrieval searched all orders and relied on the prompt to filter by customer.
4. **Planned mistake:** fix it by adding "never reveal other customers' data" to the prompt. Fix: enforce authorization in the retrieval and tool layer by the caller's identity.
5. Assess affected users from logs, involve security and privacy, and prepare notifications.
6. Re-enable behind a canary after an evaluation gate with cross-customer test cases; write the postmortem.

**Check:** Where should access control for customer data live? *(In deterministic code on the data path, not in the prompt.)*
