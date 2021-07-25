Lecture10-Graph DB
---

[TOC]

# 1. NoSQL-No SQL or Not Only SQL

## 1.1. NoSQL- Comes in many different variants
> 一些可能的特性可能不支持所有特性

1. 非关系
2. 灵活的架构
3. SQL以外的其他查询语言
4. 分布式水平缩放
5. 较少的结构化数据
6. 支持大数据

## 1.2. NoSQL的优点
> 与关系数据库相比，NoSQL数据库具有更高的可伸缩性和更高的性能，并且它们的数据模型解决了关系模型无法解决的几个问题：
1. 地理分布的架构，而不是昂贵的整体架构
2. 大量快速变化的结构化，半结构化和非结构化数据
3. 敏捷的冲刺，快速的模式迭代和频繁的代码推送
4. 易于使用且灵活的面向对象编程

## 1.3. 规模
> 数据库扩展
1. RDBMS可以通过添加硬件处理能力来扩容
2. NoSQL可以通过负载均衡来，分区(分片)/复制

## 1.4. NoSQL数据库类型
1. 图形存储用于存储有关数据网络的信息，例如社交关系。Graph商店包括Neo4J和Fuseki等三重商店。
2. 文档数据库将每个密钥与称为文档的复杂数据结构配对。
3. **键值存储是最简单的NoSQL数据库**。数据库中的每一项都与属性值一起存储为属性名称(或"键")。键值存储的示例有Riak和Berkeley DB。
4. Cassandra和HBase之类的宽列存储针对大型数据集的查询进行了优化，并将数据列而不是行存储在一起。

## 1.5. 文档存储
1. 中心概念是"文档"的概念，它对应于RDBMS中的一行。
2. 文档采用某些标准格式，例如JSON(BSON)。
3. 通过代表该文档的唯一密钥在数据库中寻址文档。
4. 数据库提供了一种API或查询语言，可根据其内容检索文档。
5. 文档是无架构的，即不同的文档可以具有彼此不同的结构和架构。(RDBMS要求每一行包含相同的列。)

## 1.6. MongoDB存储文档(JSON)
```
{
  _id: ObjectId("51156a1e056d6f966f268f81"),
  type: "Article",
  author: "Derick Rethans",
  title: "Introduction to Document Databases with MongoDB",
  date: ISODate("2013-04-24T16:26:31.911Z"),
  body: "This arti…"
},
{
  _id: ObjectId("51156a1e056d6f966f268f82"),
  type: "Book",
  author: "Derick Rethans",
  title: "php|architect's Guide to Date and Time Programming with PHP",
  isbn: "978-0-9738621-5-7"
}
```

## 1.7. 最热门的NoSQL数据库
1. Grace联合创始人Vadim Ismakaev 2015年4月27日更新
2. 问"什么是NoSQL最流行的数据库"有点不正确，因为不同的问题需要不同类型的NoSQL解决方案。
3. 专注于解决非常具体的问题。虽然这可以在那些特定情况下实现最佳结果，但要付出其他一些功能的代价。

## 1.8. 什么是最热门的NoSQL数据库
> 评价一个系统是否热门的一些参数
1. 网站上提及该系统的次数
2. 对系统的普遍兴趣：对于此度量，我们使用Google趋势中的搜索频率。
3. 关于系统的技术讨论频率(Stack Overflow)
4. 提及系统的工作机会数量
5. 提到系统的专业网络中的个人资料数量 
6. 社交网络中的相关性：我们计算提到该系统的Twitter推文的数量

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/1.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/2.png) |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/3.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/4.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/5.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/6.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/7.png) |                      |

## 1.9. 图数据模型
1. 图的概念
   1. G=(V，E)，V为顶点的集合，E为边的集合
   2. 有向图：边有方向
   3. 无向图：边没有方向(可以用有向图表达无向图：每条无向边->2条有向边)
2. 图数据存储系统:
   1. 存储图顶点和边，提供顶点和边的查询
   2. 一个数据库，该数据库使用图结构进行语义查询，并使用节点，边和属性来表示和存储数据，而与内部存储数据的方式无关。 真正重要的是模型和实现的算法。

# 2. Neo4j

## 2.1. 什么是Neo4j
1. Neo4j是由Neo Technologies开发的最受欢迎的图形数据库，其是用Java实现的开源，面向图的数据库
2. 以Java实施，可通过交换HTTP端点使用Cypher查询语言从其他语言编写的软件中访问。
3. 符合**ACID**的**事务**数据库，具有**本机图存储和处理功能**。
4. 一切都存储为边，节点或属性。
   1. 每个节点和边缘可以具有任意数量的属性。
   2. 节点和边均可标记。
   3. 标签可用于缩小搜索范围。

## 2.2. 图数据库
1. 数据库使用带有节点，边和属性的图结构来存储数据
2. 提供无索引的邻接：每个节点都是指向其相邻元素的指针
3. 边缘可容纳大多数重要信息并进行连接
   1. 节点到其他节点
   2. 属性的节点

## 2.3. Neo4j数据存储
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/8.png)

## 2.4. Neo4j数据读写
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/9.png)

## 2.5. 图属性模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/10.png)

## 2.6. 图数据库优点
1. 当存在要分析的关系时，由于数据结构，Graph数据库变得非常合适
2. 图形数据库对于关联数据集非常快，就像社交网络
3. 更直接地映射到面向对象的应用程序，对象分类和父级->子级关系

## 2.7. 图数据库缺点
1. 如果数据只是表格格式，数据之间的关系不多，则图数据库的运行状况不佳
2. 对图数据库的OLAP(联机处理分析)支持不够完善，该领域有大量的人在研究。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/11.png)

## 2.8. Neo4j的显著特点
1. Neo4j不含架构：数据不必遵循任何约定
2. ACID：原子的，一致的，隔离的和持久的逻辑工作单元
3. 易于上手和使用
4. 资料丰富的大型开发者社区
5. 支持多种语言：Java，Python，Perl，Scala，Cypher等

> Neo4j 逻辑结构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/12.png)

## 2.9. Cypher(了解即可)
1. Neo4j的查询语言
2. 易于根据关系制定查询
3. 许多功能源于使用SQL改善痛点，例如连接表

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/13.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/14.png) |
| --------------------- | --------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/15.png) |                       |

## 2.10. 结论
1. 问自己的关键问题
   1. 我的数据会有很多关系吗？
   2. 我想问我的数据库什么样的问题？
2. Neo4j是一个很棒的图形数据库

# 3. 图数据库比较

## 3.1. 数据存储特征
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/16.png)

## 3.2. 操作特征
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/17.png)

## 3.3. 图数据结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/18.png)

## 3.4. 模式和实例表示
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/19.png)

## 3.5. 查询特征
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/20.png)

## 3.6. 完整性约束
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/21.png)

## 3.7. 对于潜在图查询的支持
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec10/22.png)


## 3.8. 总结
1. 图数据库模型的整体均衡
2. 数据结构:
   1. 很多种图结构类型
   2. 可以很好的表示数据模型
3. 查询特征
   1. 限制提供API
   2. 很好的对于潜在图查询操作的支持
   3. 缺少图查询语言
4. 完整性约束
   1. 约束的观念
   2. 面向无架构