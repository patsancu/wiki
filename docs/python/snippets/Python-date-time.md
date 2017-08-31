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
