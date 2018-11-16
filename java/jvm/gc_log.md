####how to enable gc log
```
-Xloggc:gc.log
-XX:+PrintGCDetails
-XX:+PrintGCDateStamps
-XX:+PrintTenuringDistribution 
-XX:+PrintGCCause
-XX:+UseGCLogFileRotation
-XX:NumberOfGCLogFiles=10 
-XX:GCLogFileSize=5M
```