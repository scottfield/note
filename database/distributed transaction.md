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
 
 
###处理方案
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
   
- 补偿模式
    TCC(Try/Confirm/Cancel)
