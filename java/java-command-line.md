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