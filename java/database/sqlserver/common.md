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
