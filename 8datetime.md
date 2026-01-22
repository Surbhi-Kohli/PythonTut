# How to work with dates, times , timedeltas and Timezones:
Important module for all these tasks is datetime module.

## What is UTC
UTC stands for Coordinated Universal Time. 🌎🕒

It’s the world standard time that all other timezones are based on. Think of it as the “baseline” clock for the planet.

Key points about UTC:
1. Universal reference
  * UTC is the same everywhere.
  * When it’s 12:00 UTC, it’s 12:00 everywhere in UTC, but local clocks show different times depending on the timezone.
2. Not a timezone per se
  * It doesn’t change with daylight saving.
  * It’s always consistent: UTC+0.
3. Used for coordination
  *Internet servers, flight schedules, banking transactions, programming logs all use UTC to avoid confusion.
  * Example: A server in Singapore (UTC+8) and a server in New York (UTC-5) can both log an event as 2026-01-21 08:00 UTC → easy to compare.
4. Relation to local time
   * Local time = UTC +(-) offset
   * Singapore: UTC+8 → if UTC is 10:00, local time is 18:00
   * New York: UTC-5 → if UTC is 10:00, local time is 05:00  

Quick analogy:

Think of UTC as Greenwich Mean Time (GMT)—the “mother clock” of the world.
Local timezones are just UTC plus/minus a few hours.

### There are 2 types of times: Naive and Aware times
Naive datetime: Dont have enough info to determine timezone, daylight saving time, etc.But these are easier to work with and better in case you would not need timezone etc info.

Aware datetime: Have enough info of timezone and daylight savings

## Naive datetime
### Naive dates:(Work with years, months and days)
#### There are a couple of ways to create a naive  date:
1.
```
import datetime
d= datetime.date(2025,5,5) # Gives year, month ,day without hrs, mins, sec ,ms
print(d) # 2025-05-05

# Dont do  d= datetime.date(2025,05,05)
# SyntaxError: leading zeros in decimal integer literals are not permitted; use an 0o prefix for octal integers
```
2.To get today date
```
today  = datetime.date.today()
print(today) # 2026-01-19
print(today.year)  # 2026
print(today.day) #19
print(today.weekday()) # 0
print(today.isoweekday()) # 1

```
for weekday(), Monday is 0 and Sunday is 6,
For isoweekday(), Monday is 1 and Sunday is 7

#### Time deltas in naive datetime

1. Subtracting/adding delta from/to a date eg date+delta or date-delta
```
 today  = datetime.date.today()
 print(today)
 tdelta= datetime.timedelta(days=7)
 print(today+tdelta) # 2026-01-26
 print(today-tdelta) # 2026-01-12
```
2. Diffing dates gives timedelta : date1-date2

```
today  = datetime.date.today()
print(today) # 2026-01-19
bday=datetime.date(2026,10,25) # 2026-10-25
tillbday = bday-today
print(tillbday) # 279 days, 0:00:00
print(tillbday.days) # 279
print(tillbday.total_seconds()) # 24105600.0
```

### Naive time: Work with hours , mins , seconds and microseconds without year, month,day

```
t=datetime.time()
print(t) # 00:00:00
t1 = datetime.time(9,30,45,10000)
print(t1) # 09:30:45.010000
print(t1.hour) # 9
```
We hardly ever use datetime.time standalone because when i need time of a day , i also need the date and thats where datetime.datetime is used for.

### Naive datetime : gives hrs, mins, seconds, ms, year, month, day
```
dt= datetime.datetime(2016,7,26,12,30,45,10000)
print(dt) # 2016-07-26 12:30:45.010000
print(dt.date()) # 2016-07-26
print(dt.time()) # 12:30:45.010000
print(dt.year) # 2016
```
##### Timedelta with datetime:

```
tdelta= datetime.timedelta(days=7)
dt= datetime.datetime(2016,7,26,12,30,45,10000)
print(dt) # 2016-07-26 12:30:45.010000
print(dt+tdelta) # 2016-08-02 12:30:45.010000

hdelta = datetime.timedelta(hours=12)
print(dt+hdelta) #2016-07-27 00:30:45.010000
```
#### datetime.now() vs datetime.utcnow()


datetime.now() and datetime.utcnow() return different clock times
Both return “naive” datetimes → tzinfo is None
“UTC” here means the value, not that it’s timezone-aware

1️⃣ datetime.datetime.now()

```dt_now = datetime.datetime.now()```
* Returns current local time (based on your system clock)
* Timezone is assumed, not attached
* Result is naive

Example (if your system is in Singapore):
```
2026-01-21 14:30:00
tzinfo = None

```
Python does not store “Asia/Singapore” anywhere here.
2️⃣ datetime.datetime.utcnow()
dt_utcnow = datetime.datetime.utcnow()

* Returns current UTC time(which does not specify the timezone that it is UTC)
* BUT still returns a naive datetime
* tzinfo is None

```
 import datetime
 dt_today = datetime.datetime.today()

 dt_now= datetime.datetime.now() # lets u pass a timezone, here we did not pass 
 dt_utcnow= datetime.datetime.utcnow() # this gives us current utc time but  here also tzinfo is None
# <stdin>:1: DeprecationWarning: datetime.datetime.utcnow() is deprecated and scheduled for removal in a future version. Use timezone-aware objects to represent datetimes in UTC: datetime.datetime.now(datetime.UTC).
 print(dt_today) # 2026-01-21 20:53:58.924482 - gives current local datetime with timezone of none
 print(dt_now) # 2026-01-21 20:53:52.314170
 print(dt_utcnow) # 2026-01-21 15:24:50.128305

```
Why does utcnow() still have tzinfo=None?

Because of historical Python design.

Originally:
Python treated timezones as external knowledge.Functions returned raw timestamps, not metadata

So:utcnow() means “this value represents UTC”,not “this object is timezone-aware”.

This is why Python docs now say:

❗ datetime.utcnow() is deprecated for new code
The correct way (modern Python)
✅ Use timezone-aware datetimes
```
from datetime import datetime, timezone

dt_utc = datetime.now(timezone.utc)
```

Now:

2026-01-21 06:30:00+00:00
tzinfo = UTC
This is aware and safe.
### Mental Model:
| Function            | Time value | tzinfo  |
| ------------------- | ---------- | ------- |
| `now()`             | Local      | ❌ None  |
| `utcnow()`          | UTC        | ❌ None  |
| `now(timezone.utc)` | UTC        | ✅ Aware |

For timezone aware work we will use pytz instead of datetimes original timezone as pytz is easier to use and also recommended in python docs.
But Why??
#### 1️⃣ The problem with Python’s built-in timezones

Python’s standard library (datetime.timezone) can only represent fixed offsets like:
```
from datetime import timezone, timedelta
UTC_plus_5 = timezone(timedelta(hours=5))
```

✅ Works for simple offsets

❌ Cannot handle daylight saving time (DST) or historical changes
For example, Mountain Time in the US:
Winter: UTC-7
Summer: UTC-6 (DST)

If you try to use datetime.timezone, you have to manually adjust offsets for DST—painful and error-prone.
#### 2️⃣ Why pytz is better

pytz comes with the full IANA timezone database (the same one used by your OS and Linux servers).

This means:
It knows about DST rules automatically
It knows historical changes, like if a country changed its timezone in the past

You can just do:
```
import pytz
from datetime import datetime

dt_utc = datetime.now(pytz.UTC)
dt_mtn = dt_utc.astimezone(pytz.timezone("US/Mountain"))
print(dt_mtn)
# Automatically adjusts for DST

```
✅ No manual math for offsets
✅ Safe for real-world applications

#### 3️⃣ Python docs recommendation

Python docs themselves say:

“For accurate and cross-platform timezone calculations, use pytz or zoneinfo. Avoid using fixed-offset timezone objects for real-world timezones.”
pytz → historically recommended
Python 3.9+ → now also has zoneinfo in the standard library (similar functionality)

#### 4️⃣ Easy way to remember

* Built-in timezone of python : good for simple fixed offsets only (UTC+5)
* pytz: good for real-world zones with DST

Always use pytz (or zoneinfo) for apps, like logging, calendars, servers

The ONE thing to remember

Real places have moving clocks.
Python’s basic timezone has a fixed clock.
pytz knows when clocks move.


Golden rule (tattoo-worthy 😄)

Store time in UTC.
Convert with pytz.
Never trust fixed offsets.
