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