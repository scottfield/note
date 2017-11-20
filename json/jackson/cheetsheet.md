##jackson2常用配置
###注解
- 对字段重命名
```
public class User implements Serializable {
   @JsonProperty("full_name") 
   private String name;
}
```