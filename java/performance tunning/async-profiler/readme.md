###profiler home page
https://github.com/async-profiler/async-profiler

###how to find humongous object in G1 collector
```shell
./profiler.sh -e G1CollectedHeap::humongous_obj_allocate -d 10 -f out.jfr 8983
```

###how to profile memory leak
```shell
#start live allocation profiling for LeakApplication
./profiler.sh -e alloc --live --total start LeakApplication
#trigger some load on the system
ab -n 10000 http://localhost:8080/hard 
#trigger GC to free memory
jcmd LeakApplication GC.run
#stop the profiler and export the profiling result as flame graph
./profiler.sh -f live.html stop LeakApplication
```

###some useful native method to profile
```shell
G1CollectedHeap::humongous_obj_allocate - trace the _humongous allocation_ of the G1 GC,
JVM_StartThread - trace the new thread creation,
Java_java_lang_ClassLoader_defineClass1 - trace class loading.
```

###different profiling mode
- wall clock profile suit for blocking IO related issue , such as start up time profiling.
```shell
./profiler.sh -e wall -t -i 5ms -f result.html 8983
```
- CPU profiling used to profile CPU intensive code
- Memory Allocation profiling is suitable for profiling memory leak issue
- Method profiling is very useful when you want to know what's the target method's call stack,the method can be native or java method full qualified name, also support wildcard method name
```shell
#profiling getProperty method of Properties class
./profiler.sh -e java.util.Properties.getProperty -t -i 5ms -f result.html 8983
#profiling all methods of Properties class
./profiler.sh -e java.util.Properties.* -t -i 5ms -f result.html 8983
#profiling the constructor method of NullPointerException class
./profiler.sh -e java.lang.NullPointerException.<init> -t -i 5ms -f result.html 8983
#profiling native method call
./profiler.sh -e G1CollectedHeap::humongous_obj_allocate -d 10 -f out.jfr 8983

```