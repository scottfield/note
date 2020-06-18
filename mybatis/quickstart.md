###do a fuzzy search query
```xml
<select id="selectName"
          resultType="your result type">
<bind name="pattern" value="'%' + _parameter.get('paramName') + '%'" />
select * from tableName where fieldName like #{pattern}
</select>
```