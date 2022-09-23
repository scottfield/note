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
