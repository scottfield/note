### OSI network model
7.application layer(HTTP,HTTPS,FTP,SMTP)
6.presentation layer(MIME,SSL/TLS,XDR)
5.session layer(Sockets)
4.transport layer(TCP,UDP,SCTP,DCCP)
    The transport layer provides the functional and procedural means of transferring variable-length data sequences
    from a source host to a destination host from one application to another across a network,
    while maintaining the quality-of-service functions. Transport protocols may be connection-oriented or connectionless.
3.network layer(e.g. IP,IPsec,ICMP,IGMP,OSPF,RIP)
    The network layer provides the functional and procedural means of transferring packets from one node to another connected in "different networks"
2.data link layer(e.g.PPP,SBTV,SLIP,802.3 Ethernet, 802.11 Wi-Fi, and 802.15.4 ZigBee)
    provides node-to-node data transfer—a link between two directly connected nodes
1.physical layer(e.g. network interface controller,ethernet hub, network switch)
    It converts the digital bits into electrical, radio, or optical signals


### TCP/IP network model
4.application layer(HTTP,FTP)
     providing process-to-process data exchange for applications
3.transport layer(TCP,UDP,SCTP)
     handling host-to-host communication
2.internet layer(IPv4,IPv6)
    providing inter-networking between independent networks
1.link layer(MAC,LLC)
    containing communication methods for data that remains within a single network segment (link)

### use fiddler to analyze java application network
```
start up java application with the following jvm options:
-Dhttp.proxyHost=localhost
-Dhttp.proxyPort=8888
then open fiddler you could see all network traffic of this application.
```
