# MID-069 · Tool calling and agents — Quiz

Outcomes: O1 how tool calling works · O2 tool design · O3 authorization · O4 approval and loop limits · O5 MCP.

**Q01 (O1)** In tool calling, the model: A. Proposes a call with arguments B. Executes the tool itself C. Stores the result in the database D. Validates the user's token
**Q02 (O1)** Tool arguments produced by the model should be treated as: A. Trusted B. Verified by the model already C. Untrusted input to validate D. Only strings
**Q03 (O1)** After the tool runs, its result is: A. Discarded B. Shown only in logs C. Sent to the user unchanged always D. Sent back to the model to continue
**Q04 (O2)** Which tool is best designed? A. `run_sql(query)` B. `call_api(url, body)` C. `get_order_status(orderId)` D. `do_anything(text)`
**Q05 (O2)** A good error result is: A. A full stack trace B. An empty reply C. A short code such as `NOT_ALLOWED` D. A random string
**Q06 (O3)** Tool calls should run with: A. A powerful service account B. The model's own identity C. No identity D. The end user's identity
**Q07 (O3)** Who decides whether a refund is allowed? A. Application code and policy B. The model C. The user's prompt D. The tool description
**Q08 (O4)** A refund tool should: A. Pay immediately B. Create a pending request for approval C. Retry until success D. Skip logging
**Q09 (O4)** Why use an idempotency key? A. A retried call does not repeat the effect B. To encrypt arguments C. To speed up calls D. To pick the model
**Q10 (O5)** MCP is: A. A database engine B. A standard for exposing tools and data to models C. A Java framework only D. A payment protocol

## Answers
Q01 A · Q02 C · Q03 D · Q04 C · Q05 C · Q06 D · Q07 A · Q08 B · Q09 A · Q10 B

## Practical part
Seven exercises `MID-069-EX01` to `EX07` (EX07 is the tool-design review) plus the assistant lab. Pass: at least five exercises including EX07, and a lab where the ownership test passes and no side-effect tool runs without approval.
