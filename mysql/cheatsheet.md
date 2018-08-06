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