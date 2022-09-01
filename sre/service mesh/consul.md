###what problems consul can address
- service discovery
- central configuration management(consul kv store)
- service segmentation(enforce mTLS)

###start up consul agent
```
consul agent -dev
```

###get nodes info
```
use consul command
consul members  

or query http endpoint
curl localhost:8500/v1/catalog/nodes

or query dns server
dig @127.0.0.1 -p 8600 LEUSX1909521680
```

###graceful shutdown consul agent
```
consul leave
```

###query service
```
query by DNS
dig @127.0.0.1 -p 8600 {service_name}.service.consul SRV

list all services by http
curl http://localhost:8500/v1/catalog/services

query service detail by http
curl http://localhost:8500/v1/catalog/service/{service_name}

query healthy service instance by http 
curl 'http://localhost:8500/v1/health/service/{service_name}?passing'

```
