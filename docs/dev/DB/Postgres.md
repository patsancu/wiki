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
