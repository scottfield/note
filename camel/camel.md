###define type converter
step 1:
```java
import org.apache.camel.TypeConverter;
@Converter
public final class PurchaseOrderConverter {

    @Converter
    public static PurchaseOrder toPurchaseOrder(byte[] data, Exchange exchange) {
        TypeConverter converter = exchange.getContext().getTypeConverter();

        String s = converter.convertTo(String.class, data);
        if (s == null || s.length() < 30) {
            throw new IllegalArgumentException("data is invalid");
        }

        s = s.replaceAll("##START##", "");
        s = s.replaceAll("##END##", "");

        String name = s.substring(0, 9).trim();
        String s2 = s.substring(10, 19).trim();
        String s3 = s.substring(20).trim();

        BigDecimal price = new BigDecimal(s2);
        price.setScale(2);

        Integer amount = converter.convertTo(Integer.class, s3);

        PurchaseOrder order = new PurchaseOrder(name, price, amount);
        return order;
    }

}
```
step 2:
declare register file named "META-INF/services/org/apache/camel/TypeConverter"
```
camelinaction//package name to scan converter
```
###camel registry
```
org.apache.camel.spi.Registry
 -org.apache.camel.impl.CompositeRegistry
 -org.apache.camel.spring.spi.ApplicationContextRegistry
 -org.apache.camel.impl.PropertyPlaceholderDelegateRegistry
 -org.apache.camel.core.osgi.OsgiServiceRegistry
 -org.apache.camel.impl.SimpleRegistry
 -org.apache.camel.impl.JndiRegistry
```
###camel use org.apache.camel.component.bean.BeanProcessor to call bean method