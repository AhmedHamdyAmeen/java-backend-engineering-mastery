# MID-069 · Tool calling and agents — Exercises and lab

## Lab
### MID-069-LAB1 · Assistant with tools
**Outcomes:** 1–5 · **Time:** ~3.5 h
Give the order-support assistant read-only tools (order status, shipment tracking) that call Shop Platform services with the customer's token, and a "request refund" tool that only creates a pending request for a human agent. Add step, time, and cost limits to the agent loop.
**Acceptance:** a customer can never see another customer's order through the assistant (test); no tool with side effects executes without approval; loops stop at the configured step and cost limits.

## Exercises (assessment: tool-design review)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-069-EX01 | 1 | Draw the sequence of one tool call and mark which steps the model does and which the application does. |
| MID-069-EX02 | 2 | Redesign `run_sql(query)` into three narrow tools with typed parameters and error results. |
| MID-069-EX03 | 3 | Review a tool that takes `userId` as an argument; fix it so identity comes from the session. |
| MID-069-EX04 | 4 | Add an idempotency key and a pending-approval state to `cancel_order`. |
| MID-069-EX05 | 4 | Write a loop with step, time, and cost limits and a test where each limit stops it. |
| MID-069-EX06 | 5 | Write a half-page note: would you adopt MCP for Shop's three tools? State the trigger that would change your answer. |
| MID-069-EX07 | 2–4 | Review a provided tool set; list authorization, idempotency, and approval gaps with fixes. |

## Solutions
- **EX01** Model: proposes name and arguments, writes the final answer. Application: validates, authorizes, executes, returns the result.
- **EX02** `get_order_status(orderId)`, `list_my_orders(page)`, `get_shipment(orderId)`; each with a positive-long or bounded page parameter and `NOT_FOUND`/`NOT_ALLOWED` errors.
- **EX03** Remove `userId`; read the subject from the authenticated token and forward the token downstream.
- **EX04** Tool creates `PENDING` request keyed by `(orderId, action)`; repeat calls return the same request; a human endpoint moves it to `APPROVED`/`EXECUTED`.
- **EX05** `for (step = 0; step < maxSteps && elapsed < maxTime && cost < maxCost; step++)`; tests use a fake model that always asks for another call.
- **EX06** Three tools in one app: no, a direct tool interface is simpler; adopt MCP when several assistants or teams must share tools. Authorization is needed either way.
- **EX07** Typical gaps: service-account calls, model-supplied user id, refund executing directly, no idempotency key, no limits; fix each as in EX03-EX05.

**Outcome 1** is also checked by quiz Q01-Q03; outcome 5 by quiz Q09-Q10 and EX06.
