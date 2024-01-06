
###show database version information
```
SHOW VARIABLES LIKE '%version%'
```
###show table structure
```
mysql> EXPLAIN  tableName;
mysql> DESC tableName;
```
###show create table sql
```
mysql> SHOW CREATE TABLE tableName;
```
###display query result vertically
```
select * from table_name \G
```
###check mysql server supported storage engines
```
SHOW ENGINES;
```
###check table's storage engine information
```
SHOW TABLE STATUS LIKE 'user'\G
```
### temporarily disable foreign key constrains check
```
SET FOREIGN_KEY_CHECKS=0
SHOW GLOBAL variables like 'FOREIGN_KEY_CHECKS' ;
after operation don't forget to enable it:
SET FOREIGN_KEY_CHECKS=1
SHOW GLOBAL variables like 'FOREIGN_KEY_CHECKS' ;
```
### check table size
```
select table_schema "DB name (table_schema)", 
sum((data_length+index_length)/1024/1024) AS "DB size in MB" from 
information_schema.tables group by table_schema
```