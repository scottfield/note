###spring事务相关类说明
ProxyTransactionManagementConfiguration


Advisor
  ^--PointcutAdvisor
    ^--AbstractPointcutAdvisor
      ^--AbstractBeanFactoryPointcutAdvisor
        ^--BeanFactoryTransactionAttributeSourceAdvisor

TransactionAspectSupport
  ^--TransactionInterceptor
  
- transaction注解解析器，用于支持解析各种不同的事务定义注解将其解析为TransactionAttribute对象
TransactionAnnotationParser
  ^--SpringTransactionAnnotationParser
  ^--JtaTransactionAnnotationParser
  ^--Ejb3TransactionAnnotationParser

- 指定如何从方法上获取事务信息
TransactionAttributeSource
  ^--AnnotationTransactionAttributeSource(将@Transaction注解定义的事务定义转换为transactionAttribute)
 
- 事务信息的抽象数据定义
TransactionDefinition(定义传播行为、隔离级别、只读事务、超时设置以及事务名称)
  ^--TransactionAttribute(扩展支持rollbackOn特性)
    ^--DefaultTransactionAttribute
      ^--RuleBasedTransactionAttribute(如果是通过spring自带的或JTA的@Transactional就返归该对象)

PlatformTransactionManager
   ^--AbstractPlatformTransactionManager
      ^--JpaTransactionManager
      ^--DataSourceTransactionManager

TransactionStatus
TransactionSynchronizationManager
TransactionSynchronization
