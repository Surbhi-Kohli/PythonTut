# How to work with dates, times , timedeltas and Timezones:
Important module for all these tasks is datetime module.

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
Timedelta with datetime:

```
tdelta= datetime.timedelta(days=7)
dt= datetime.datetime(2016,7,26,12,30,45,10000)
print(dt) # 2016-07-26 12:30:45.010000
print(dt+tdelta) # 2016-08-02 12:30:45.010000

hdelta = datetime.timedelta(hours=12)
print(dt+hdelta) #2016-07-27 00:30:45.010000
```
