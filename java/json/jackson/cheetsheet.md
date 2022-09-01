##jackson2常用配置
###注解
- 对字段重命名
```
public class User implements Serializable {
   @JsonProperty("full_name") 
   private String name;
}
```
- 定义日期格式
```
@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "MM/dd/yyyy")
 private Date endDate;
```
