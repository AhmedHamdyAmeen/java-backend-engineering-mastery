# MID-062 · API evolution — Quiz

Outcomes: O1 classify changes · O2 schema registry and compatibility · O3 deprecation process · O4 tolerant reader.

**Q01 (O1)** Which change is usually compatible? A. Renaming a field B. Changing cents to euros C. Making a parameter required D. Adding an optional response field
**Q02 (O1)** Changing a price from cents to euros while keeping type `long` is: A. Compatible B. Only a documentation change C. Compatible with a default D. Breaking, because the meaning changed
**Q03 (O1)** A consumer that rejects an unknown field is: A. Tolerant B. Forward looking C. Strict and fragile to additive change D. Required by REST
**Q04 (O2)** BACKWARD compatibility means: A. Old schema reads new data B. No checks C. Both directions D. New schema reads data written with the old one
**Q05 (O2)** In Avro, adding a field safely under BACKWARD needs: A. A new topic B. A new subject C. Removing another field D. A default value
**Q06 (O2)** In Protobuf, a removed field's number should be: A. Reserved B. Reused C. Renumbered D. Set to zero
**Q07 (O3)** The correct order for retiring a field: A. Remove, announce, measure B. Measure, remove, announce C. Announce, measure, migrate, remove D. Migrate, remove, announce
**Q08 (O3)** Before removing a deprecated field you need: A. A new major version number B. Usage data showing who still depends on it C. Approval from QA only D. Nothing if it was announced
**Q09 (O4)** The tolerant-reader principle says: A. Read all fields and fail on extras B. Copy the provider DTO C. Validate the whole payload strictly D. Read only what you need and ignore the rest
**Q10 (O1)** Versioning every change is a mistake because: A. Versions are forbidden B. It breaks HTTP C. Registries do not allow it D. It multiplies versions to maintain; most changes can be additive

## Answers
Q01 D · Q02 D · Q03 C · Q04 D · Q05 D · Q06 A · Q07 C · Q08 B · Q09 D · Q10 D

## Practical part
Five exercises `MID-062-EX01` to `EX05` plus the lab. Pass: classification quiz at 80% or better and a lab where contract tests and the registry pass at every step.
