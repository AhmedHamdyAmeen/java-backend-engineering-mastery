# JNR-020 · API design conventions — Quiz

Outcomes: O1 DTO mapping · O2 consistent formats · O3 filtering · O4 versioning.

**Q01 (O1)** A main reason to use DTOs: A. They are faster B. Databases require them C. Annotations need them D. The API shape can change without exposing internals
**Q02 (O1)** MapStruct is: A. A mapper library that generates mapping code B. A web server C. A database D. A test framework
**Q03 (O1)** For a tiny model, a reasonable choice is: A. Plain mapping code B. Never mapping C. Return entities D. Reflection everywhere
**Q04 (O2)** Best way to send a price: A. `19.99` as double B. A float C. Integer minor units plus currency D. A free-text string
**Q05 (O2)** Best date format: A. `03/04/26` B. ISO 8601 with offset, e.g. `2026-04-03T10:00:00Z` C. `April 3rd` D. Local time with no offset
**Q06 (O2)** Enums are best sent as: A. Ordinal numbers B. Random codes C. Stable uppercase strings D. Class names
**Q07 (O2)** Why share one error shape? A. Clients handle all errors the same way B. It hides bugs C. It is required by HTTP D. It makes responses smaller
**Q08 (O3)** `GET /products?minPrice=500` means: A. Delete cheap items B. Only products costing at least 500 C. Sort by price D. Page 500
**Q09 (O4)** Which is a breaking change? A. Adding an optional field B. Adding a new endpoint C. Renaming a response field D. Adding a description
**Q10 (O4)** `/v2/products` is which strategy? A. Header versioning B. Media-type versioning C. No versioning D. URL versioning

## Answers
Q01 D · Q02 A · Q03 A · Q04 C · Q05 B · Q06 C · Q07 A · Q08 B · Q09 C · Q10 D

## Practical part
Six exercises `JNR-020-EX01` to `EX06` plus the style-guide lab. Pass: at least five exercises, a style guide, and no endpoint violating it.
