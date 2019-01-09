###check a query's profiling data
```
mysql> SET SESSION profiling = 1;#0表示关闭,1表示开启
mysql> USE profile_sampling;
mysql> SELECT * FROM users WHERE name = 'Jesse';
mysql> SHOW PROFILES;
mysql> SHOW PROFILE CPU, SWAPS, BLOCK IO, MEMORY, CONTEXT SWITCHES, IPC, PAGE FAULTS, SOURCE FOR QUERY queryId;//get query id from SHOW PROFILES
```
###show a query's explain plan
```
mysql> EXPLAIN your_query
```
###show index of table
```
mysql> SHOW INDEX FROM tbl_name
```

###use profiling schema to profile sql
#####setup:
```
mysql> UPDATE performance_schema.setup_actors
       SET ENABLED = 'NO', HISTORY = 'NO'
       WHERE HOST = '%' AND USER = '%';

mysql> INSERT INTO performance_schema.setup_actors
       (HOST,USER,ROLE,ENABLED,HISTORY)
       VALUES('localhost','test_user','%','YES','YES');

mysql> UPDATE performance_schema.setup_instruments
       SET ENABLED = 'YES', TIMED = 'YES'
       WHERE NAME LIKE '%statement/%';

mysql> UPDATE performance_schema.setup_instruments
       SET ENABLED = 'YES', TIMED = 'YES'
       WHERE NAME LIKE '%stage/%';
mysql> UPDATE performance_schema.setup_consumers
       SET ENABLED = 'YES'
       WHERE NAME LIKE '%events_statements_%';

mysql> UPDATE performance_schema.setup_consumers
       SET ENABLED = 'YES'
       WHERE NAME LIKE '%events_stages_%';

``` 
#####check query statistics:
```
mysql> SELECT EVENT_ID, TRUNCATE(TIMER_WAIT/1000000000000,6) as Duration, SQL_TEXT
       FROM performance_schema.events_statements_history_long WHERE SQL_TEXT like '%10001%';

mysql> SELECT event_name AS Stage, TRUNCATE(TIMER_WAIT/1000000000000,6) AS Duration
       FROM performance_schema.events_stages_history_long WHERE NESTING_EVENT_ID=31;
```
