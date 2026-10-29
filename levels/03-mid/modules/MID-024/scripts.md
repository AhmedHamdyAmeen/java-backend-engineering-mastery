# MID-024 · Communication models — Lecture scripts

**Video:** 60 min · **Analogy used throughout:** a phone call versus a voicemail or letter: a call needs both sides present; a letter does not.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## MID-024-L01 · Sync vs async (10 min)
**Goal:** compare the two styles by coupling, latency, and failure.

**Key points**
- Synchronous: the caller waits for the answer (HTTP, gRPC). Simple, immediate result.
- Asynchronous: the caller sends a message and continues (broker). Decoupled in time, harder to reason about.
- Sync couples availability: if `inventory` is down, `orders` fails too.
- Async absorbs spikes and outages, but the result arrives later and must be tracked.
- Use sync for queries needing an answer now; async for work that can finish later.

**Show:** two sequence sketches for "place order": a sync chain versus `OrderPlaced` published to a broker.

**Check:** Which style needs both services up at the same moment? *(Synchronous.)*

---

## MID-024-L02 · Temporal coupling (8 min)
**Goal:** recognize and reduce temporal coupling.

**Key points**
- Temporal coupling: A can only work while B is available right now.
- Availability multiplies: three services at 99.9% each give about 99.7% for a chain.
- Long synchronous chains also add up latency and failure.
- Reduce it with async messaging, local copies of read data, or fewer hops.
- Not every call must be removed; keep those where the user waits for the answer.

**Show:** a chain `gateway → orders → inventory → pricing → catalog` marked with the availability maths.

**Check:** Why is a five-service synchronous chain risky? *(Availability and latency multiply or add across it.)*

---

## MID-024-L03 · REST vs gRPC (10 min)
**Goal:** pick between them using four criteria.

**Key points**
- Contract: REST commonly uses OpenAPI (optional); gRPC requires a `.proto` file and generates code.
- Performance: gRPC uses binary Protocol Buffers over HTTP/2, usually smaller and faster; REST commonly sends JSON over HTTP/1.1 or HTTP/2.
- Tooling: REST is easy to test with curl and browsers; gRPC needs special clients (grpcurl).
- Browsers cannot call gRPC directly; they need gRPC-Web or a gateway.
- Typical split: REST for public APIs, gRPC for internal service-to-service calls with strict contracts.

**Show:** a comparison table with contract, format, streaming, browser support, and debugging.

**Check:** Can a browser call a gRPC service directly? *(No; it needs gRPC-Web or a gateway.)*

---

## MID-024-L04 · gRPC and Protocol Buffers (12 min)
**Goal:** define a service in `.proto` and understand the call types.

**Key points**
- A `.proto` file defines messages (typed, numbered fields) and services (methods).
- Field numbers identify fields on the wire; never reuse or renumber them. Adding fields is backward compatible.
- Four call types: unary, server streaming, client streaming, bidirectional streaming.
- Set a deadline on every client call; deadlines propagate and replace ad-hoc timeouts.
- In Spring, use a gRPC starter such as Spring gRPC or `grpc-spring-boot-starter` (verify the current choice and version before recording).

**Show**
```proto
syntax = "proto3";
service InventoryService {
  rpc CheckStock (StockRequest) returns (StockReply);
}
message StockRequest { string sku = 1; int32 quantity = 2; }
message StockReply   { bool available = 1; int32 on_hand = 2; }
```

**Check:** Why never renumber a proto field? *(Existing clients identify fields by number and would misread data.)*

---

## MID-024-L05 · Request/reply over messaging (8 min)
**Goal:** get an answer through a broker when needed.

**Key points**
- Request/reply: the requester sends a message with a correlation ID and a reply-to address; the responder answers on that queue.
- It keeps temporal decoupling for the sender's transport, but the caller still waits, so it is not free of failure handling.
- Needs a timeout and handling of late or duplicate replies.
- Prefer plain sync calls for simple queries; use this when a broker is already the integration channel.
- Do not use async for queries that need an immediate answer.

**Show:** a diagram: request queue, reply queue, `correlationId` copied from request to reply.

**Check:** What links a reply to its request? *(The correlation ID.)*

---

## MID-024-L06 · Demo: the same call in REST and gRPC (12 min)
**Goal:** implement inventory's stock check twice and compare. Prepares `MID-024-LAB1`.

**Steps**
1. Implement `GET /stock/{sku}` in `inventory` with Spring MVC and call it from `orders`.
2. Write `inventory.proto`; generate stubs with the build plugin.
3. Implement the gRPC service and call it from `orders` with a deadline of 500 ms.
4. Compare payload sizes and latency with a quick benchmark (note it is indicative only).
5. **Planned mistake:** renumber a proto field and show the old client reading garbage; restore the number and add a new field instead.
6. Stop `inventory` and compare how each client reports the failure.

---
