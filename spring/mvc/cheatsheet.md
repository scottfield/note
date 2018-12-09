##spring mvc常用配置
###配置jackson2转换日期的格式
```
@Bean
public HttpMessageConverter jsonMessageConverter() {
    ObjectMapper objectMapper = Jackson2ObjectMapperBuilder.json().dateFormat(new SimpleDateFormat("MM/dd/yyyy HH:mm:ss")).build();
    return new MappingJackson2HttpMessageConverter(objectMapper);
}
```
###开启详细日志
```
enable mvc logger level as TRACE
<Logger name="org.springframework.web.servlet" level="TRACE"/>

print request and response detail
org.springframework.web.servlet.FrameworkServlet#enableLoggingRequestDetails=true
```