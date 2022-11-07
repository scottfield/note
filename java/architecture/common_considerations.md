###微服务的优缺点
优点：
- 独立部署，发布周期短，在发生错误时能很好的进行隔离
- 代码模块化，按照业务功能进行划分，更好的代码可读性（更好理解）
- 更好的扩展性，可以针对单个的服务进行水平扩缩容
- 每个服务可以依据业务特性选择合适的开发语言

缺点：
- 数据一致性问题(最终一致性,补偿操作)，但是只要补偿操作带来的损失是小于更好的强一致性带来的收益时这种做法都是值得的
- 由于网络通信，而网络本身又是不稳定的因此需要服务具有有更高的容错性(客户端负载均衡，网络超时，错误重试，服务降级，错误隔离)
- 要求更高的实时监控和日志收集基础设施来观察各个服务的健康情况(各种基础指标，业务指标)
- 大量的微服务不易于管理(配置管理)
- 全局测试更加困难，测试某个服务不仅需要当前服务可以，还要确保其所依赖的所有服务也可用
- 更高的安全性要求，确保服务之间能安全的通信
- 增加整体系统的复杂性
- 问题定位更加困难，不同系统间可能日志格式各不相同，需要有能力把各个系统日志串连起来的能力

###服务治理
- 服务注册发现：Eureke，Nacos，Consul，ZooKeeper
- 服务配置：Spring Cloud Config，Archaius
- 服务熔断：Hystrix，resilience4j
- 网关：Zuul，Spring Cloud Gateway
- 客户端负载均衡：Ribbon，Feign
- 链路追踪工具：Sleuth，Zipkin，Htrace,skywalking
- 日志采集：logback，ElasticSearch
- 监控平台：Promethues，Kibana，grafna，Spring boot admin

###服务网格化(service mesh)

###如何评估一门语言
- 类型系统
    良好的类型系统应该具备优秀的类型推断能力，以及高级抽象数据类型支持(例如泛型)可以将很多编程错误在编译时期就能检查出来，这将极大的提高代码的稳定性
- 学习难度
     易学，容易上手，能减少开发人员的学习成本
- 空值
     如果语言不再带空值处理则需要人工的判断，这会增加很多模板代码破坏代码风格
- 错误处理
     捕获异常并不是一种好的错误处理方式。抛出异常本身没有问题，但仅适用于程序没有办法恢复而必须崩溃这类异常情况。异常和空值一样，会破坏类型系统。
- 并发
   语言自带并发支持能更容易的利用多核的优势，实现高性能的程序
- 不可变性
   不可变对象的支持能避免很多并发访问的问题，从而实现更优雅的并发代码
- 生态系统和工具链
    强大的生态和工具链有助于提高开发效率，在遇到不熟悉的问题时也更容易找到解决方案
- 速度
    编译速度快能提升开发效率
    启动速度快能更好的支持水平扩展
    运行速度快可以提升系统的吞吐量
- 诞生年代
     一般而言，新设计的语言能更好的支持当下的软硬件，而且通常也会修复已有语言的一些痛点


###常用技术
####负载均衡
#####LVS(Linux Virtual Server)网络接入层
- LVS/NAT(LVS需同时处理请求/响应流量，请求和响应都需要经过LVS设备，会导致性能瓶颈)
- LVS/DR(LVS只需处理请求流量，LVS通过修改源mac地址来实现不改源IP而能路由请求到对应的后端服务，后端服务需要和LVS部署在同一个机房)
- LVS/TUNNEL(LVS只需处理请求流量，LVS可以跨机房调用后端服务，但是需要后端服务支持tunnel模式对IP报文进行二次解析)
#####nginx(openresty)应用层接入
-分布式会话

#Dubbo服务治理


####消息中间件
- activemq
- kafka(适合流式处理)
- rocketmq(支持事务消息)

####任务调度
- Timer (单线程执行环境，任务异常将导致整个调度程序结束，所有任务是按顺序执行,支持定时触发和规定频率触发以及延迟触发)
- ScheduledExecutorService (多线程执行环境,自动补偿异常退出线程，支持定时触发和规定频率触发以及延迟触发)
- Quartz(多线程执行环境,自动补偿异常退出线程，支持crontab这种复杂的调度规则以及misfire机制)
- Elastic Job (支持分布任务调度,任务分片)

####池化技术(线程池，连接池)

####缓存

####数据库选型SQL vs NOSQL

####服务监控

####服务隔离,队列，限流，熔断与降级

####服务间的通信方式
- gRPC
PROS:
    - Lightweight messages(up to 30% smaller in size than JSON)
    - high performance(5~8 times faster than REST+JSON)
    - build-in code generation(no need to write client code)
    - more connection options(not only support request-response style communication, also support data streaming)
Cons:
    - community is not as mature as REST
    - browser dont support gRPC call
    - lack of debugging tools such as curl, postman
    - Not human-readable format
    - steeper learning curve

when to use gRPC:
    - Real-time communication services where you deal with streaming calls
    - When efficient communication is a goal
    - In multi-language environments
    - For internal APIs where you don’t have to force technology choices on clients
    - New builds as part of transforming the existing RPC API might not be worth it

- REST
Pros:
    - Easy to understand.
    - Web infrastructure is already built on top of http
    - Tools for in inspection, modification, testing are readily available.
    - Loose coupling between client and server makes changes relatively easy.
    - There are lots of frameworks in most of the widely used languages to create REST Api’s.
    - Http status codes are well-defined and helps in identifying cause of problems
Cons:
    - need to write client by yourself
    - lack of streaming support
    - duplex streaming is impossible
    - hard to get multiple resource in a single request
    - need semantic versioning whenever contracts needs to change
