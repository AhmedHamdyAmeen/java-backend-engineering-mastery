# MID-024 · Communication models — Quiz

Outcomes: O1 sync vs async · O2 REST vs gRPC · O3 gRPC in Spring · O4 choose a style.

**Q01 (O1)** Synchronous calls couple services by: A. Language B. Package names C. Database vendor D. Availability at the same moment
**Q02 (O1)** Async messaging mainly helps with: A. Immediate answers B. Absorbing spikes and outages C. Removing the need for retries D. Strong consistency
**Q03 (O1)** A five-service synchronous chain is risky because: A. Availability and latency compound B. It uses JSON C. It uses HTTP D. It needs a broker
**Q04 (O2)** gRPC typically uses: A. XML over SOAP B. Plain text over FTP C. JSON over WebSocket D. Protocol Buffers over HTTP/2
**Q05 (O2)** Which is true about browsers and gRPC? A. They call gRPC natively B. They need gRPC-Web or a gateway C. gRPC needs no HTTP D. gRPC only works in browsers
**Q06 (O3)** Protocol Buffers fields are identified on the wire by: A. Name B. Order in the file C. Their number D. Their type
**Q07 (O3)** A safe, backward-compatible change to a message is: A. Renumbering a field B. Changing a field's type C. Reusing a removed field number D. Adding a new field with a new number
**Q08 (O3)** Every gRPC client call should have: A. A deadline B. A shared database C. A retry loop with no limit D. No timeout
**Q09 (O4)** A price lookup needed to render checkout should be: A. Fire-and-forget B. Asynchronous with no reply C. Synchronous D. Daily batch
**Q10 (O4)** In request/reply over messaging, the reply is matched with the request by: A. Queue name only B. Timestamp C. Message size D. Correlation ID

## Answers
Q01 D · Q02 B · Q03 A · Q04 D · Q05 B · Q06 C · Q07 D · Q08 A · Q09 C · Q10 D

## Practical part
Five exercises `MID-024-EX01` to `EX05` plus the lab. Pass: at least four exercises correct, an interaction map with justifications, and a working gRPC stock check with a deadline.
