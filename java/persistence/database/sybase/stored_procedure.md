###call sybase store procedure
```
declare @result INT
declare @param int
SELECT @param=110
declare @err_msg varchar(60)
EXECUTE @result=some_store_procedure @param,@err_msg OUTPUT
SELECT @result,@err_msg
```
