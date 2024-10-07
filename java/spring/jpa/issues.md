###spring jpa data cannot call stored procedure with multiple out parameter
https://stackoverflow.com/questions/42531970/correctly-call-a-stored-procedure-using-spring-data-jpa
https://jira.spring.io/browse/DATAJPA-707
https://jira.spring.io/browse/DATAJPA-748

## enable jpa transaction logs in log4j
```
<Logger level="trace" name="org.springframework.transaction.interceptor"/>
```

## enable jpa sql logs in log4j
```
<Logger level="trace" name="org.hibernate.sql"/>
<Logger level="trace" name="org.hibernate.type.descriptor.sql"/>
<Logger level="trace" name="org.springframework.jdbc"/>
```

