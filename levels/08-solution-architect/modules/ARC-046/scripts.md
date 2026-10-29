# ARC-046 · AI security, privacy, and compliance architecture — Lecture scripts

**Video:** 58 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM, now adding a customer and staff AI assistant.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-046-L01 · Data classification for AI (10 min)
**Goal:** classify the data that can reach, pass through, or leave an AI feature, and set a rule for each class.

**Key points**
- Data can enter a model in three places: the prompt (user input), retrieved content (documents, orders), and tool results; it can leave in outputs and logs.
- Use the company's classes (public, internal, confidential, restricted) and add AI-specific rules: what may be sent to which model, and what may be stored.
- Payment card data and credentials are never allowed; personal data only with a purpose, minimization, and masking.
- Enforce by design: filter or tokenize before the model call, not by asking the model to ignore it.
- Classify outputs too: an answer built from confidential documents is confidential.

**Show:** a table for the Larkspur assistant: class, examples (public product text, order status, customer name and address, card number), allowed to hosted model? (yes, masked, no), logging rule.

**Check:** Where can sensitive data enter an AI feature? *(Prompts, retrieved content, and tool results, and it can leave through outputs and logs.)*

---

## ARC-046-L02 · Provider terms: residency, retention, training use (12 min)
**Goal:** check AI provider terms against company policy and reflect them in the architecture and contract.

**Key points**
- Questions for every provider: where is data processed and stored, how long is it kept, is it used to train models, who are the sub-processors, and what are the breach terms.
- Defaults are not policy: consumer-grade and enterprise terms differ, and options such as zero or limited retention may need to be requested or configured.
- Residency and cross-border rules may restrict regions; confirm region options and any fallback routing.
- Capture terms in the contract and a data processing agreement; ask legal and privacy to review.
- Terms change: record the version reviewed and review again on provider updates. Verify before recording any specific provider term.

**Show:** a provider-terms checklist for Larkspur: processing region, retention, training use, sub-processors, deletion on request, audit rights, incident notice, exit and data return; each with status and evidence.

**Check:** Why not rely on provider defaults? *(They may not meet company policy; terms must be checked, configured, and contracted.)*

---

## ARC-046-L03 · Architectural guardrails (12 min)
**Goal:** place guardrails in the architecture so they hold even when the prompt is bypassed.

**Key points**
- Prompt injection: untrusted text (a customer message, a web page, a document) tries to steer the model. Treat all model input as untrusted and output as untrusted.
- Data leakage: limit what the model can see by access-controlled retrieval using the end user's permissions, plus output filters.
- Excessive agency: give the assistant the minimum tools, read-only by default, with confirmation or human approval for actions like refunds.
- Put controls in code and infrastructure: input and output filtering, schema validation of tool calls, allowlists, rate limits, and scoped credentials. Prompts alone are not a control.
- Layer them: no single guardrail is relied on.

**Show:** a flow for the Larkspur assistant: user, input filter, retrieval with user's entitlements, model, output filter, tool gateway (allowlist, scopes, approval step for refunds), audit log.

**Check:** Why is a prompt instruction alone not a guardrail? *(The model can be manipulated or ignore it; real controls must be enforced outside the model.)*

---

## ARC-046-L04 · Auditability and data-subject rights (10 min)
**Goal:** make AI outcomes auditable and support deletion and access requests for data used by AI features.

**Key points**
- Log what is needed to explain an outcome: request id, user, model and prompt version, retrieved sources, tool calls, and response, with sensitive content masked.
- Balance audit and privacy: keep the minimum, with retention periods and access controls on the logs.
- Data-subject rights (access, correction, deletion) must reach conversation logs, vector indexes, caches, and evaluation datasets.
- Design a deletion path early: index entries tied to source records so deleting a customer removes derived data.
- Keep a record of automated decisions affecting customers and a route to human review.

**Show:** a data map: where Larkspur customer data lands in AI features (conversation log, vector index, cache, evaluation set) with the deletion mechanism and retention for each.

**Check:** Name two places beyond the main database where deletion must reach. *(For example conversation logs and vector indexes; also caches and evaluation sets.)*

---

## ARC-046-L05 · Demo: threat-modeling the Larkspur assistant (14 min)
**Goal:** threat-model the Larkspur assistant and turn findings into design controls. This prepares ARC-046-LAB1.

**Steps**
1. Draw the data flow: customer or staff user, assistant service, retrieval over product, order, and policy content, model provider, tool gateway to order and refund services, logs.
2. Mark trust boundaries: user to service, service to provider, tool gateway to internal systems.
3. **Planned mistake:** rely on the system prompt ("never reveal card numbers"). A tester pastes a card number into chat and an injected instruction in a product review makes the assistant echo it. Fix: mask card patterns at the input filter and never log them, filter outputs, and keep card data out of retrieved content.
4. List threats per boundary (injection, cross-customer leakage, over-powered refund tool, provider retention, log exposure) with a control and owner for each.
5. Add residual risks and test cases to the assurance plan, and record the decisions.
6. Review with the role-played security and privacy officer and confirm no payment card data can reach the model.

**Check:** What was the planned mistake? *(Relying on the prompt as the control instead of enforcing masking and filtering in the architecture.)*
