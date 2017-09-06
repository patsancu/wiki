### Change column type without changing order
From [here](https://stackoverflow.com/a/36718450/2769307)
```
CREATE TEMP TABLE temp_table AS SELECT * FROM original_table;
DROP TABLE original_table;
CREATE TABLE original_table ...
INSERT INTO original_table SELECT * FROM temp_table;
```

### List tables
```sql
SELECT * FROM pg_catalog.pg_tables
where tablename like '%patata%' ;
```

```sql
SELECT * FROM pg_catalog.pg_tables
where schema like '%some_model%' ;
```

### Describe table
```sql
select column_name, data_type, character_maximum_length
from INFORMATION_SCHEMA.COLUMNS where table_name = 'table_name_without_schema'
```

### Capitalize first letter of each word
```sql
select initcap(lower(deli.short_title))
from deli
```

### Select top N from groups
#### Select top 2 subcategories from each category, according to the movie screentime
```sql
with grouped_stuff as
    ( select movie.category, movie.subcategory,
    sum(movie.screentime) as total_screentime
    from movies movie
    where upload_date = '2017-09-18 00:00:00'
    group by movie.subcategory, movie.category),
ranking as
(
	select grouped_stuff.*,
	rank() over
	(
		partition by category
		order by total_screentime desc
	)
	from
	grouped_stuff
)
select * from ranking where rank < 3
```
