spring use BeanPostProcessor to create proxy object,
following class will handle processes all AspectJ 
annotation aspects in the current application context,
as well as Spring Advisors.
```
org.springframework.aop.aspectj.annotation.AnnotationAwareAspectJAutoProxyCreator
```
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


  org.aopalliance.intercept.Interceptor