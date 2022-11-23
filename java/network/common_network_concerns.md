####how to configure custom DNS server
```
configure below system properties to specify name service's address
-Dsun.net.spi.nameservice.nameservers=8.8.8.8
-Dsun.net.spi.nameservice.provider.1=dns,sun

configure below system properties we can customize dns server cache ttl

networkaddress.cache.ttl
Indicates the caching policy for successful name lookups from the name service. The value is specified as as integer to indicate the number of seconds to cache the successful lookup. The default setting is to cache for an implementation specific period of time.
A value of -1 indicates "cache forever".
networkaddress.cache.negative.ttl (default: 10)
Indicates the caching policy for un-successful name lookups from the name service. The value is specified as as integer to indicate the number of seconds to cache the failure for un-successful lookups.
A value of 0 indicates "never cache". A value of -1 indicates "cache forever"
```
