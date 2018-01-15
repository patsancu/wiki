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

