###some important terminologies in AOP
  - Advice:define what's the enhancement of an aspect, and when to apply to a target object.
  - Pointcut:when to apply the enhancement to the target object
  - Advisor: contains the advice and pointcut
  - JoinPoint: any invocation point in the program,namely the methods of all objects(in Spring AOP)

we can use AOP by either declarative or programmatically way.

###declarative way
manually configure a bean of type org.springframework.aop.framework.ProxyFactoryBean,
or use BeanPostProcessor to declarative create proxy objects,
we can register any one of the following auto-proxy creator beans to enable
automatically create proxy objects for candidate objects.
we can use either one of annotation @EnableAspectJAutoProxy or @EnableTransactionManagement 
on a @Configuration class to automatically register the auto-proxy creator accordingly.

  org.springframework.aop.framework.autoproxy.AbstractAutoProxyCreator
    |-- org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator(simple creator used for creating proxies by specified bean names)
    |-- org.springframework.aop.framework.autoproxy.AbstractAdvisorAutoProxyCreator
        |-- org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator
        |-- org.springframework.aop.aspectj.autoproxy.AspectJAwareAdvisorAutoProxyCreator
            |-- org.springframework.aop.aspectj.annotation.AnnotationAwareAspectJAutoProxyCreator(support declare AOP by aspectJ annotations)
        |-- org.springframework.aop.framework.autoproxy.InfrastructureAdvisorAutoProxyCreator(default creator for transaction management)

###programmatically way
we can use ProxyFactory class to manually setup and create proxy objects
```
org.springframework.aop.framework.ProxyFactory#getProxy(java.lang.Class<T> proxyInterface, org.aopalliance.intercept.Interceptor interceptor)
```
###how Spring creates a proxy object
no matter which style you choose to use spring AOP, under the hood, spring
always use the AopProxyFactory(DefaultAopProxyFactory) to create a proxy object.
inside the AopProxyFactory, it will read the aop configuration to determine what kind
of proxy object(JdkDynamicAopProxy or CglibAopProxy) should be created.  
                
AopProxyFactory--call createAopProxy to generate--> AopProxy   --call getProxy to generate--> a real Poxy Object.
for JdkDynamicAopProxy, it will build a ReflectiveMethodInvocation which contains all interceptors.
when this ReflectiveMethodInvocation is invoked, the interceptors will be called one by one until the invocation on the method of target object.


###different type of advice supported by spring AOP
```

 |-- org.aopalliance.aop.Advice 
    |-- org.aopalliance.intercept.Interceptor
        |-- org.aopalliance.intercept.MethodInterceptor
            |-- org.springframework.aop.framework.adapter.MethodBeforeAdviceInterceptor    
            |-- org.springframework.aop.aspectj.AspectJAfterAdvice
    |-- org.springframework.aop.BeforeAdvice
        |-- org.springframework.aop.MethodBeforeAdvice
            |-- org.springframework.aop.aspectj.AspectJMethodBeforeAdvice
    |-- org.springframework.aop.AfterAdvice
        |-- org.springframework.aop.ThrowsAdvice(this is a tag interface)
        |-- org.springframework.aop.AfterReturningAdvice
            |-- org.springframework.aop.aspectj.AspectJAfterReturningAdvice
```

###advanced feature
- TargetSource: you can use this interface to dynamically get the target object,e.g. get from database query, or hot swap the current target object.
