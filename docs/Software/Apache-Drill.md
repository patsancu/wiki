Before googling, check errors

* https://drill.apache.org/docs/troubleshooting/
* https://drill.apache.org/docs/alter-system/

### Change store format
```sql
use dfs.tmp;
alter session set store.`format`='json';
```
After that, 

```sql
CREATE TABLE movieRegions (region, title, purchases) as  SELECT region, title, count(*) as numberOfPurchases  FROM dfs.`/home/user/data/some/path/some_file.json` group by region, title;
```
will create table on `/tmp/movieRegions/SOME_NUMBERS.json`

### query custom *sv file (fields delimited by another character)
```
select * from table(dfs.`/path/to/file/some_data.xsv` (type => 'text', fieldDelimiter => '~', extractHeader => true));
```

### Query file given absolute path
select * from dfs.`/home/patrick/dev/tvmetrix/extractor/data/liveevents/2018-01-18/liveevents_DF_2018-01-18_153010_469.json.gz` limit 20;

### Query the system
#### Identify the Foreman

Issue the following query to identify the Foreman node:

```sql
SELECT hostname FROM sys.drillbits WHERE `current` = true
```

#### Get drill version
```sql
SELECT version FROM sys.version;
```

#### Get a complete list of planning and execution options that are currently set at the system or session level

```sql
SELECT name, type FROM sys.options WHERE type in ('SYSTEM','SESSION') order by name;
```
### Change system settings
```
alter system set planner.enable_hashagg = true;
```
```
alter system set planner.enable_multiphase_agg = false;
```

### Change port of web UI
```shell
$ vim conf/drill-override.conf
```
```
drill.exec: {
  cluster-id: "drillbits1"
  rpc: {
        user: {
          server: {
            port: 31910
            }
        },
        bit: {
          server: {
            port : 31911,
            retry:{
              count: 7200,
              delay: 500
            },
            threads: 1
          }
        },
    },
    http: {
          enabled: true,
          ssl_enabled: false,
          port: 8989
          session_max_idle_secs: 3600, # Default value 1hr
          cors: {
            enabled: false,
            allowedOrigins: ["null"],
            allowedMethods: ["GET", "POST", "HEAD", "OPTIONS"],
            allowedHeaders: ["X-Requested-With", "Content-Type", "Accept", "Origin"],
            credentials: true
          }
        },
}
drill.logical.function.package+=[com.mapr.drill]

```


### Change log level
Edit `/conf/logback.xml`
