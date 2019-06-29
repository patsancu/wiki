### Date/Time conversions

```python
import datetime
import time

# Create date from epoch
date = datetime.datetime.utcfromtimestamp(1489968401)

# Create date from year, month, day
date = datetime.datetime(2017, 8, 20)

# Get seconds from epoch
time.time()

# Test things
datetime.datetime.utcfromtimestamp(int(time.time()))

# Get tuple of year, month, ...
## Check the structure help(datetime.datetime.timetuple)
date.timetuple()

# Convert from tuple to epoch
time.mktime(p.timetuple())
```

### Date/time arithmetic
```python
import datetime
import time

date = datetime.datetime(2017, 8, 20)
# datetime.datetime(2017, 8, 20, 0, 0)
diff_8_days = datetime.timedelta(days = 8)
diff_3_minutes = datetime.timedelta(minutes = 3)

date_plus_8_days = date + diff_8_days
# datetime.datetime(2017, 8, 28, 0, 0)
date_minus_3_minutes = date - diff_3_minutes
# datetime.datetime(2017, 8, 19, 23, 57)
```

### Difference between dates
From [here](https://gist.github.com/amalgjose/c767a4846d6ecaa3b6d7)

```python
from datetime import datetime
from dateutil import relativedelta

##Aug 7 1989 8:10 pm
date_1 = datetime(1989, 8, 7, 20, 10)

##Dec 5 1990 5:20 am
date_2 = datetime(1990, 12, 5, 5, 20)

#This will find the difference between the two dates
difference = relativedelta.relativedelta(date_2, date_1)

years = difference.years
months = difference.months
days = difference.days
hours = difference.hours
minutes = difference.minutes

print "Difference is %s year, %s months, %s days, %s hours, %s minutes " %(years, months, days, hours, minutes)
```

### Get date time for different timezones
```
import datetime

import pytz
"""
    timezone must be one of the format "Europe/Berlin"
    returns string according to format (e.g. "%Y-%m-%dT%H:%M:%S%z")
"""
def get_now_for_timezone(timezone):
    utcmoment_naive = datetime.datetime.utcnow()
    utcmoment = utcmoment_naive.replace(tzinfo=pytz.utc)
    localDatetime = utcmoment.astimezone(pytz.timezone(timezone))
    return localDatetime

def get_now_for_timezone_plus_minutes(timezone, minutes):
    now = get_now_for_timezone(timezone)
    return add_minutes(now, minutes)

def get_string_now_for_timezone_and_dateformat_string(timezone, dateformat):
    localDatetime = get_now_for_timezone(timezone)
    return localDatetime.strftime(dateformat)

def add_minutes(some_date, minutes_to_add):
    diff_45_minutes = datetime.timedelta(minutes = minutes_to_add)
    return some_date + diff_45_minutes

def get_string_now_plus_minutes_for_timezone_and_dateformat(minutes, timezone, dateformat):
    plus_minutes = get_now_for_timezone_plus_minutes(timezone, minutes)
    return plus_minutes.strftime(dateformat)

date_format = "%Y-%m-%dT%H:%M:%S%z"
print(get_now_for_timezone("UTC"))
# 2019-06-28 09:53:44.435425+00:00
print(get_now_for_timezone_plus_minutes("America/Los_Angeles", 20))
# 2019-06-28 03:13:44.435985-07:00
print(get_string_now_for_timezone_and_dateformat_string("UTC", date_format))
# 2019-06-28T09:53:44+0000
print(get_string_now_plus_minutes_for_timezone_and_dateformat(2, "Europe/Madrid", date_format))
# 2019-06-28T11:55:44+0200
```
