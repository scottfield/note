open source solution:
- SEATA: 
    https://seata.io/zh-cn/docs/overview/what-is-seata.html
    https://github.com/seata/seata
- DTM
    https://github.com/yedf/dtm
    

reliable messaging solutions
the local message scheme or the transaction message scheme.
TCC scheme(high consistency)
 SAGA mode(low consistency
 the XA solution is suitable)
###使用XA协议(2PC)
可用的实现：Atomikos and Bitronix.
优点：使用简单，大部分数据库都支持XA协议，Java中可以使用JTA来集成到应用中
缺点：
- 锁定资源的时间过长，导致系统的吞吐量很差，而且容易导致死锁。(不适合跨服务的微服务架构)
- TM(Transaction Manager)如果挂掉会导致单点故障
- 有可能造成split-brain的问题，如果TM在两阶段提交的第二阶段出现故障时可能会导致一些RM收到了TM的提交/回滚指令
  而一部分RM没有收到相应的指令，在TM恢复后由于decision log丢失或损坏而无法重发之前的指令，从而造成数据一致性的问题。
- 在发生TM挂掉的情况下，作为一种应急方案，RM允许自己觉得是否commit/rollabck，这违反了事务的原子性原则，从而可能会造成数据不一致的问题。
- 虽然后面出现了改进的3PC协议来解决单点故障和长时间锁定资源，但是3PC仍然无法解决split-brain的问题。

 
###消息事件处理方案
 - 可靠事件通知模式
 ```
    本地同步事件方案(应用服务器与消息服务器间的网络异常和应用服务器宕机会导致主服务提交数据库事务失败，而消息却被从服务消费的情况)
     |优化
     V
     本地异步事件方案(需要保存消息到本地数据库，高并发场景导致数据库性能下降)
     |优化
     V
     外部事件服务(事务消息)方案(多了一次确认消息的网络开销，需要单独提供消息状态查询接口)
```
  事件模式需要注意的有两点，1. 事件的正确发送 2. 消费端需要对重复消息进行幂等处理


 - 最大努力通知模式
    ```
        相比可靠事件通知模式，最大努力通知模式就容易理解多了。最大努力通知型的特点是，业务服务在提交事务后，
        进行有限次数（设置最大次数限制）的消息发送，比如发送三次消息，若三次消息发送都失败，则不予继续发送。
        所以有可能导致消息的丢失。同时，主业务方需要提供查询接口给从业务服务，用来恢复丢失消息。
        最大努力通知型对于时效性保证比较差（既可能会出现较长时间的软状态），所以对于数据一致性的时效性要求比较高的系统无法使用。
        这种模式通常使用在不同业务平台服务或者对于第三方业务服务的通知，如银行通知、商户通知等，这里不再展开。
   ```
   
###补偿模式TCC(Try/Confirm/Cancel)
开源实现：ByteTCC,Himly和TCC-transaction
本质上TCC也是一种两阶段提交协议的变种，需要应用提供三个接口，
Try接口：锁定资源
Confirm接口：提交锁定资源
Cancel接口：释放锁定资源
优点：无需长时间锁定资源，系统的吞吐量高
缺点：对业务有强侵入性，需要把原来的一个接口变成三个接口

由于会存在网络通信错误和异步网络延迟的问题，需要业务对提供的接口支持以下处理：
- 空回滚
- 幂等性
- 防悬挂

###补偿模式SAGA
事务中的每一个步骤都需要提供一个补偿步骤用于在发生错误时进行回滚操作。
开源实现：
- Choreography style:
    SEATA,eventuate

- Orchestration style:
    Apache Camel

