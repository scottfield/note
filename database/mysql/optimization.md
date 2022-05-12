###关联优化
默认查询优化器会自动评估怎样的关联顺序是最优的，可以在查询时添加STRAIGHT_JOIN关键字来强制使用指定
的关联顺序。
```
SELECT * from tbl1 STRAIGHT_JOIN tbl2 on tbl1.id=tbl2.fk_id
```
