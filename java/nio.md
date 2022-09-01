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
