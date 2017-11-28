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
