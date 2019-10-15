### Selective count
```sql
SELECT count(
	CASE
		WHEN content.parental_rating IS NULL THEN 1
	end
)/count(*)*100
FROM CONT_AV_CONTENT content
```

### Rank rows relative to some column
A content has multiple genres. This will rank genres of each content (categorised according to their title).
```sql
SELECT content.content_id,
       content.title,
       genre.NAME,
       Row_number() OVER ( partition BY content.title ORDER BY genre.genre_id DESC) AS ranking
FROM   cont_av_content CONTENT
       JOIN cont_content_genre_map cmap
         ON content.content_id = cmap.content_id
       JOIN cont_genre genre
         ON genre.genre_id = cmap.genre_id
```

### From string to timestamp
```
TO_TIMESTAMP('2016-05-14', 'YYYY-MM-DD')
```

### Calculate table size
[source](https://stackoverflow.com/a/10109416)
```sql
-- Tables + Size MB
select owner, table_name, round((num_rows*avg_row_len)/(1024*1024)) MB
from all_tables
where owner not like 'SYS%'  -- Exclude system tables.
and num_rows > 0  -- Ignore empty Tables.
order by MB desc -- Biggest first.;
--Tables + Rows
select owner, table_name, num_rows
 from all_tables
where owner not like 'SYS%'  -- Exclude system tables.
and num_rows > 0  -- Ignore empty Tables.
order by num_rows desc -- Biggest first.;
```

### Group by truncated date
```
select TRUNC(created), count(*)
from PURCHASES
where created >=  TO_TIMESTAMP ( '01-OCT-2017 00:00:00', 'DD-MON-YYYY HH24:MI:SS')
group by TRUNC(created)
```

### Look for table by name
```sql
SELECT owner, table_name
  FROM dba_tables
  where owner = 'da_owner'
```


### Round timestamp/datetime to next 5 minutes
```sql
with table_x as (
 select timestamp '2010-02-19 01:25:46' t from dual union all
 select timestamp '2010-02-19 01:40:46' from dual union all
 select timestamp '2010-02-19 01:55:46' from dual union ALL
 select timestamp '2010-02-19 01:19:46' from dual union ALL
 select timestamp '2010-02-19 01:00:00' from dual union ALL
 select timestamp '2010-02-19 01:00:01' from dual union ALL
 select timestamp '2010-02-19 23:58:01' from dual union all
 select timestamp '2010-02-19 02:10:46' from dual)
select t AS input_time,
case when mod(60*extract(minute from t)+extract(second from t),60*5) > 0
     then t+NumToDsInterVal(60*5-mod(60*extract(minute from t)+extract(second from t),60*5),'SECOND')
     else t end as rounded_time
  from table_x;
  
  
WITH time_table AS (
	SELECT CAST(TO_DATE('2016-03-18 08:54:00', 'YYYY-MM-DD HH24:MI:SS') AS timestamp) t FROM dual UNION ALL
	SELECT CAST(TO_DATE('2016-03-20 23:59:00', 'YYYY-MM-DD HH24:MI:SS') AS timestamp) t FROM dual UNION ALL
	SELECT CAST(TO_DATE('2016-03-20 00:05:00', 'YYYY-MM-DD HH24:MI:SS') AS timestamp) t FROM dual UNION ALL
	SELECT CAST(TO_DATE('2016-03-20 00:05:01', 'YYYY-MM-DD HH24:MI:SS') AS timestamp) t FROM dual UNION ALL
	SELECT CAST(TO_DATE('2016-03-31 23:59:00', 'YYYY-MM-DD HH24:MI:SS') AS timestamp) t FROM dual
)
SELECT 
	t AS input_time,
	case when mod(60*extract(minute from t)+extract(second from t),60*5) > 0
     then t+NumToDsInterVal(60*5-mod(60*extract(minute from t)+extract(second from t),60*5),'SECOND')
     else t end as rounded_time_TO
FROM time_table
```

### Split string and pick last
```sql
WITH some_table AS (
	SELECT 'SOME_CITY_NAME_1' city_name FROM dual UNION ALL
	SELECT 'BERLIN_24' FROM dual UNION ALL
	SELECT 'MADRID_3' FROM dual UNION ALL
	SELECT 'SOME_OTHER_CITY_NAME_2' FROM dual
)
SELECT city_name, SUBSTR( city_name,
               INSTR( city_name, '_', -1 )+1 ) FROM some_table

-- RESULTS
-- CITY_NAME	SUBSTR(CITY_NAME,INSTR(CITY_NAME,'_',-1)+1)
-- ========================================
-- SOME_CITY_NAME_1 || 1
-- BERLIN_24 || 24
-- MADRID_3 || 3
-- SOME_OTHER_CITY_NAME_2 || 2
```
### Split string and pick all but last
```sql
WITH some_table AS (
	SELECT 'SOME_CITY_NAME_1' city_name FROM dual UNION ALL
	SELECT 'BERLIN_24' FROM dual UNION ALL
	SELECT 'MADRID_3' FROM dual UNION ALL
	SELECT 'SOME_OTHER_CITY_NAME_2' FROM dual
)
SELECT city_name, SUBSTR( city_name,
               0, INSTR( city_name, '_', -1 )-1 ) FROM some_table

-- RESULTS
-- CITY_NAME;SUBSTR(CITY_NAME,0,INSTR(CITY_NAME,'_',-1)-1)
-- ========================================
-- SOME_CITY_NAME_1;SOME_CITY_NAME
-- BERLIN_24;BERLIN
-- MADRID_3;MADRID
-- SOME_OTHER_CITY_NAME_2;SOME_OTHER_CITY_NAME
```

### Compare dates with and without timezone

```sql
-- trans_time is with time zone and SUBSCRIPTION.VALID_FROM is in UTC but with no explicit timezone
SELECT
    *
FROM
    a
JOIN
    subscription ON a.customer_id = subscription.customer_id
WHERE
    a.TRANS_TIME >=	FROM_TZ( CAST(SUBSCRIPTION.VALID_FROM AS TIMESTAMP), 'UTC' )
```
