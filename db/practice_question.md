# 实践遇到的问题

### 隐式类型转换
 > 发生情况
 - 一般发生在字段查询时没有加引号或使用的查询条件与字段类型不一致导致查询时存在隐式类型转换
 ```sql
#mobile是varchar类型字段,而且是索引字段

sql1: explain select * from table where mobile=18812341234
sql2: explain select * from table where mobile='18812341234'
#对于sql1 mysql会将转隐式换成字符串
#如上两条SQL查询效率是不一样的
#sql1 没有使用索用,全表扫描
#sql2 使用了索用

```
 > 原理
  - 系统内部检测到查询的类型与字段类型不一样会将转换成字段类型
  
 > 如何避免
  - 写查询条件时一定要与字段类型相一致