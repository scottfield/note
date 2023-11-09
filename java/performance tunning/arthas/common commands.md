###start arthas
```
java -jar arthas-boot.jar
```

###trace method by cost
```
#the cost time unit is milliseconds
trace full_class_name method_name '#cost > 5000'
```
###update logger level
```
logger logger_name DEBUG
```
###generate jfr profile
```
jfr start

jfr dump -r 1
```

###use jstack to verify if attach VM works as expected
```
jstack -l 16147
```

###OGNL
```
call static method
ognl '@java.lang.System@out.println("hello world")'

get static field
ognl -c  18b4aac2 @com.walmart.ct.srt.overwatch.storeservice.App@LOGGER

search classloader of a specific class
sc com.walmart.ct.srt.overwatch.storeservice.App  -d

dynamic change logger's log level
ognl '@org.slf4j.LoggerFactory@getLogger("root").setLevel(@ch.qos.logback.classic.Level@INFO)'

check all classes loaded by a specific classloader
classloader -c 62fe6067 -a

check urls usage stats of classloaders
classloader --url-stat
```
