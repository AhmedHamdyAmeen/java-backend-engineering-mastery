# BEG-033 · Date and time — Exercises and lab

## Lab
### BEG-033-LAB1 · Meeting planner
**Outcomes:** 1–4 · **Time:** ~1.5 h
Schedule a meeting in one time zone and show it in three others. Compute days until a deadline. Store the meeting as an `Instant` and explain in a comment why.
**Acceptance:** correct across a daylight-saving change.

## Exercises (assessment: three exercises)
| ID | Outcome | Task |
| --- | --- | --- |
| BEG-033-EX01 | 1 | Choose the type for each: a birthday; a log timestamp; a flight departure with its city's zone; "9 am every day" alarm. |
| BEG-033-EX02 | 2, 3 | Compute the days between today and 31 December, and the hours between 08:30 and 17:45. Then print a date as `15 Mar 2026`. |
| BEG-033-EX03 | 4 | Write two sentences on why a database should store UTC timestamps and convert at display time. |

## Solutions
- **EX01** `LocalDate`; `Instant`; `ZonedDateTime`; `LocalTime`.
- **EX02** `ChronoUnit.DAYS.between(LocalDate.now(), LocalDate.of(year, 12, 31))`; `Duration.between(LocalTime.of(8,30), LocalTime.of(17,45)).toHours()` gives 9 (hours part; `toMinutes()` gives 555); format with `ofPattern("dd MMM yyyy")`.
- **EX03** UTC has no daylight saving and is one fixed reference, so sorting and comparing are correct and data from many zones agrees. Each user then sees their own local time, converted when displayed.
- Outcome 2 is also covered by the lab and quiz Q05–Q06.
