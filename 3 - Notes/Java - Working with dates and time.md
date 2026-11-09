Tags: [[_Java]] [[__Programming_languages]]
#Java #ProgrammingLanguages 

# Introduction
Java provides a modern date and time API called `java.time`, introduced in Java 8. It is the recommended way to work with dates, times, durations, time zones, and timestamps.

The most important thing to understand is that Java distinguishes between several concepts:
- Date – a calendar date, e.g. November 7, 2026.    
- Time – a time of day, e.g. 14:30.    
- Date and time – both combined.    
- Timestamp – a specific point in time, independent of the local time zone.    
- Duration – an amount of elapsed time.    
- Period – a calendar-based amount of time, e.g. 2 months.    

Let's go through them.
# 1. LocalDate – working with dates
`LocalDate` represents a calendar date without a time or time zone.
```java
import java.time.LocalDate;

LocalDate today = LocalDate.now();

LocalDate specificDate = LocalDate.of(2026, 11, 7);

System.out.println(today);
System.out.println(specificDate);
```

Output:
```
2026-11-07
2026-11-07
```

You can access individual components:
```java
int year = today.getYear();
int month = today.getMonthValue();
int day = today.getDayOfMonth();
```

You can also perform operations:
```java
LocalDate tomorrow = today.plusDays(1);
LocalDate yesterday = today.minusDays(1);

LocalDate nextMonth = today.plusMonths(1);
LocalDate nextYear = today.plusYears(1);
```

Notice that `LocalDate` is immutable. Methods like `plusDays()` don't modify the original object. They return a new one.
# 2. LocalTime – working with time
`LocalTime` represents a time of day without a date or time zone.
```java
import java.time.LocalTime;

LocalTime now = LocalTime.now();

LocalTime specificTime = LocalTime.of(14, 30, 45);

System.out.println(now);
System.out.println(specificTime);
```

You can access individual components:
```java
int hour = now.getHour();
int minute = now.getMinute();
int second = now.getSecond();
int nano = now.getNano();
```

And perform operations:
```java
LocalTime later = now.plusHours(2);
LocalTime earlier = now.minusMinutes(30);
```
# 3. LocalDateTime – date and time together
`LocalDateTime` combines `LocalDate` and `LocalTime`.
```java
import java.time.LocalDateTime;

LocalDateTime now = LocalDateTime.now();

LocalDateTime specificDateTime =
    LocalDateTime.of(2026, 11, 7, 14, 30);

System.out.println(now);
System.out.println(specificDateTime);
```

You can also combine existing date and time objects:
```java
LocalDate date = LocalDate.of(2026, 11, 7);
LocalTime time = LocalTime.of(14, 30);

LocalDateTime dateTime = LocalDateTime.of(date, time);
```

Important: `LocalDateTime` does not contain time zone information. For example, `2026-11-07 14:30` doesn't tell you whether that means 14:30 in Poland, Japan, or somewhere else.

This distinction becomes important when developing backend applications.
# 4. ZonedDateTime – working with time zones
`ZonedDateTime` represents a date and time in a particular time zone.
```java
import java.time.ZonedDateTime;
import java.time.ZoneId;

ZonedDateTime now = ZonedDateTime.now();

ZonedDateTime polandTime =
    ZonedDateTime.now(ZoneId.of("Europe/Warsaw"));

ZonedDateTime tokyoTime =
    ZonedDateTime.now(ZoneId.of("Asia/Tokyo"));
```

You can convert between time zones:
```java
ZonedDateTime tokyo =
    polandTime.withZoneSameInstant(ZoneId.of("Asia/Tokyo"));
```

Notice `withZoneSameInstant()`.

It preserves the actual moment in time but changes the displayed local date and time.
# 5. Instant – representing an exact moment in time
`Instant` represents a specific point on the global timeline.

It is generally represented as the number of seconds and nanoseconds since the Unix epoch (January 1, 1970, UTC).
```java
import java.time.Instant;

Instant now = Instant.now();

System.out.println(now);
```

Example output:
```
2026-11-07T10:00:00Z
```

The `Z` means UTC.

You can also create an instant from Unix timestamps:
```java
Instant instant = Instant.ofEpochSecond(1794045600);
```

Or get the Unix timestamp:
```java
long timestamp = Instant.now().getEpochSecond();

long milliseconds = Instant.now().toEpochMilli();
```

When would you use it?

For example, when storing:
- When a user registered.    
- When an order was created.    
- When a transaction happened.    
- When a background job was executed.    

For backend applications, `Instant` is often a good choice for storing event timestamps because it represents an unambiguous moment in time.
# 6. Duration and Period – measuring time
These two classes represent different concepts.

Duration represents elapsed time, typically measured in seconds and nanoseconds.
```java
import java.time.Duration;
import java.time.LocalTime;

LocalTime start = LocalTime.of(10, 0);
LocalTime end = LocalTime.of(12, 30);

Duration duration = Duration.between(start, end);

System.out.println(duration.toHours());   // 2
System.out.println(duration.toMinutes()); // 150
```

You can also create durations directly:
```java
Duration duration = Duration.ofMinutes(90);
```

Period represents a calendar-based amount of time, measured in years, months, and days.
```java
import java.time.Period;
import java.time.LocalDate;

LocalDate start = LocalDate.of(2026, 1, 1);
LocalDate end = LocalDate.of(2026, 3, 15);

Period period = Period.between(start, end);

System.out.println(period.getMonths()); // 2
System.out.println(period.getDays());   // 14
```

Why are these different?

Adding one month to January 31 is not equivalent to adding 30 days. Calendar months have different lengths.

Use:
- `Duration` for elapsed time.    
- `Period` for calendar-based differences.    
# 7. Comparing dates and times
You can compare date/time objects using methods such as `isBefore()`, `isAfter()`, and `isEqual()`.
```java
LocalDate date1 = LocalDate.of(2026, 11, 7);
LocalDate date2 = LocalDate.of(2026, 11, 10);

System.out.println(date1.isBefore(date2)); // true
System.out.println(date1.isAfter(date2));  // false
System.out.println(date1.isEqual(date2));  // false
```

You can also use `compareTo()`:
```java
int result = date1.compareTo(date2);
```

It returns:
- Negative number if `date1` is earlier.    
- Zero if they are equal.    
- Positive number if `date1` is later.    
# 8. Formatting dates and times
You can format date/time objects using `DateTimeFormatter`.
```java
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

LocalDateTime now = LocalDateTime.now();

DateTimeFormatter formatter =
    DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm:ss");

String formatted = now.format(formatter);

System.out.println(formatted);
```

Example output:
```
07-11-2026 14:30:45
```

Some useful formatting patterns:

|Pattern|Meaning|Example|
|---|---|---|
|`yyyy`|Year|2026|
|`MM`|Month|11|
|`dd`|Day|07|
|`HH`|Hour (24h)|14|
|`hh`|Hour (12h)|02|
|`mm`|Minutes|30|
|`ss`|Seconds|45|
|`E`|Day of week|Sat|
|`MMMM`|Full month name|November|

You can also parse a string into a date:
```java
String input = "07-11-2026";

DateTimeFormatter formatter =
    DateTimeFormatter.ofPattern("dd-MM-yyyy");

LocalDate date = LocalDate.parse(input, formatter);
```

This is useful when receiving date values from HTTP requests or reading files.
# 9. Summary – which class should you use?
This is probably the most important part to remember.

|Class|Represents|Example|
|---|---|---|
|`LocalDate`|Calendar date|2026-11-07|
|`LocalTime`|Time of day|14:30|
|`LocalDateTime`|Date and time without zone|2026-11-07T14:30|
|`ZonedDateTime`|Date and time with time zone|2026-11-07T14:30+01:00[Europe/Warsaw]|
|`Instant`|Exact moment in UTC|2026-11-07T13:30:00Z|
|`Duration`|Elapsed time|90 minutes|
|`Period`|Calendar-based period|2 months, 5 days|
