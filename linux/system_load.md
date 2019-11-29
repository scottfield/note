###the system load is related to the cpu utilization

e.g. we have system load as the following, it has different means under different cpu cores

```
23:16:49 up  10:49,  5 user,  load average: 1.00, 0.40, 3.35
```

####On a single core system this would mean:
- The CPU was fully (100%) utilized on average; 1 processes was running on the CPU (1.00) over the last 1 minute.
- The CPU was idle by 60% on average; no processes were waiting for CPU time (0.40) over the last 5 minutes.
- The CPU was overloaded by 235% on average; 2.35 processes were waiting for CPU time (3.35) over the last 15 minutes.

####On a dual-core system this would mean:

- The one CPU was 100% idle on average, one CPU was being used; no processes were waiting for CPU time(1.00) over the last 1 minute.
- The CPUs were idle by 160% on average; no processes were waiting for CPU time. (0.40) over the last 5 minutes.
- The CPUs were overloaded by 135% on average; 1.35 processes were waiting for CPU time. (3.35) over the last 15 minutes.

###获取系统负载信息
```
~ $ uptime
or
~ $ cat /proc/loadavg
```
###获取CPU核心数
```
~ $ grep "model name" /proc/cpuinfo | wc -l
or
~ $ nproc
```