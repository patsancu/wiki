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
