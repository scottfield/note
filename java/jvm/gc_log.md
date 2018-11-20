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
###The goals are addressed in the following order:

1.Maximum pause time goal

2.Throughput goal

3.Minimum footprint goal

###tuning gc with Maximum Garbage Collection Pause Time Goal
```
 -XX:MaxGCPauseMillis=<N>
```
###tuning gc with Throughput Goal
```
-XX:GCTimeRatio=<N>
1 / (1 + <N>)
```

###The Mostly Concurrent Collectors
- Concurrent Mark Sweep (CMS) Collector
 ```
 -XX:+UseConcMarkSweepGC
 -XX:-UseGCOverheadLimit
  -XX:CMSInitiatingOccupancyFraction=<N>// value of N[0,100]
 ```
- Garbage-First Garbage Collector
```

```