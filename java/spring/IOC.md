ContextLoaderListener
|
V
ContextLoader
|
V
AbstractApplicationContext
BeanFactoryPostProcessor
BeanDefinitionRegistryPostProcessor
ConfigurationClassPostProcessor
####ConfigurationClassParser

####bean definition(对bean的数据结构定义)
BeanDefinition
  ^--AnnotatedBeanDefinition
  ^--AbstractBeanDefinition
    ^--RootBeanDefinition
    ^--ChildBeanDefinition
    ^--GenericBeanDefinition
      ^--ChildBeanDefinition
      ^--AnnotatedGenericBeanDefinition
####Bean Definition Reader(读取bean的配置将其转换为bean definition)
BeanDefinitionReader
AnnotatedBeanDefinitionReader
ClassPathBeanDefinitionScanner
XmlBeanDefinitionReader
PropertiesBeanDefinitionReader
ConfigurationClassBeanDefinitionReader      

####Bean Definition Registry(用于注册bean definition)
BeanDefinitionRegistry
  ^--DefaultListableBeanFactory
  ^--GenericApplicationContext

####BeanFactoryPostProcessor (用于修改bean definition)
BeanFactoryPostProcessor
  ^--PropertyResourceConfigurer
    ^--PropertyOverrideConfigurer
    ^--PlaceholderConfigurerSupport
  ^--BeanDefinitionRegistryPostProcessor(可以用于在 BeanFactoryPostProcessor调用前注册额外的Bean定义，例如@Configuration注解就是通过ConfigurationClassPostProcessor来解析定义的bean)

