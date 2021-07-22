### execute class main method
'dir/*' classpath element will include all jar files under dir
but the order of jar file is unspecified
```
java -cp ./* package-name.classname args
```
use ';' semicolon to seperate jar files
```
java -cp a.jar;b.jar package-name.classname args
```
### execute jar file
the filename is the jar file which contains a manifest
contains a line in the format  Main-Class:classname
```
java -jar filename
```
###specify jvm working directory
```
-Duser.dir=your_directory

```
###get current jvm working directory
```
System.getProperty("user.dir")

```
### get running jvm's environment information
```
step 1. get java process's id
jps -lv
or 
ps aux

step 2. use jinfo to get environment information
jinfo <pid>
```
###get linux process environment information:
```
step 1. get PID
ps aux|grep 'your_process_name'

step 2. get process environment information
cat /proc/<PID>/environ
```
###get java threads 
```
 ps -efL|grep java
```

###monitor java threads cpu consuming
```
 top -H -p process_id         
```

###find TCP connections opened by a java process
```
sudo lsof -nPiTCP -p 4693 -a
```

oracle java tool document link
https://docs.oracle.com/javase/10/tools/java.htm#JSWOR624

oracle document for classpath
https://docs.oracle.com/javase/6/docs/technotes/tools/windows/classpath.html 