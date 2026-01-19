# How to work with dates, times , timedeltas and Timezones:
Important module for all these tasks is datetime module.

### There are 2 types of times: Naive and Aware times
Naive datetime: Dont have enough info to determine timezone, daylight saving time, etc.But these are easier to work with and better in case you would not need timezone etc info.

Aware datetime: Have enough info of timezone and daylight savings

## Naive datetime
### There are a couple of ways to create a naive  date:
```
import datetime
d= datetime.date(2025,5,5)
print(d) # 2025-05-05

# Dont do  d= datetime.date(2025,05,05)
# SyntaxError: leading zeros in decimal integer literals are not permitted; use an 0o prefix for octal integers
```
