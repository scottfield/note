###why we need async IO
###the drawbacks of blocking IO
- most of the time, threads are in dormant, they are waiting for input or output of data
- each thread need consume about 64KB~1M stack memory
- the context-switch overhead is expensive with increasing threads count.

###how to achieve a non-blocking IO
1. hardware interrupts
2. signals(inter-process communication)
3. event loop(current solution)


##how does IO works in OS level
- Buffer handling
- Kernel versus user space
- Virtual memory
- Paging
- File-oriented versus stream I/O
- Multiplexed I/O (readiness selection)


##IO type
- block IO(typical file IO)
- stream IO(socket(network connections),console,printer port)
  nonblocking mode and readiness selection
###OS level async IO support
- IOCP(IO completion port) for windows,
- epoll,io_uring(since linux kernel 5.1) for linux system
- kqueue for unix system


###important netty interface
ServerBootstrap
Bootstrap
EventLoopGroup
EventLoop

ChannelPipeline
ChannelHandlerContext
io.netty.channel.Channel
ChannelGroup
ChannelInitializer
ChannelHandler,ChannelInboundHandler, ChannelOutboundHandler,ChannelDuplexHandler
ChannelHandlerAdapter, ChannelInboundHandlerAdapter, ChannelOutboundHandlerAdapter,CombinedChannelDuplexHandler, 
SimpleChannelInboundHandler(auto release bytebuf), 
SimpleUserEventChannelHandler
ChannelFuture,io.netty.util.concurrent.Future

ByteBuf
ByteBufHolder
ByteBufAllocator
ByteBufUtil
Unpooled
ReferenceCounted
ReferenceCountUtil

###Channel lifecycle callback
- channelRegistered 
    The Channel is registered to an EventLoop.
- channelActive 
    The Channel is active (connected to its remote peer). It’s now possible to receive and send data.
- channelInactive 
    The Channel isn’t connected to the remote peer.
- channelUnregistered 
    The Channel was created, but isn’t registered to an EventLoop.
###Channel state change model
ChannelRegistered==> ChannelActive==> ChannelInactive==> ChannelUnregistered

###Channel handler lifecycle
- handlerAdded 
    Called when a ChannelHandler is added to a ChannelPipeline
- handlerRemoved 
    Called when a ChannelHandler is removed from a ChannelPipeline
- exceptionCaught
    Called if an error occurs in the ChannelPipeline during processing

###how to enable memory leak detection
```
JVM option
'-Dio.netty.leakDetectionLevel=ADVANCED'
``` 
