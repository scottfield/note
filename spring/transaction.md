###how does @EnableTransactionManagement works
the @EnableTransactionManagement will trigger to load
|
V
TransactionManagementConfigurationSelector, the selectImports of this selector will determine
what kind of proxy configuration should be loaded base on AdviceMode method argument
|
V
load ProxyTransactionManagementConfiguration and AutoProxyRegistrar if advice mode is PROXY
- ProxyTransactionManagementConfiguration:configure transaction interceptor and BeanFactoryTransactionAttributeSourceAdvisor bean
- AutoProxyRegistrar: handle auto proxy creator registering base on annotation on configuration class( the qualified annotation should
have mode attribute of type AdviceMode and proxyTargetClass of type Boolean.
e.g.@EnableTransactionManagement,@EnableAsync,@EnableAspectJAutoProxy,@EnableCaching etc.).
|
V
when a bean created, the auto proxy creator will be applied to create a proxy if any methods of this bean,
or the bean class itself is annotated with @Transactional annotation.
|
V
when a proxied method called, the transaction interceptor will try to load the transaction attribute of this method 
by using the transaction attribute source,if the attribute is exist, will open a transaction to handle this method invocation. 



###spring事务相关类说明
ProxyTransactionManagementConfiguration(this is the configuration class used for setup transaction related infrastructure beans)


Advisor
  ^--PointcutAdvisor
    ^--AbstractPointcutAdvisor
      ^--AbstractBeanFactoryPointcutAdvisor
        ^--BeanFactoryTransactionAttributeSourceAdvisor(used for holding the TransactionInterceptor and AnnotationTransactionAttributeSource pointcut)

TransactionAspectSupport
  ^--TransactionInterceptor(this interceptor will hold the transaction manager and responsible for opening a transaction if necessary)
  
- transaction注解解析器，用于支持解析各种不同的事务定义注解将其解析为TransactionAttribute对象
TransactionAnnotationParser
  ^--SpringTransactionAnnotationParser
  ^--JtaTransactionAnnotationParser
  ^--Ejb3TransactionAnnotationParser

- 指定如何从方法上获取事务信息
TransactionAttributeSource
  ^--AnnotationTransactionAttributeSource(将@Transaction注解定义的事务定义转换为transactionAttribute)
  ^--org.springframework.transaction.interceptor.NameMatchTransactionAttributeSource(use this one to define pattern based transaction attribute for different type of methods)
  ^--org.springframework.transaction.interceptor.CompositeTransactionAttributeSource(use this one to combine multiple transaction attribute source)
  
 
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

###enable logging to see if transactions are open and closed correctly
```
//this is a logback configuration
<logger level="trace" name="org.springframework.transaction.interceptor"/>
``` 
