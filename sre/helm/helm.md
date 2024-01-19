### Rollback:
```shell
helm rollback --tiller-namespace=namespace chart_name 0
helm init --client-only
helm repo add stable repo_url
get install failed error:
helm ls --tiller-namespace=namespace
Helm history --tiller-namespace=namespace chart_name
Helm delete --tiller-namespace=namespace chart_name --purge
Helm status release_name
```
