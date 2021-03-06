### How to turn off oracle password expiration
[source](https://stackoverflow.com/a/6777079)

To alter the password expiry policy for a certain user profile in Oracle first check wich profile the user is in using:
```sql
select profile from DBA_USERS where username = '<username>';
```
Then you can change the limit to never expire using:
```sql
alter profile <profile_name> limit password_life_time UNLIMITED;
```
If you want to previously check the limit you may use:

```sql
select resource_name,limit from dba_profiles where profile='<profile_name>';
```

## What do if password expired oracle

### delete user
```
drop user cms_int cascade;
```


### create user again
```
create user cms_int identified by cms_int;
grant all privileges to cms_int identified by cms_int;
```

## Import db dump

```sql
CREATE USER bakbak IDENTIFIED BY bakbak;
GRANT CREATE TRIGGER, CREATE SEQUENCE, CREATE SESSION, CREATE TABLE, CREATE VIEW, CREATE PROCEDURE, CREATE SYNONYM, CREATE TABLESPACE TO bakbak;
GRANT ALTER TABLESPACE TO bakbak;
GRANT ALTER ANY TABLE, ALTER ANY PROCEDURE TO bakbak;
GRANT DROP TABLESPACE, DROP ANY TABLE, DROP ANY VIEW, DROP ANY PROCEDURE,DROP ANY SYNONYM TO bakbak;
ALTER USER bakbak QUOTA UNLIMITED ON USERS;
GRANT UNLIMITED TABLESPACE TO bakbak;

GRANT CREATE ANY DIRECTORY TO bakbak;
GRANT DROP ANY DIRECTORY TO bakbak;

GRANT CREATE TRIGGER TO bakbak;
GRANT DROP ANY PROCEDURE TO bakbak;
GRANT ALTER ANY PROCEDURE TO bakbak;
GRANT CREATE PROCEDURE TO bakbak;
GRANT CREATE SEQUENCE TO bakbak;
GRANT DROP ANY VIEW TO bakbak;
GRANT CREATE VIEW TO bakbak;
GRANT DROP ANY SYNONYM TO bakbak;
GRANT CREATE SYNONYM TO bakbak;
GRANT DROP ANY TABLE TO bakbak;
GRANT ALTER ANY TABLE TO bakbak;
GRANT CREATE TABLE TO bakbak;
GRANT UNLIMITED TABLESPACE TO bakbak;
GRANT DROP TABLESPACE TO bakbak;
GRANT ALTER TABLESPACE TO bakbak;
GRANT CREATE TABLESPACE TO bakbak;
GRANT CREATE SESSION TO bakbak;
GRANT IMP_FULL_DATABASE TO bakbak;
GRANT EXP_FULL_DATABASE TO bakbak;
CREATE DIRECTORY mydir AS '/home/patrick/Data/dumps_db/'; GRANT read, write on directory mydir to public;
GRANT read, write ON mydir TO bakbak;
ALTER USER bakbak QUOTA UNLIMITED ON USERS;
GRANT UNLIMITED TABLESPACE TO bakbak;
commit;
```

Execute in bash
```bash
impdp bakbak/bakbak directory=mydir file=export_data.dmp remap_schema=cv_mex_mtv:bakbak "EXCLUDE=TABLE:\"IN \(\'EIT_MANIFEST\',\'WH_FACT_AUDIENCE\',\'ACT_ACTIVITY\', \'REC_RECORDING\', \'REC_RECORDING_I18N\', \'ADI_FILE_IMPORT\' \)\"" logfile=data_pump_dir:expsh.log
### Stop job impdp
Import> KILL_JOB
### Find and delete pending import jobs
```sql
SELECT owner_name, job_name, operation, job_mode,
state, attached_sessions
FROM dba_datapump_jobs
ORDER BY 1,2;
```

```sql
SELECT *
  FROM dba_objects o, dba_datapump_jobs j
 WHERE o.owner=j.owner_name AND o.object_name=j.job_name
   AND j.job_name NOT LIKE 'BIN$%' ORDER BY 4,2;

DROP TABLE BAKBAK.SYS_IMPORT_FULL_01;
```

### Delete views, tables for a user
#### Get scripts to drop tables and views
```sql
select 'drop table '||table_name||' cascade constraints;' from user_tables;
```
```sql
select 'drop view '||view_name||' cascade constraints;' from user_views;
```

### Delete sequences
```sql
BEGIN

  --Bye Sequences!
  FOR i IN (SELECT us.sequence_name
              FROM USER_SEQUENCES us) LOOP
    EXECUTE IMMEDIATE 'drop sequence '|| i.sequence_name ||'';
  END LOOP;

  --Bye Tables!
  FOR i IN (SELECT ut.table_name
              FROM USER_TABLES ut) LOOP
    EXECUTE IMMEDIATE 'drop table '|| i.table_name ||' CASCADE CONSTRAINTS ';
  END LOOP;

END;
```
