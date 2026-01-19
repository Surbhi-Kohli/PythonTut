# How to work with dates, times , timedeltas and Timezones:
Important module for all these tasks is datetime module.

### There are 2 types of times: Naive and Aware times
Naive datetime: Dont have enough info to determine timezone, daylight saving time, etc.But these are easier to work with and better in case you would not need timezone etc info.

Aware datetime: Have enough info of timezone and daylight savings

## Naive datetime
### Naive dates:
#### There are a couple of ways to create a naive  date:
1.
```
import datetime
d= datetime.date(2025,5,5)
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

### Naive time:
