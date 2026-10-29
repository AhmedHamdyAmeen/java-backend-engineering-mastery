# ARC-045 · AI solution architecture — Exercises and lab

## Lab
### ARC-045-LAB1 · Larkspur AI assistant
**Outcomes:** 1–4 · **Time:** ~4 h
1. Write the use cases and choose the reference architecture for each.
2. Draw the C4 container view and the data-flow diagram, with the model reaching ERP and CRM only through governed APIs.
3. List the tools with read or write type and approval rules.
4. Choose the deployment option and justify it against data, latency, and cost.
5. Estimate cost and latency per conversation with stated assumptions.
6. Design the human handover and the fallback when the AI path is down.
7. Defend the architecture to role-played customer-service and security leads.
**Acceptance:** C4 container view, data flows, deployment choice justified, cost per conversation estimated, human handover designed.

## Exercises (case-based; six exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| ARC-045-EX01 | 1 | Choose assistant, retrieval, or agent for: store opening hours, returns-policy answers, "where is my parcel", "refund my order". Justify. |
| ARC-045-EX02 | 2 | A developer proposes giving the model a read-only database account on the ERP. Write the objection and the alternative. |
| ARC-045-EX03 | 3 | Choose hosted API, private endpoint, or self-hosted for Larkspur given customer names and order data in prompts and a three-person platform team. |
| ARC-045-EX04 | 4 | Estimate cost for 40,000 conversations per month, 6 turns each, with stated token assumptions and a placeholder price. |
| ARC-045-EX05 | 4 | Define five handover triggers and what the human agent receives. |
| ARC-045-EX06 | 2, 3 | Review a design with no audit of tool calls and a single provider with no fallback; give three corrections. |

## Solutions
- **EX01** Opening hours: retrieval or static page; returns policy: retrieval; parcel: agent with read tool; refund: agent proposes, human or customer-confirmed workflow executes, no direct refund tool.
- **EX02** Bypasses access rules, audit, and schema isolation, and exposes more data than needed; use a user-scoped order API returning only required fields.
- **EX03** Private endpoint or hosted API with approved terms, since a small team cannot run models; keep identifiers minimal; verify provider terms on retention and training use.
- **EX04** Per turn: input tokens (prompt + retrieved text + history) plus output tokens; sum across six turns, with history growing; multiply by price per token (placeholder) and by 40,000; add retrieval, hosting, and monitoring; show cost per conversation, not per call.
- **EX05** Low confidence, customer asks for human, refund or complaint, repeated failure, detected distress; agent gets transcript, summary, identified customer, and actions already taken.
- **EX06** Log each tool call with user, arguments, and result summary; add timeout and fallback to the human queue; add a second provider or a non-AI path.

Outcome 4 on latency is also covered by lab step 5.

**Workplace evidence:** an AI solution architecture you designed or reviewed.
