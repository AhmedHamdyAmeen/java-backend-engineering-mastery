# BEG-033 · Date and time — Lecture scripts

**Video:** 48 min · **Analogy used throughout:** a wall of world clocks showing one moment in many cities.
Format: **Goal** · **Key points** · **Show** · **Check**.

---

## BEG-033-L01 · Why time is hard (8 min)
**Goal:** see why dates need careful types.

**Key points**
- Time zones differ; the same moment has different clock times around the world.
- Daylight saving makes some days 23 or 25 hours long.
- Months have different lengths; leap years exist.
- The old `java.util.Date` and `Calendar` are confusing; use the `java.time` package instead.
- `java.time` objects are immutable: operations return new objects.

**Show:** the same moment shown on clocks in Riyadh, London, and New York.

**Check:** Which package should you use for dates today? *(`java.time`.)*

---

## BEG-033-L02 · Local dates and times (10 min)
**Goal:** use dates without a time zone.

**Key points**
- `LocalDate`: a date only (2026-03-15). Good for birthdays and deadlines.
- `LocalTime`: a time of day only.
- `LocalDateTime`: date plus time, but no zone. It is not a specific moment.
- Create with `of(...)`, `now()`, or `parse(...)`.
- Change with `plusDays`, `minusMonths`; each returns a new object.

**Show**
```java
LocalDate d = LocalDate.of(2026, 3, 15);
LocalDate next = d.plusDays(30);
```

**Check:** Does `LocalDateTime` know its time zone? *(No.)*

---

## BEG-033-L03 · Instants and time zones (12 min)
**Goal:** represent an exact moment and show it in any zone.

**Key points**
- `Instant`: a point on the global timeline (UTC). Good for timestamps.
- `ZoneId`: a region such as `Asia/Riyadh`. Prefer region names over fixed offsets because they know daylight saving rules.
- `ZonedDateTime`: date, time, and zone together.
- Convert with `withZoneSameInstant`: same moment, different clock.
- Rule: store timestamps in UTC; convert to the user's zone only for display.

**Show**
```java
ZonedDateTime riyadh = ZonedDateTime.of(2026, 5, 4, 10, 0, 0, 0, ZoneId.of("Asia/Riyadh"));
ZonedDateTime london = riyadh.withZoneSameInstant(ZoneId.of("Europe/London"));
Instant stored = riyadh.toInstant();
```

**Check:** Which type fits "when was this row created"? *(`Instant`, stored as UTC.)*

---

## BEG-033-L04 · Durations, periods, formatting (10 min)
**Goal:** measure gaps and print or read dates.

**Key points**
- `Duration`: time-based amount (hours, minutes, seconds). `Duration.between(t1, t2)`.
- `Period`: date-based amount (years, months, days). `Period.between(d1, d2)`.
- `ChronoUnit.DAYS.between(a, b)` counts whole days.
- `DateTimeFormatter.ofPattern("dd/MM/yyyy")` formats and parses.
- Patterns are case-sensitive: `MM` is month, `mm` is minute.

**Show**
```java
DateTimeFormatter f = DateTimeFormatter.ofPattern("dd/MM/yyyy");
LocalDate d = LocalDate.parse("15/03/2026", f);
long days = ChronoUnit.DAYS.between(LocalDate.now(), d);
```

**Check:** Which is for hours and minutes: `Duration` or `Period`? *(`Duration`.)*

---

## BEG-033-L05 · Demo: a meeting across time zones and a daylight-saving change (8 min)
**Goal:** schedule and convert a meeting. Prepares `BEG-033-LAB1`.

**Steps**
1. Create a `ZonedDateTime` for a meeting at 09:00 in `Europe/London`.
2. Convert to `Asia/Riyadh` and `America/New_York` with `withZoneSameInstant` and print with a formatter.
3. Pick a date near a daylight-saving change (verify the current year's dates before recording) and show the offset differences.
4. **Planned mistake:** use `LocalDateTime` for the meeting and see that it cannot convert; fix with `ZonedDateTime`.
5. Compute days until a deadline with `ChronoUnit.DAYS`.
