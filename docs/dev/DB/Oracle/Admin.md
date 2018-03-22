### Check number of sessions
```sql
SELECT
  'Currently, '
  || (SELECT COUNT(*) FROM V$SESSION)
  || ' out of '
  || VP.VALUE
  || ' connections are used.' AS USAGE_MESSAGE
FROM
  V$PARAMETER VP
WHERE VP.NAME = 'sessions'
```


### Change concurrency and stuff params
```
alter system set processes = 150 scope = spfile;
alter system set sessions = 300 scope = spfile;
alter system set transactions = 330 scope = spfile;
```
