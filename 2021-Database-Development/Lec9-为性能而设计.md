Lec9-为性能而设计
---

# 1. 为性能而设计

## 1.1. 数据的关系视图
1. 数据库只是对现实世界的有限描述。对特定的业务活动的描述不止一种
2. "关系模型"中的"关系"的含义
3. 关系模型的一致性
   1. 只要遵守关系理论，可以保证基于数据库的任何查询结果与原始数据具有同样的有效
   2. 关系理论包括
      1. 关系不包含重复数据
      2. 关系理论保证无限数据的正确性
      3. 记录之间没有顺序

## 1.2. 规范化（Normailization）
1. 表结构没有规范化会面临很大的风险吗？
   1. 1NF 确保原子性（Atomicity）
   2. 2NF 检查对键的完全依赖
   3. 3NF 检查属性的独立性
2. 过分精益求精会使精力分散
3. 规范化的价值
   1. 合理规范化的模型可应对需求变更
   2. 规范化数据重复降至最少

## 1.3. 有值、无值、空值
1. 表中的每一条记录都应该是特定"事物"的状态描述，如果大部分特征信息都显示"我们不知道"，无疑大大降低了信息可信性
2. 存在空值意味着关系模型存在严重的问题，动摇了查询优化的基础
3. 空值对程序逻辑是危险的
   1. 必须使用空值的话，一定要清楚它在特定情况下的影响。

## 1.4. 限用Boolean型字段
1. SQL中并不存在Boolean类型
2. 实现flag表示标志位的Y/N或T/F
   1. 例如：order_completed
   2. 但是…往往增加信息字段能包含更多的信息量
   3. 例如：completion_date completion_by
   4. 或者增加order更多状态标示
3. 极端的例子：四个属性取值都是T/F，可以用0-15这16个数值代表四个属性所有组合状态
   1. 技巧可能违反了原子性的原则
   2. 为数据而数据，是通向灾难之路

## 1.5. 理解子类型（SubType）
1. 表过"宽"（有太多属性）的另一个原因，是对数据项之间的关系了解不够深入，窄表的效率相对比较高
2. 一般情况下，给子类型表指定完全独立于父表主键的主键，是极其错误的

## 1.6. 约束应明确说明
1. 数据中存在隐含约束是一种不良设计
2. 字段的性质随着环境变化而变化时设计的错误和不稳定性
3. 数据语义属于DBMS，别放到应用程序中

```sql
/* × */
configuration(parameter_name, parameter_value)
/* √ */
configuration(parameter_id, parameter_name, parameter_type)
  configuration_numeric (parameter_id, parameter_value)
```

## 1.7. 过于灵活的危险性
1. "真理向前跨一步就是谬误"
2. 不可思议的四**通用表**设计
   1. Objects(oid, name), Attributes(attrid, attrname,type)
   2. Object_Attributes(oid,attrid,value)
   3. Link(oid1,oid2)
3. 随意增加属性，避免NULL
4. 成本急剧上升，性能令人失望
5. 基于规则的优化器：笛卡尔积往往是最消耗性能的。
6. 目前是基于成本的优化器，大量的性能消耗也使得关系数据库出现问题

## 1.8. 如何处理历史数据
1. 历史数据：例如：商品在某一时刻的价格
2. Price_history(article_id , effective_from_date , price)
3. 缺点在于查询当前价格比较笨拙
4. 设置为价格终止时间呢？

```sql
select a.article_name, h.price
from articles a,
  price_history h
where a.article_name = some_name
  and h.article_id = a.article_id
  and h.effective_from_date =
    (select max(b.effective_from_date)
      from price_history b
      where b.article_id = h.article_id)
```

```sql
select a.article_name, h.price
  from articles a,
    price_history h
  where a.article_name = some_name
    and h.article_id = a.article_id
    and h.effective_from_date =
      (select max(b.effective_from_date)
        from price_history b
        where b.article_id = h.article_id
          and b.effective_from_date <= sysdate)
```

## 1.9. 处理流程
1. 操作模式（operating mode）
   1. 异步模式处理（批处理）
   2. 同步模式处理（实时交易）
2. 处理数据的方式会影响我们物理结构的设计
3. 清算：部分锁表进行清算
4. 任何一个系统要将批处理和实时处理分开

## 1.10. 数据集中化（Centralizing）
1. 分布式数据系统复杂性大大增加
   1. 远程数据的透明引用访问代价很高
   2. 不同数据源数据结合极为困难
      1. Copy的数据传输开销
      2. 无法从数据规划中获益（物理结构，索引）
2. 数据库该如何部署呢？中庸、分析、决策
3. 离数据越近，访问速度越快

## 1.11. 系统复杂性
1. 数据库的错误很多
   1. 硬件故障
   2. 错误操作…
2. 数据恢复往往是RD和DBA争论焦点
   1. DBA，即便确保数据库本身工作正常，依然无法了解数据是否正确
   2. RD，在数据库恢复后进行所有的功能性的检查
3. 高性能数据库一般不使用防御式编程，而做进攻性编程

# 2. 小结
1. 错误的设计是导致灾难性后果的源泉
2. 解决设计问题会浪费惊人的精力和智慧
3. 性能问题非常普遍
4. 打着"改善性能"的旗号进行非规范化处理，常常使性能问题变得更糟
5. 成果的数据建模和数据操作应严格遵循基本的设计原则。