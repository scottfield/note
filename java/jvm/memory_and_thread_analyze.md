###how to get the java process id
```
jps -lv
```
###get jvm heap information
```
jcmd pid_of_java_process GC.heap_info
```

###how to get a jvm heap dump(three ways could be used)
  1 
  ```
  jmap -dump:live,format=b,file=/tmp/dump.hprof 12587
  ```
  2 
  ```
  jcmd 37320 GC.heap_dump /tmp/heapdump.bin
  ```
  3 
  ```
  -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/heapdump.bin
  ```
  
###how to capturing a thread dump(2 ways could be used)

  1 
  ```
  jstack 15548 > threaddump.txt
  ```
  2 
  ```
  jcmd 15548 Thread.print > threaddump.txt
  ```