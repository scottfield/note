##spring mvc常用配置
###配置jackson2转换日期的格式
```
@Bean
public HttpMessageConverter jsonMessageConverter() {
    ObjectMapper objectMapper = Jackson2ObjectMapperBuilder.json().dateFormat(new SimpleDateFormat("MM/dd/yyyy HH:mm:ss")).build();
    return new MappingJackson2HttpMessageConverter(objectMapper);
}
```