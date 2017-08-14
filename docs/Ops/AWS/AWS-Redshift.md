Check the [postgresql wiki page](../dev/DB/Postgres) out:

[List databases] (https://gist.github.com/patsancu/50ea9416c0c7ba5746d045e9b047955d)
### Load data into redsfhit from s3
Data can be loaded recursively.
If there's a folder with this structure
```
a/
  b/
    p.json.gz
  c/
    q.json.gz
    r.json.gz
```
Calling the copy sentence with the folder **a** as source will copy all files under the folder recursively
```sql
copy schema.table_name
from 's3://bucket-name/some_folder/some_file.json.gz'
-- from 's3://bucket-name/a'
with credentials 'aws_access_key_id=some_access_key;ws_secret_access_key=supersupersecretkey'
[gzip]
format as json 'auto'
[region 'us-east-1']
-- If the Amazon S3 buckets that hold the data files do not reside in the same region as your cluster, you must use the REGION parameter to specify the region in which the data is located.
```

#### Escape strings with Escape
**Remove** the format as csv thing
```
copy analyticsmodel.playback
from :sql:source
with credentials :sql:redshift-credentials
delimiter '~'
ignoreheader as 1
[escape]
[truncatecolumns Truncates data in columns to the appropriate number of characters it has been specified]
```


### Load into redshift with custom field ordering
You can specify a comma-separated list of column names to load source data fields into specific target columns.
[Docs](http://docs.aws.amazon.com/redshift/latest/dg/copy-parameters-column-mapping.html)
```sql
copy schema.table (column_a, column_b, column_c, column_d, column_e, colummn_f)
from 's3://some_file.csv'
with credentials 'aws_access_key_id=some_access_key;ws_secret_access_key=supersupersecretkey'
format as csv
ignoreheader as 1
TRUNCATECOLUMNS
```

### Check errors
```sql
select * from stl_load_errors
order by starttime desc;
```
### Check info about permanent tables
The STV_TBL_PERM table contains information about the permanent tables in Amazon Redshift. More info [here](http://docs.aws.amazon.com/redshift/latest/dg/r_STV_TBL_PERM.html)
```sql
select * FROM stv_tbl_perm ;
```



### Size info about tables
#### First method
```sql
select "database",
"schema" || '.' || "table", "size" as "size in Mb", "tbl_rows" as "rows"
from svv_table_info
```

#### Second method
The query below's info  is **not exhaustive nor complete**
```sql
SELECT TRIM(pgdb.datname) AS DATABASE,
      TRIM(pgn.nspname) AS SCHEMA,
      TRIM(a.name) AS TABLE,
      b.mbytes,
      a.rows
FROM (SELECT db_id,
            id,
            name,
            SUM(ROWS) AS ROWS
     FROM stv_tbl_perm a
     GROUP BY db_id,
              id,
              name) AS a
 JOIN pg_class AS pgc ON pgc.oid = a.id
 JOIN pg_namespace AS pgn ON pgn.oid = pgc.relnamespace
 JOIN pg_database AS pgdb ON pgdb.oid = a.db_id
 JOIN (SELECT tbl, COUNT(*) AS mbytes FROM stv_blocklist GROUP BY tbl) b ON a.id = b.tbl
ORDER BY a.db_id,
        a.name;
```

### Generate date series
```sql
WITH date_series_bounds AS (
	SELECT date('2012-12-21') as start, date('2013-08-23') as end
), date_series AS (
	select date(days.start + days.interval)
	from (
		select bounds.start, generate_series(0, bounds.end - bounds.start) AS interval from date_series_bounds bounds
	) as days
)
select * from date_series
```

or
```sql
select current_date - (n*30 || ' minutes')::interval
from generate_series (0, 100*5-1) n
```

or
```sql
select substr(to_date('2017-06-22', 'YYYY-MM-DD') + (n || ' days')::interval, 1,10)
from generate_series (0, 6) n
```

### List schemas
```sql
select *
from information_schema.schemata
```

### Create schema
```CREATE SCHEMA IF NOT EXISTS schema_name```

### [Check data load](http://docs.aws.amazon.com/redshift/latest/dg/r_STL_FILE_SCAN.html)
```sql
select * from STL_FILE_SCAN
where name like '%screentime%'
order by curtime desc
```
