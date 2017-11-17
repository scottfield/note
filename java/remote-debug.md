##remote debug java application
start java with following parameter:
```
-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005
For JDK 1.4.x
-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005
For JDK 1.3.x or ealier
-Xnoagent -Djava.compiler=NONE -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005
```
example:
```
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 HelloWorld
```
