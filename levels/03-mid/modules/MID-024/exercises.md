# MID-024 · Communication models — Exercises and lab

## Lab
### MID-024-LAB1 · Interaction map
**Outcomes:** 1–4 · **Time:** ~2.5 h
1. List every Shop interaction (place order, check stock, charge payment, send email, update search, and others).
2. Mark each sync or async and justify using coupling, latency, and failure impact.
3. Implement inventory's stock check as a gRPC service and a client in `orders` with a deadline.
4. Test behavior when `inventory` is down.
**Acceptance:** interaction map plus working gRPC call.

## Exercises (assessment: interaction-design review; five exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| MID-024-EX01 | 1 | Explain how an outage of `inventory` affects `orders` in a sync design and in an async design. |
| MID-024-EX02 | 1 | Compute the availability of a chain of four services each at 99.9%. |
| MID-024-EX03 | 2 | Make a REST vs gRPC table with contract, performance, tooling, and browser support for a public and an internal API. |
| MID-024-EX04 | 3 | Write a `.proto` for `GetProduct` and `ListProducts` (server streaming) and add a field without breaking clients. |
| MID-024-EX05 | 4 | Choose and justify a style for: price lookup at checkout, order confirmation email, stock decrement after payment, search index update. |

## Solutions
- **EX01** Sync: orders fails or must handle errors immediately. Async: orders accepts the request and the stock step completes when inventory returns; the user sees a pending state.
- **EX02** About 0.999^4 = 0.996, so about 99.6%.
- **EX03** Public: REST (browser support, curl, OpenAPI). Internal: gRPC (strict contract, binary, streaming, generated clients).
- **EX04** Add `optional string description = 5;` with a new number, never reusing existing ones; keep `rpc ListProducts (Query) returns (stream Product);`.
- **EX05** Price lookup: sync. Email: async. Stock decrement: async event or saga step. Search index: async event. Justify by whether the caller needs the answer now.
