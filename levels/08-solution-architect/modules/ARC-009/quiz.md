# ARC-009 · Enterprise integration — Quiz

Outcomes: O1 integration styles · O2 choosing style per interface · O3 integration landscape and canonical data · O4 error handling and ownership.

**Q01 (O1)** Events compared with synchronous APIs mainly give: A. Immediate answers B. Looser coupling with eventual consistency C. Less monitoring D. No duplicates
**Q02 (O1)** An iPaaS is best described as: A. A database B. A load balancer C. A cloud integration service with connectors D. A message format
**Q03 (O1)** A risk of an ESB is: A. No transformation B. No routing C. Cannot run on premises D. Becoming a central bottleneck holding business logic
**Q04 (O2)** The ERP supports only nightly files for posting. The suitable style is: A. Synchronous API B. Batch file exchange with safeguards C. Events directly D. Screen scraping
**Q05 (O2)** Payment authorization needs an immediate answer, so use: A. Batch B. Synchronous API C. Nightly file D. Email
**Q06 (O2)** Which does NOT drive the choice of integration style? A. Latency B. Volume C. Ownership D. The logo of the vendor
**Q07 (O3)** A canonical model is most useful when: A. Many systems exchange the same few stable entities B. Each pair has unique needs C. No one owns it D. Data is unstructured
**Q08 (O3)** A canonical model has gone wrong when it: A. Is documented B. Is versioned C. Is slow to change and satisfies nobody D. Has an owner
**Q09 (O4)** Safe retries require: A. Larger queues B. Idempotent processing C. Manual steps D. Shorter timeouts
**Q10 (O4)** A dead-letter queue holds: A. Messages that cannot be processed after retries B. Successful messages C. Logs D. Configuration

## Answers
Q01 B · Q02 C · Q03 D · Q04 B · Q05 B · Q06 D · Q07 A · Q08 C · Q09 B · Q10 A

## Practical part
Integration design review of the lab catalog and diagram plus exercises `ARC-009-EX01` to `EX06`. Pass: quiz at least 8/10, at least five of six exercises correct, and a catalog where every interface justifies its style and has defined failure handling.
