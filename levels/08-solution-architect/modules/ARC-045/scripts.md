# ARC-045 · AI solution architecture — Lecture scripts

**Video:** 70 min · **Running case:** *Larkspur Retail* — a mid-size retailer with 120 stores and a dated on-premises web shop; you are the solution architect for a new platform integrated with the existing ERP and CRM.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## ARC-045-L01 · AI reference architectures (12 min)
**Goal:** pick between assistant, retrieval over enterprise content, and agent with tools for a given capability.

**Key points**
- Assistant: a model answers from its general knowledge and the conversation; simple, but knows nothing about your orders.
- Retrieval over enterprise content (RAG): the system fetches relevant documents first and gives them to the model to answer from.
- Agent with tools: the model chooses actions, such as "look up order", through tools your platform exposes.
- Start with the simplest that meets the need; each step adds risk, cost, and testing.

**Show:** a three-row table of reference architectures with columns "what the model sees", "can it change data", "main risk", and a Larkspur example per row (generic FAQ bot, returns-policy answers, order-status lookup).

**Check:** Which architecture suits "answer from our returns policy"? *(Retrieval over enterprise content.)*

---

## ARC-045-L02 · Grounding AI in enterprise data (12 min)
**Goal:** connect AI to ERP, CRM, and knowledge bases through governed interfaces.

**Key points**
- Grounding means answers are based on retrieved company facts, not model memory.
- The model never connects to the ERP or CRM database; it calls governed APIs or reads curated indexes.
- Pass the end user's identity so the AI sees only what that user may see.
- Index knowledge-base content with owners, freshness dates, and a way to remove outdated articles.

**Show:** a flow: customer message, assistant service, order API (user-scoped token), policy index, model, response; with the ERP behind the API, not reachable from the model.

**Check:** Why call an API rather than query the database? *(The API enforces access rules, limits, and audit, and keeps the schema private.)*

---

## ARC-045-L03 · Agents and tools over enterprise systems (10 min)
**Goal:** design tool-using agents with limited authority.

**Key points**
- A tool is a described function the model may request; your code runs it, not the model.
- Give read tools freely; put write tools (refund, address change) behind confirmation or human approval.
- Limit steps, spend, and time per task; log every tool call.
- Each tool returns only needed fields; extra data is extra leakage risk.

**Show:** a tool table for the assistant: `getOrderStatus` (read), `getReturnPolicy` (read), `createReturnRequest` (write, needs customer confirm), `refund` (not exposed; human agent only).

**Check:** Who executes a tool call? *(Your platform code; the model only proposes it.)*

---

## ARC-045-L04 · Deployment options and their trade-offs (10 min)
**Goal:** choose hosted API, private endpoint, or self-hosted against data, latency, and cost.

**Key points**
- Hosted API: fastest to start and strong models; data leaves your boundary, so check provider terms.
- Private endpoint: provider model in your cloud tenancy network; better control, similar models, may cost more.
- Self-hosted: full control and fixed hardware cost; you run capacity, updates, and safety; model quality may be lower.
- Decide from data class, latency target, volume, and team skills; verify current provider terms before deciding.

**Show:** a decision table with three options against data sensitivity, latency, cost shape (per use vs fixed), and operations load.

**Check:** What is the main drawback of self-hosting? *(You carry the operations, capacity, and update work, and may get lower model quality.)*

---

## ARC-045-L05 · Demo: architecture of the Larkspur customer-service assistant (14 min)
**Goal:** design the assistant as a C4 container view with data flows and handover; prepares ARC-045-LAB1.

**Steps**
1. Collect the use cases: order status, return start, product questions, and "talk to a person".
2. Draw containers: chat widget, assistant service, policy and product index, order and customer APIs (backed by ERP and CRM), model endpoint, and the agent-desk handover.
3. Mark data flows and what each carries; the model receives only the question, retrieved text, and selected order fields.
4. **Planned mistake:** give the assistant read access to the CRM database "for speed". Fix: replace it with a customer-summary API scoped to the signed-in customer, with audit logging.
5. Design handover: triggers (low confidence, angry customer, refund request, customer asks) pass the transcript and summary to the human queue.
6. Choose a deployment option with reasons and note the open provider-term checks.

---

## ARC-045-L06 · Demo: costing the assistant per conversation (12 min)
**Goal:** estimate cost and latency per conversation, not per request, and design fallbacks.

**Steps**
1. Gather volumes with customer service: conversations per month, turns per conversation, share that hand over.
2. Estimate tokens per turn: system prompt, retrieved text, history, and answer; the history grows each turn.
3. Multiply by the provider's price per input and output token (verify current prices before recording) to get cost per conversation.
4. **Planned mistake:** cost one request and multiply by conversations. Fix: sum all turns, including retrieval and retries, then add vector search and hosting costs.
5. Estimate latency end to end: retrieval, tool calls, model; set a timeout.
6. Define fallbacks: after timeout show a static help page; during provider outage route to the human queue; compare cost against a human-handled conversation.
