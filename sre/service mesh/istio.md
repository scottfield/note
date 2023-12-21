### how Istio works
Istio Gateway, VirtualService, and DestinationRule are three core components in Istio's traffic management model. They work together in a seamless way to control the routing of traffic in an Istio service mesh.

1. Gateway: The Gateway describes a load balancer operating at the edge of the mesh, receiving incoming or
outgoing HTTP/TCP connections. It configures exposed ports, protocols, etc. The Gateway is responsible for
exposing services to the outside world.

2. VirtualService: The VirtualService component defines the rules that control how requests for a service 
are routed within an Istio service mesh. It binds itself to a set of gateways and then describes the routing rules.
You can use a VirtualService to configure traffic routing based on HTTP paths and headers, retries, timeouts, and other settings.

3. DestinationRule: The DestinationRule defines policies that apply to traffic intended for a service after
routing has occurred. They define configurations like load balancing policies, outlier detection, 
or circuit breaker settings. Basically, how requests are handled after being routed by the VirtualService.

The way these three components work together can be summarized as follows: 
The Gateway defines how the external traffic is allowed in. The VirtualService defines how the traffic is routed 
to different services. The DestinationRule defines the behavior of traffic after being routed. For services 
exposed to external traffic, you might use all three. For internal services, you might just use VirtualService and DestinationRule.