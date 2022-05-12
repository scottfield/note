###innodb structure
![innodb structure](innodb-architecture.png)
###buffer pool list
![innodb structure](innodb-buffer-pool-list.png)
###change buffer
![innodb structure](innodb-change-buffer.png)

###innodb逻辑存储结构
- 表空间（tablespace）
- 段（segment）
- 区（extent）64个页即1M
- 页（page）16KB
- 行（row）
###行记录的存储格式分为compact和redundant
- 每行数据除了用户定义的列以外还有两个隐藏列，事务ID列（6字节）和回滚指针列（7字节），如果没定义主键还会自动生成一个rowid列（6字节）
- Null值不占用存储空间，只用Null标志位来标识
- 一行最多支持1023个列
- 可以通过在建表时指定ROW_FORMAT参数来指定存储格式
###MySQL支持的分区类型
- range
- list
- key
- column
- hash
###不同应用类型是否应该使用分区
- 对于在线事务处理（OLTP）的应用类型使用分区得十分小心，往往不能带来性能提升反倒降低性能
- 对于在线分析处理（OLAP）的应用类型则比较适合使用分区
###innodb支持的索引类型
- B+树索引（由平衡二叉树演变而来）
    - 聚集索引（clustered index）叶节点保存整行数据
    - 辅助聚集索引(secondary index)
    - 联合索引
- 自适应哈希索引（自动生成无法人工干预,只有等值查询时才会用到自适应哈希索引,可以通过innodb_adaptive_hash_index来禁用/开启该特性）
###何时该使用联合索引
是在一张表的多个字段添加索引，如果查询是根据联合索引的第一个字段进行过滤然后通过索引的后面字段排序就比较适合使用联合索引，因为联合索引的数据也是按顺序存储因此查询可以省掉一次filesort的操作

###通过show engine innodb status可以查看自适应哈希索引的使用信息

###删除/添加索引时MySQL是如何操作的？
先创建一张临时表，导入数据，删除原表，临时表更名为原表名
对于辅助索引可以使用快速索引创建方法
###如何查看表的索引信息
使用show index from tbl_name来查看表索引
###如和理解表的cardinality
cardinality越大表示列的取值范围越大，是重复度低，适合使用B+树索引，反之如果索引的cardinality非常小则可以考虑删除该索引
使用analyze table来更新索引的cardinality
可以在非业务高峰段使用analyze table来优化核心表，以便更好的利用索引提高查询性能
###MySQL优化器什么时候会使用索引？
当查询的数据占全表的数据大部分时查询优化器会使用全表扫描而不会使用索引，只有在查询数据占全表少部分数据时才会使用索引，
但是也可以通过select * from tbl_name force index（index_name）来强制使用索引
###为什么优化器要这样做？
因为传统的机械硬盘的随机读性能是远低于顺序读的性能，所以当需要读入一个表中的大部分数据时显然采用全表扫描进行顺序读取性能更好，
但是如果使用的是固态硬盘可能强制使用索引查询效率会更好，因为固态硬盘没有读写磁头，因此其随机读取性能很高
###innodb的锁类型有哪些
- 行级锁：共享锁(S)，排他锁(X)
    只有两个共享锁(SS)是兼容的，共享锁和排他锁或两个排他锁都是互斥的
- 表级锁
- 意向锁：意向共享锁，意向排他锁
###如何查看锁请求信息
- 方式一：
    show engine innodb status
    show full processlist

- 方式二：
    也可以查看information_schema中的三张表
    innodb_trx
    innodb_locks
    innodb_lock_waits
###如何查看连接的事务隔离级别
select @@tx_isolation
###一致性非锁定读在不同隔离级别下的区别
- read committed隔离级别下总是读取最新的快照版本
- repeatable read隔离级别下则是永远读取事务开始时的快照版本
###如何手动添加行锁(语句都必须在事务中执行)
- select ... for update对读取的行记录加一个X锁，其他任何事务想在这行上加任何锁都会被阻塞
- select ... lock in share mode 对读取的行加一个S锁，其他事务可以向被锁定的记录加S锁，但对于加X锁则会被阻塞

###锁算法
- record lock
- gap lock
- next-key lock
###自增长列的实现原理
- 插入类型
    - simple insert：表示在插入前就能知道插入行数的语句比如insert ..., replace ...
    - bulk insert:表示在插入前不能确定插入行数的语句比如 insert ... select, replace ... select
自增长列可以有三种不同的模式，通过以下参数配置
- innodb_autoinc_lock_mode进行设置
    - 0表示auto-inc locking模式，对于插入语句是逐条执行的
    - 1表示对于 simple insert采用对内存计数器的互斥量来解决，而对于bulk insert则是使用auto-inc locking
    - 2表示对所有插入都采用内存互斥量
###使用锁带来的问题
- 丢失更新
- 脏读
- 不可重复读
###阻塞相关设置
- innodb_rollback_on_timeout超时后是否回滚事务，默认不回滚
- innodb_lock_wait_timeout事务等待锁的超时时间

###innodb对死锁情况的自动处理
- 当innodb检测到死锁时会自动回滚一个事务
- innodb会自动对外键添加索引以防止死锁，而且该索引不能人为删除
###为什么innodb引擎没有锁升级的问题
innodb不会发生锁升级，一个锁与10000个锁对于innodb的开销都是一样的

###如何提高innodb数据写入可靠性
- 开启双写机制（double write）,可以解决部分写失效问题（partial page write）
- 参数skip_innodb_doublewrite可以开启或关闭双写
###慢查询日志设置参数
- long_query_time慢查询阈值
- log_slow_queries是否开启慢查询日志
- log_queries_not_using_indexes
- log_out控制慢查询日志输出位置，默认为file，当设置为table时会把慢查询日志输出到mysql.slow_log表中
###查询日志
- 可以被保存到表general_log中
