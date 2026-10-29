# JNR-029 · Spring Data JPA — Quiz

Outcomes: O1 repositories · O2 derived queries · O3 JPQL and native queries · O4 projections and paging.

**Q01 (O1)** Who creates the implementation of a `JpaRepository` interface? A. You B. The database C. The JDK compiler D. Spring Data at startup
**Q02 (O1)** `findById` returns: A. The entity or null B. An `Optional` C. A list D. A `Page`
**Q03 (O2)** `findByNameContainingIgnoreCase(String)` produces: A. A case-insensitive "contains" search B. An exact match C. A delete D. A sort
**Q04 (O2)** A derived name that is 60 characters long should be: A. Kept B. Shortened by removing words C. Moved to `@Query` D. Turned into a native query
**Q05 (O3)** JPQL queries refer to: A. Entities and fields B. Tables and columns C. Files D. Indexes
**Q06 (O3)** Query input must be passed: A. Concatenated into the string B. As parameters C. In the URL D. As comments
**Q07 (O3)** Native queries are best used: A. By default B. Never C. Only for the main entity D. When JPQL cannot express the need
**Q08 (O4)** A projection is: A. A write model B. A migration C. A read-only view of selected data D. A cache
**Q09 (O4)** `Slice` differs from `Page` by: A. Having no total count query B. Returning entities only C. Being unsorted D. Needing native SQL
**Q10 (O4)** `PageRequest.of(0, 20)` means: A. Page 20, size 0 B. Page 1, size 20 C. All rows D. First page (index 0), 20 items

## Answers
Q01 D · Q02 B · Q03 A · Q04 C · Q05 A · Q06 B · Q07 D · Q08 C · Q09 A · Q10 D

## Practical part
Six exercises `JNR-029-EX01` to `EX06` plus the lab; the assessment is implementing three queries from requirements (EX02, EX04, EX06). Pass: all three assessment queries correct, at least five of six exercises correct, and lab tests green.
