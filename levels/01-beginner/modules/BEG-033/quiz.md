# BEG-033 · Date and time — Quiz

Outcomes: O1 choosing types · O2 Duration and Period · O3 formatting and parsing · O4 UTC storage.

**Q01 (O1)** Best type for a birthday: A. `Instant` B. `ZonedDateTime` C. `Date` D. `LocalDate`
**Q02 (O1)** Best type for a database "created at" timestamp: A. `Instant` B. `LocalDate` C. `LocalTime` D. `String`
**Q03 (O1)** Which type is NOT a specific moment on the global timeline? A. `ZonedDateTime` B. `Instant` C. `LocalDateTime` D. `OffsetDateTime`
**Q04 (O1)** An event in several time zones should use: A. `LocalDateTime` B. `ZonedDateTime` or `Instant` C. `int` D. `LocalTime`
**Q05 (O2)** For hours and minutes use: A. `Period` B. `Duration` C. `LocalDate` D. `Year`
**Q06 (O2)** For years, months, days use: A. `Duration` B. `Instant` C. `Period` D. `ZoneId`
**Q07 (O3)** In `DateTimeFormatter` patterns, `MM` means: A. Minutes B. Milliseconds C. Midnight D. Month
**Q08 (O3)** `LocalDate.plusDays(5)`: A. Changes the original B. Returns a new object C. Throws D. Returns void
**Q09 (O4)** Why store timestamps in UTC? A. It is shorter B. It has no daylight saving and is one fixed reference C. It is required by Java D. It hides data
**Q10 (O1)** Which should you avoid in new code? A. `java.util.Date` B. `Instant` C. `LocalDate` D. `ZoneId`

## Answers
Q01 D · Q02 A · Q03 C · Q04 B · Q05 B · Q06 C · Q07 D · Q08 B · Q09 B · Q10 A

## Practical part
Three exercises `BEG-033-EX01` to `EX03` plus the lab. Pass: all three exercises correct and the lab correct across a daylight-saving change.
