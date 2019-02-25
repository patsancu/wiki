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

### List sesssions per pid, machine, username, etc
```
select
       substr(a.spid,1,9) pid,
       substr(b.sid,1,5) sid,
       substr(b.serial#,1,5) ser#,
       substr(b.machine,1,6) box,
       substr(b.username,1,10) username,
       substr(b.osuser,1,8) os_user,
       substr(b.program,1,30) program
from v$session b, v$process a
WHERE b.paddr = a.addr
and type='USER'
order by spid; 
```

### Delete all tables

Proceed with caution

```
BEGIN
   FOR cur_rec IN (SELECT object_name, object_type
                     FROM user_objects
                    WHERE object_type IN
                             ('TABLE',
                              'VIEW',
                              'PACKAGE',
                              'PROCEDURE',
                              'FUNCTION',
                              'SEQUENCE'
                             ))
   LOOP
      BEGIN
         IF cur_rec.object_type = 'TABLE'
         THEN
            EXECUTE IMMEDIATE    'DROP '
                              || cur_rec.object_type
                              || ' "'
                              || cur_rec.object_name
                              || '" CASCADE CONSTRAINTS';
         ELSE
            EXECUTE IMMEDIATE    'DROP '
                              || cur_rec.object_type
                              || ' "'
                              || cur_rec.object_name
                              || '"';
         END IF;
      EXCEPTION
         WHEN OTHERS
         THEN
            DBMS_OUTPUT.put_line (   'FAILED: DROP '
                                  || cur_rec.object_type
                                  || ' "'
                                  || cur_rec.object_name
                                  || '"'
                                 );
      END;
   END LOOP;
   BEGIN
      EXECUTE IMMEDIATE 'DROP  MATERIALIZED VIEW CONT_CORE_PACKAGE_VIEW';
      EXCEPTION
        WHEN OTHERS THEN NULL;
  END;
END;
```


### Find table with column name.sql
```sql
select 
  * 
from 
  dba_tab_columns 
where 
  column_name LIKE '%POI%'
  AND owner != 'SYS' 
  AND owner != 'XDB'
  AND owner != 'APEX_040000'
  AND owner != 'MSSQL_ORACLE';
```
