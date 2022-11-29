###Finding containers with tight CPU limits
```
(sum by
(namespace,pod,container)(rate(container_cpu_usage_seconds_total{container!=""}[5m])) / 
sum by(namespace,pod,container)(kube_pod_container_resource_limits{resource="cpu"})) > 0.8
```

###Finding containers without CPU limits by namespace
```
sum by (namespace)
(count by (namespace,pod,container)(kube_pod_container_info{container!=""})
unless sum by (namespace,pod,container)(kube_pod_container_resource_limits{resource="cpu"}))
```
###check CPU over committing in cluster
```
100 * sum(kube_pod_container_resource_limits{container!="",resource="cpu"} ) /
sum(kube_node_status_capacity_cpu_cores)
```


https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt
https://www.kernel.org/doc/Documentation/scheduler/sched-design-CFS.txt
