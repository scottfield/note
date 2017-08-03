#JDBC读取数据库元数据信息
##读取数据库中所有的表
```
DatabaseMetaData metaData = connection.getMetaData();
ResultSet resultSet = metaData.getTables("", "jackie_dw", "%", new String[]{"TABLE"});
List<String> tableNames = new ArrayList<>();
while(resultSet.next()){
    tableNames.add(resultSet.getString("table_name"));
}
```
##读取数据库中表的列信息
```
ResultSet tableColumns = metaData.getColumns(catalog, schemaPattern, tableName, "%");
List<String> columnNames = new ArrayList<>();
while(tableColumns.next()){
    columnNames.add(tableColumns.getString("column_name"));
}
```