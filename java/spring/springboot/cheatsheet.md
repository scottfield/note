### how springboot detect which autoConfiguration class should be loaded and processed
```
Spring Boot loads auto-configuration classes during the application startup process using the following steps:

1. Identify auto-configuration classes: Spring Boot auto-configuration classes are annotated with `@Configuration`
   and are usually located in the `spring.factories` file under the `org.springframework.boot.autoconfigure.EnableAutoConfiguration` key.
   This file is present in the `META-INF` directory of the auto-configuration library (such as `spring-boot-autoconfigure`).

2. Enable auto-configuration: In your main application class, you should have the `@SpringBootApplication` annotation. 
   This annotation includes the `@EnableAutoConfiguration` annotation, which triggers the auto-configuration process.

3. Load auto-configuration classes: When the application starts, Spring Boot reads the `spring.factories` file and loads all auto-configuration classes listed there.

4. Conditionally enable configurations: Spring Boot evaluates the conditions specified in the auto-configuration classes using annotations 
   like `@ConditionalOnClass`, `@ConditionalOnBean`, `@ConditionalOnMissingBean`, etc. If the conditions are met, the configurations in the auto-configuration class are enabled.

5. Ordering: Auto-configuration classes can be ordered using the `@AutoConfigureOrder`, `@AutoConfigureBefore`, and `@AutoConfigureAfter` annotations to control the order
   in which they are processed. This can be useful when one auto-configuration class depends on another or when you need to ensure 
   that a custom configuration is applied before or after a specific auto-configuration.

6. Register beans: Spring Boot processes the enabled auto-configuration classes and registers the beans defined in them using the `@Bean` annotation.

7. Use auto-configured beans: The auto-configured beans are now part of the application context and can be injected and used throughout your application.
   By following these steps, Spring Boot loads and applies auto-configuration classes during application startup, 
   making it easy to configure common components with minimal manual configuration.

```
### start up app without database available
```
 @Bean(name = "mysqlEntityManager")
    public LocalContainerEntityManagerFactoryBean mysqlEntityManagerFactory() {
        HibernateJpaVendorAdapter vendorAdapter = new HibernateJpaVendorAdapter();
        vendorAdapter.setDatabasePlatform("org.hibernate.dialect.MySQL5Dialect");
        LocalContainerEntityManagerFactoryBean factoryBean = new LocalContainerEntityManagerFactoryBean();
        factoryBean.setDataSource(hyveDataSource());
        factoryBean.setJpaVendorAdapter(vendorAdapter);
        factoryBean.setPackagesToScan("com.synnex.service.hyve.assetdb.service.dao.entities.hyve");
        return factoryBean;
    }
```
### how springboot load application(yml/properties) config file
```
org.springframework.boot.context.config.ConfigFileApplicationListener.Loader#load(org.springframework.boot.env.PropertySourceLoader, java.lang.String, org.springframework.boot.context.config.ConfigFileApplicationListener.Profile, org.springframework.boot.context.config.ConfigFileApplicationListener.DocumentFilter, org.springframework.boot.context.config.ConfigFileApplicationListener.DocumentConsumer)
```