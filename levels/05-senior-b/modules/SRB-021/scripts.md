# SRB-021 · AI platform capabilities — Lecture scripts

**Video:** 88 min · **Running case:** The FulfillCo integration (Shop Platform acquires FulfillCo, a 10-year-old Java modular monolith on one PostgreSQL database; four teams integrate in real time and extract capabilities without stopping either business).
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## SRB-021-L01 · Why AI needs platform support (10 min)
**Goal:** see why AI features repeat the same hard problems across teams.

**Key points**
- Every team needs keys, quotas, cost tracking, privacy controls, and evaluation.
- Uncontrolled direct provider access causes cost surprises and data leaks.
- A platform gives safe defaults without blocking product work.
- Decide the line between central and product-owned.

**Show:** a map of four FulfillCo teams each calling a provider directly with their own keys, and the same map with a gateway in the middle.

**Check:** What problem do per-team provider keys create? *(Poor control, cost visibility, and security.)*

---

## SRB-021-L02 · The LLM gateway (14 min)
**Goal:** describe the central entry point for model calls.

**Key points**
- Functions: authentication, routing to models, quotas, redaction, logging, and cost attribution.
- One internal API hides provider differences and supports fallbacks.
- The gateway is critical: make it highly available and low latency.
- Keep prompt design out of the gateway.

**Show:** a diagram: team services -> gateway (auth, quota, redaction, logging, router) -> providers; a table of responsibilities versus non-goals.

**Check:** What does the gateway not own? *(Prompt design that belongs to product teams.)*

---

## SRB-021-L03 · Quotas, redaction, and cost attribution (12 min)
**Goal:** control usage, protect data, and charge costs correctly.

**Key points**
- Per-team quotas by tokens and requests, with burst limits and alerts.
- Redaction removes or tokenizes personal data before the model call and in logs.
- Cost attribution tags each call with team and feature; report per period.
- Isolation: one team's runaway usage must not exhaust another's quota.

**Show:** a quota config sketch (team, daily tokens, rate limit) and a redaction rule list (email, phone, address) with test cases.

**Check:** Why isolate quotas per team? *(So one runaway team cannot starve others.)*

---

## SRB-021-L04 · Shared retrieval services and data ownership (12 min)
**Goal:** offer embedding, indexing, and search with clear data ownership.

**Key points**
- Shared service gives embedding, vector indexing, and search APIs.
- Each team owns its data and index; the platform owns the machinery.
- Access control must follow source permissions; do not index data a user cannot see.
- Deletion and re-embedding must be supported.

**Show:** diagram: team corpora -> ingestion -> embedding -> per-team index namespaces -> search API with access filter.

**Check:** Who owns the data in a shared index? *(The team that supplied it.)*

---

## SRB-021-L05 · An AI golden path (10 min)
**Goal:** pre-wire a safe route for new AI features.

**Key points**
- Template with gateway client, config, and error handling.
- Evaluation harness with test sets and regression checks.
- Observability: traces, token use, latency, quality signals.
- Security checks: redaction tests, prompt injection tests, and dependency scans. Verify tooling before recording.

**Show:** a template checklist: gateway client, eval folder with sample cases, dashboard, security scan job, runbook.

**Check:** What does the golden path include for quality? *(An evaluation harness with test sets.)*

---

## SRB-021-L06 · Demo: four teams, one gateway, one cost report (15 min)
**Goal:** onboard the four teams to one gateway and report costs.

**Steps**
1. Register the four teams with keys and quotas.
2. Route calls from each team service through the gateway.
3. Simulate a runaway loop in one team and watch quota enforcement.
4. **Planned mistake:** use a single shared key for everyone; fix with per-team identity tags.
5. Generate the cost report per team and feature.

Prepares SRB-021-LAB1.

---

## SRB-021-L07 · Demo: redacting customer data before it reaches a model (15 min)
**Goal:** remove personal data from prompts and logs.

**Steps**
1. Send a sample support prompt with name, email, and address through the gateway.
2. Apply redaction rules and show the model receiving placeholders.
3. Check logs for unredacted data using a scan.
4. **Planned mistake:** redact only the prompt and log the raw request; fix by redacting before any log write.
5. Add tests with tricky formats and note the limits of pattern-based redaction.

Prepares SRB-021-LAB1.

---
