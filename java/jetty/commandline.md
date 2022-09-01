##this note base on jetty 9.4.11.v20180605

###start up sample jetty server
```
cd $JETTY_HOME/demo-base/
java -jar $JETTY_HOME/start.jar
```

###list modlue
``` 
java -jar $JETTY_HOME/start.jar --list-modules
```
###list configuration
```
java -jar $JETTY_HOME/start.jar --list-config
```

###create a new jetty base
```
mkdir testbase
cd testbase
java -jar $JETTY_HOME/start.jar --create-startd
java -jar $JETTY_HOME/start.jar --add-to-start=http,deploy
cp $JETTY_HOME/demo-base/webapps/async-rest.war ./webapps/
java -jar $JETTY_HOME/start.jar
```
###enable modules
```
java -jar $JETTY_HOME/start.jar --add-to-start=http,webapp,deploy
```
###change jetty port through commandline
```
java -jar $JETTY_HOME/start.jar jetty.http.port=80
java -jar $JETTY_HOME/start.jar jetty.ssl.port=443
```
###change jetty http port through {jetty.base}/start.d/http.ini
```
## Connector port to listen on
jetty.http.port=80
```
###change jetty https port through {jetty.base}/start.d/https.ini
```
## Connector port to listen on
jetty.ssl.port=443
```
###enable https support
```
java -jar $JETTY_HOME/start.jar --add-to-start=https,http2
```
###enable remote debug
```
java -Xdebug -agentlib:jdwp=transport=dt_socket,address=5005,server=y,suspend=n -jar $JETTY_HOME/start.jar
```
