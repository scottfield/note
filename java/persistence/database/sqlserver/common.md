###add identity to existing primary key
```
--create test table
drop table test;
CREATE TABLE overwatchdb.dbo.test (
	id int primary key   NOT NULL,
	test varchar(100) NULL
);

--add test data
INSERT into test(id,test) values(3,'xx'),(5,'zzz');
select * from test;

--delete existing primary key constraint
ALTER TABLE test drop constraint PK__test__3213E83FA31A8181;

--add the new primary key with expected identity definition
ALTER TABLE test add another_id int IDENTITY not null primary key;

--delete the old primary key column
alter table test drop column id;

--rename the new primary key column to old column name
EXEC overwatchdb.sys.sp_rename 'overwatchdb.dbo.test.another_id' , 'id', 'COLUMN';
select * from test;
```

###how to logging sqlserver jdbc driver
sqlserver driver use java.util.logging, so we need to configure a logging.properties to fine control
logging level.

- copy the logging.properties file to your application's resource folder
- start java application with below VM parameter to where the logging.properties.
  ```
  -Djava.util.logging.config.file=the_absolute_path_to_logging.properties
  ```
adjust related logger's level to control the output
logger categories:https://learn.microsoft.com/en-us/sql/connect/jdbc/tracing-driver-operation?view=sql-server-ver16

###Index Design

####Clustered index(B+ Tree)
####Non-clustered index(B+ Tree)
    - The data rows of the underlying table are not sorted and stored in order based on their nonclustered keys.
    - The leaf level of a nonclustered index is made up of index pages instead of data pages. The index pages on the leaf level of a nonclustered index contain key columns and included columns.
    - At least one key column must be defined. The maximum number of nonkey columns is 1023 columns. This is the maximum number of table columns minus 1.
    - Index key columns, excluding nonkeys, must follow the existing index size restrictions of 16 key columns maximum, and a total index key size of 900 bytes
    - The total size of all nonkey columns is limited only by the size of the columns specified in the INCLUDE clause; for example, varchar(max) columns are limited to 2 GB.
    
####Unique index(B+ Tree)
####Filtered index(B+ Tree)
####Columnstore indexes
####Hash index
####Memory-Optimized non-clustered index(Bw-tree)
