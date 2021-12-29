###node的异步IO是如何实现的
    node使用多线程和非阻塞IO来实现高效的异步IO，并利用事件循环将js代码和底层IO操作进行衔接，
    使用libuv来封装各个平台下不同的非阻塞IO方案
    Linux：epoll
    Unix:kqueue
    Windows:IOCP
###node中有哪些异步编程解决方案
- 事件发布/订阅模式
    适用于事件于业务逻辑是一对多的场景
    node核心库EventEmitter 或使用基于EventEmitter封装的第三方库，例如eventproxy库
- promise/deferred模式
    核心模块Promise，when模块
- 流程控制库
    尾触发(例如connect中间件)
    async模块
    streamline模块
###V8
- 内存限制
    默认64位系统为1.4G，32位系统为0.7G
    可以使用以下参数在启动node时进行调节
    ```
    --max-old-space-size
    --max-new-space-size
    ```
- 自动垃圾回收
    V8也是使用分代垃圾回收器来进行垃圾回收
- 如何突破V8的内存使用限制
    - 使用Buffer对象来操作堆外内存
    - 使用上面的启动参数来调节默认内存大小
###内存泄露的常见原因
- 使用内存当缓存
- 队列的堆积
###内存泄露排查工具
- heapdump
- memwatch
