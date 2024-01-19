### kubectl Output log flag:
```shell
--v=8
```
### Set context's default namespace
```shell
kubectl config set-context kube-cluster-ctx --namespace=my-namespace
```
### how to specify flags:
```shell
k top pods -n cpc --sort-by=memory
```

### get all api resources:
```shell
kubectl api-resources --sort-by=name
```
### Get logs at specific time and limit output only 100 characters each line:
```shell
k logs  pod_name -n namespace -c container_name --since-time=2020-03-04T21:00:57Z --limit-bytes=10000 --timestamps=true|cut -c1-100
```
### Connect to pod's service by port forwarding:
```shell
kubectl port-forward pod_name service_port:local_port
```

### Copy logs from pod to local machine:
```shell
kubectl cp cpc-cart-app-55b558879-psgh5:/home/app/tomcat/bin/threaddump.txt cart_threaddump.txt -c cpc-cart-app -n cpc
```

### Check cluster context information:
```shell
kubectl config get-contexts
kubectl config use-context
kubectl config current-context
```

### create a deployment
```
kubectl create deployment {deployment_name} --image={docker_image_name}
```
### view all deployments
```
kubectl get deployments
```
### view all pods
```
kubectl get pods
```
### view all pods filtered by label
```
kubectl get pods -l app=v1
```
### view cluster events
```
kubectl get events
```
### view services
```
kubectl get services
```
### view kubectl configuration
```
kubectl config view
```
### create a service
```
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
```
### get pods detail
```
kubectl describe pods
```
### get pod name and store into variable
```
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
```
### get logs for container
```
kubectl logs $POD_NAME
```
### execute command in pod's container(can omit container name when pod contains only one container)
```
kubectl exec $POD_NAME env
```
### open a bash in pod container(can omit container name when pod contains only one container)
```
kubectl exec -ti $POD_NAME bash
```
### update pod's label
```
kubectl label pod $POD_NAME app=v1
```
### update deployment's image
```
kubectl set image deployments/{deployment_name} {container_name}={image_name}
```
### watch the rollout status of deployment
```
kubectl rollout status deployment/{deployment_name}
```
### rollback rollout
```
kubectl rollout undo deployments/{deployment_name}
```
### how to trigger a threaddump in a container and save it into local machine:
```shell
k exec  pod_name  -c container_name -n namespace jstack 16 > test.tdump
```

### Get All Pod Image information(please use below command in bash shell):
kubectl get pods -n namespace -o jsonpath="{..image}" |tr -s '[[:space:]]' '\n' |sort |uniq -c > images.txt

### Check if node rebooted:
k get events | findstr Reboot

### rolling restart deployment:
kubectl rollout restart deployment <deployment-name>  -n <namespace>
## what's Service ?
A Service in Kubernetes is an abstraction which defines a logical set of Pods and a policy by which to access them.
Services enable a loose coupling between dependent Pods.
An API object that describes how to access applications, such as a set of Pods , and can describe ports and load-balancers.
The access point can be internal or external to the cluster.
## what's Pod ?
The smallest and simplest Kubernetes object. A Pod represents a set of running containers on your cluster.
A Pod is typically set up to run a single primary container. 
It can also run optional sidecar containers that add supplementary features like logging.
Pods are commonly managed by a Deployment.
## what's Deployment ?
 An API object that manages a replicated application.
 Each replica is represented by a Pod Lifecycle , and the Pods are distributed among the nodes of a cluster. 
 
## what's Node ?
A node is a worker machine in Kubernetes.
A worker machine may be a VM or physical machine, depending on the cluster.
It has the Services necessary to run Pods and is managed by the master components.
The Services on a node include Docker, kubelet and kube-proxy.

### pod initialization
![innodb structure](pod-init-to-ready.png)

### why we use init container
Separation of concerns
Security
