# MID-069 · Tool calling and agents — Lecture scripts

**Video:** 80 min · **Analogy used throughout:** a junior clerk who may only fill in request forms; the clerk proposes, the office checks the badge and decides. Running project: Shop.
Format: **Goal** · **Key points** · **Show** · **Check**.
Version note: tool-calling APIs and the Model Context Protocol change quickly; verify version before recording and name the API used.

---

## MID-069-L01 · From answering to acting (8 min)
**Goal:** see why letting a model act changes the risk profile.

**Key points**
- An answering assistant can be wrong; an acting assistant can be wrong and change data.
- Typical Shop actions: look up an order, track a shipment, request a refund.
- The model is a proposer: it produces text, including a proposed action. Your code is the actor.
- Every extra capability is attack surface (preview of MID-071).

**Show:** two columns: "answers" (explain return policy) versus "acts" (cancel order 42), with the failure cost of each.

**Check:** Who executes an action the model suggests? *(The application, after its own checks.)*

---

## MID-069-L02 · How tool calling works (12 min)
**Goal:** trace one tool call through the loop.

**Key points**
- You send the model a list of tool definitions: name, description, JSON schema of parameters.
- The model replies with a tool call (name plus arguments), not with an executed result.
- Your code validates the arguments, decides whether to run, runs the tool, and sends the result back.
- The model then writes the final answer, or proposes another call.
- Arguments are untrusted input, exactly like an HTTP request body.

**Show:** sequence: user question → model returns `get_order_status{orderId:42}` → app validates and calls `orders` → result returned to model → final answer.

**Check:** Does the model call your service directly? *(No; your application does, after validation.)*

---

## MID-069-L03 · Designing safe tools (10 min)
**Goal:** design tools that are hard to misuse.

**Key points**
- Narrow scope: `get_order_status(orderId)`, not `run_sql(query)` or `call_any_api(url)`.
- Typed, constrained parameters: enums, ranges, patterns; reject everything else.
- Idempotency: the same call twice has the same effect.
- Clear error results ("not found", "not allowed") so the model can explain, without leaking internals.
- Return only the fields the answer needs.

**Show:**
```java
record OrderStatusArgs(@Positive long orderId) {}
// result: {status:"SHIPPED", eta:"2026-11-02"}  or  {error:"NOT_FOUND"}
```

**Check:** Why is `run_sql` a bad tool? *(It is unbounded; one bad argument reads or destroys anything.)*

---

## MID-069-L04 · Authorization and identity for tool calls (10 min)
**Goal:** make every tool call run as the end user.

**Key points**
- The tool call carries the customer's token (from the session), never a shared service account.
- The downstream service checks ownership exactly as it does for the customer's own request.
- Never put the user id in a model-controlled argument; take it from the authenticated context.
- Whether an action is allowed is decided by code and policy, never by the model's judgment ("the user seems entitled").

**Show:** diagram: customer token → assistant backend → `orders` API (ownership check) → 403 for someone else's order; the model sees only `{error:"NOT_ALLOWED"}`.

**Check:** Where does the user id for a tool call come from? *(The authenticated session, not the model.)*

---

## MID-069-L05 · Side effects, idempotency, and human approval (8 min)
**Goal:** control tools that change things.

**Key points**
- Classify tools: read-only, reversible write, irreversible or money-moving.
- Side-effect tools create a pending request; a human (or explicit user confirmation) approves.
- Use idempotency keys so a retried call does not refund twice.
- Log who requested, who approved, and the arguments.

**Show:** state machine: `PENDING → APPROVED → EXECUTED` or `REJECTED`; the tool only creates `PENDING`.

**Check:** Why can an agent loop double-refund? *(It retries a non-idempotent tool after a timeout.)*

---

## MID-069-L06 · Agent loops and their limits; MCP as a concept (7 min)
**Goal:** bound loops and understand MCP.

**Key points**
- An agent loop repeats call-tool-then-think until done; without limits it can run forever and cost a lot.
- Set limits on steps, wall-clock time, and tokens or cost; stop with a clear message.
- MCP (Model Context Protocol) is a standard way for an app to discover and call tools and data exposed by a server.
- Worth adopting when many assistants or tools must interoperate; overhead for one app with three tools. Authorization still applies to every MCP tool.

**Show:** config: `maxSteps=6, maxSeconds=30, maxCostUsd=0.10`.

**Check:** Name two limits for an agent loop. *(Any two of steps, time, cost.)*

---

## MID-069-L07 · Demo: an order-status tool that respects ownership (12 min)
**Goal:** build a read-only tool that cannot leak another customer's order. Prepares `MID-069-LAB1`.

**Steps**
1. Define `get_order_status(orderId)` with a typed schema.
2. Execute it by calling `orders` with the customer's bearer token.
3. Return a trimmed result or `NOT_ALLOWED`/`NOT_FOUND` (same shape for both, to avoid probing).
4. Write the test: customer A asks for customer B's order and gets no data.
5. **Planned mistake:** use a service account for the call; the test fails because B's order is visible. Fix by forwarding the user token.
6. Show the trace of the call in logs without the token value.

---

## MID-069-L08 · Demo: a refund request routed to human approval (13 min)
**Goal:** add a side-effect tool that only creates a pending request. Prepares `MID-069-LAB1`.

**Steps**
1. Define `request_refund(orderId, reason)`; it inserts a `PENDING` refund request.
2. Add an idempotency key (order id plus reason hash); a repeat returns the existing request.
3. Build the approval endpoint used by a support agent; only that role can execute the refund.
4. Add loop limits (steps, time, cost) and show the loop stopping.
5. **Planned mistake:** let the tool call the payment API directly "to save a step"; the test "no side effect without approval" fails. Fix by moving execution behind approval.
6. Show the audit record: requester, approver, arguments.
