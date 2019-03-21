###start up app without database available
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
###how springboot load application(yml/properties) config file
```
org.springframework.boot.context.config.ConfigFileApplicationListener.Loader#load(org.springframework.boot.env.PropertySourceLoader, java.lang.String, org.springframework.boot.context.config.ConfigFileApplicationListener.Profile, org.springframework.boot.context.config.ConfigFileApplicationListener.DocumentFilter, org.springframework.boot.context.config.ConfigFileApplicationListener.DocumentConsumer)
```