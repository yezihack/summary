# mysql 设计原则

#### 明确业务功能是什么?

- 事物性质
 >在这类程序中，你的终端用户更多操作的是CURD。比如：创建、读取、更新和删除表中的记录。这种数据库的比较官方说法是 OLTP (Transactional)
 
- 分析性质
 > 在这类程序中，你的终端用户更多操作的是分析、报告、预报等。这类数据库的插入和查询操作很少。更快的查询和分析数据是首要考虑的问题。这种数据库的比较官方说法是 OLAP (Analytical)
 
 
 #### 数据库规范化需要注意
 
 > 数据冗余
  - 尽可能少地冗余,减少到最少.不仅节省物理空间,更重要的是保持数据一致性.
  
 > 数据混乱
  - 避免insert,update,delete操作导致数据混乱
  
  
 #### 3大范式定义
 
 
 > 第一范式 1NF(normal form)
  - 符合1NF的关系中每一个属性(字段)不可再分隔
  - 确保每一个字段的原子性.
  
 > 第二范式 2NF
  - 所有的属性必须完全依赖于所有主键,绝不允许依赖于部分主键,尤其出现双主键
  - 必须存在主键,才能找到某一行数据
  - 其它属性依赖主键,不相干的属性不允许存在
  
 > 第三范式 3NF
  - 一个表中不包含已在其它表中已包含的非主键信息
  - 消除传递依赖(相当于消除冗余属性)
  - 非主键外的所有字段必须互不依赖
  - 重点是消除冗余,避免数据冗余不同表中
  - 一般设计中会出现反三范式情况(性能是关键的话，就不用太关注去避免冗余)


### 导航
- [目录](../README.md)