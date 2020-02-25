###use fiddler to analyze java application network
```
start up java application with the following jvm options:
-Dhttp.proxyHost=localhost
-Dhttp.proxyPort=8888
then open fiddler you could see all network traffic of this application.
```