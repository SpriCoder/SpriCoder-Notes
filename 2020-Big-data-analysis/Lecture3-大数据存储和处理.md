Lecture3-大数据存储和处理
---

[TOC]

# 1. 常见存储方式
1. 关系型数据库
2. NoSQL:泛指非关系型数据库，比如MongoDB
3. 全文检索框架:Elasticsearch

## 1.1. 存储的区别
1. 行式存储：大数据量查询，如果没有索引，则会遍历
2. 列式存储：可以大量的压缩空间
3. 位图索引

> 位图索引的例子，如下图所示，我们可以存储为
> 1. "男":100101
> 2. "女":011010

| 行号 | 姓名 |
| ---- | ---- |
| 1    | 男   |
| 2    | 女   |
| 3    | 女   |
| 4    | 男   |
| 5    | 女   |
| 6    | 男   |

## 1.2. 不同形式存储的对比
| ID  | name     | age | sex | aihao    |
| --- | -------- | --- | --- | -------- |
| 1   | 小明     | 21  | 男  | 女       |
| 2   | 隔壁老王 | 25  |     | 隔壁孩子 |

1. MySQL形式存储

```sql
1,小明,21,男,女
2,隔壁老王,25, null, 隔壁孩子
```
2. HBase的形式存储:
   1. HBase是一个分布式列式存储系统，记录按**列簇**集中存放，通过主键(row, key)和主键的range来检索数据。
   2. HBase表中每个列都属于某一个列簇
   3. 列簇是表的Schame的一部分，但是列不是，列名都是以列簇作为前缀。

```
<1, name>,小明
<1, age>, 21
...
<2, name>, 隔壁老王
```

3. 传统表中使用Alter子句来修改表结构，而HBase直接插入就可以修改表结构

## 1.3. ES方式
| 文档id | 文档内容                                                      |
| ------ | ------------------------------------------------------------- |
| doc1   | how are you? fine, thank you, and you? I fine too, thank you! |
| doc2   | good morning, LiLei, good morning, Hanmeimei                     |

> 倒排索引示例:ES的存储(倒排索引)的结果如下
> 1. 应该将查询频率高的单词放在前面(越高越前)
> 2. ES默认将文档存储，也可以配置不存储文件信息
> 3. TF-IDF算法：参见[Tec1-TF-IDF算法](Tec1-TF-IDF算法.md)

| dictionary | posting-list    |
| ---------- | --------------- |
| fine       | `->` doc1         |
| Hanmei     | `->` doc2         |
| good       | `->` doc2         |
| LiLei      | `->` doc2         |
| ...        | ...             |
| you        | `->` doc1 `->` doc2 |

## 1.4. 列存储和行存储

|          | 列存储                                       | 行存储                                 |
| -------- | -------------------------------------------- | -------------------------------------- |
| 关注点   | 经常关注一张表某几列而非整表数据的时候       | 关注整张表的内容，或者需要经常更新数据 |
| 计算需要 | 数据表列有非常多行数据并且需要聚集计算的时候 | 不需要聚集运算，或者快速查询需求       |
| 计算方式 | 基于一列或者比较少的列计算的时候             | 需要经常读取某行数据                   |
| 数据形式 | 数据表拥有非常多的列的时候                   | 数据表本身数据行并不多                 |
| 数据特性 | 数据表列有非常多的重复数据，有利于高度压缩   | 数据表的列本身有太多唯一的数据         |

## 1.5. 读写的区别
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/7.png)

## 1.6. 聚簇索引和非聚簇索引
> 物理存储的最小的单位是块(Block)

| 聚集索引            | 非聚集索引          |
| ------------------- | ------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/9.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/8.png) |

## 1.7. MySQL
1. 查询:`Select (tuple) from database`
2. 插入:`Insert into database value`
3. 更新:`Update database set xxx = xxx where statement`
4. 删除:`Delete from database where xxx`

## 1.8. HBase

### 1.8.1. HBase对LSM的实现
> LSM，Log-Structured Merge-Tree，日志结构合并树

1. 假设内存非常大，有限的使用内存存储，结合日志结构实现。
2. 有数据更新不是立马更新，而是先驻留数据，积累到一定条目后归并排序，然后追加到磁盘的队列中，这样子可以显著减少磁盘的开销，一次性大规模写入，减少随机的I/O，不能命中会导致较多的磁盘消耗。

### 1.8.2. HBase的实现
1. 查询
2. 插入
3. 更新&删除:看做一个插入操作，使用时间戳和Delete标识来标识

> memstore:插入时优先放置到memstore，驻存内存，到了一定程度后再刷新到storeFile、插入都是写入操作

## 1.9. ES

### 1.9.1. ES的部分实现方式
1. 一个Node是一个进程
2. 容灾的话就是多副本容灾

### 1.9.2. ES的操作
1. 插入:和HBase相似，不是写入即可查询，建立index需要比较大的开销
2. 读取
3. 更新&删除

## 1.10. 不同存储的容灾方式

| 存储方式     | 结构                                            |
| ------------ | ----------------------------------------------- |
| MySQL        | 单节点，包含数据、日志两个层面的操作            |
| HBase & HDFS | 分布式文件系统，每一个节点操作类似MySQL的单节点 |
| ES           | 各节点备份                                      |

# 2. Hadoop介绍
> Hadoop:一个Apache基金会开发的开源软件框架，支持在由普通计算机组成的集群中运行海量数据的分布式计算，他可以让应用程序轻松扩展到上千个节点和PB级别的数据。

## 2.1. Google 三大论文
1. MapReduce
2. GFS
3. Big Table

## 2.2. Doug Cutting 山寨项目
1. MapReduce
2. HDFS
3. HBase

## 2.3. 大数据处理层次架构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/2.png)


## 2.4. Hadoop核心
1. MapReduce
   1. Map:任务的分解
   2. Reduce:结构的汇总
2. HDFS
   1. NameNode
   2. DataNode
   3. Client

### 2.4.1. MapReduce
1. MapReduce是一种并行编程模型，其实是分治算法的一种实现，适用于大规模数据集的并行计算
   1. map:`(k1,v1)->list(k2,v2)`
   2. reduce:`(k2,list(v2)) -> (k3, v3)`
2. 示例:曹冲称象
3. 过程:`Input -> Map -> Sort -> Combine -> Partition -> Reduce -> Output`

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/1.png)

### 2.4.2. HDFS的基本概念
1. Block
2. NameNode & Secondary NameNode
3. Datanode

### 2.4.3. HDFS架构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/3.png)

#### 2.4.3.1. Block
1. 块大小默认为64M(v1.0)
2. 块大小默认为128M(v2.0)
3. 数据和元数据

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/4.png)

3. 备份
4. 一次写入多次读取

#### 2.4.3.2. NameNode
1. 可以看做是分布式文件系统中的管理者，存储文件系统的metadata，主要负责管理文件系统的命名空间，集群配置信息，存储块的赋值
2. 两个文件：EditLog、FSImage
3. 两个映射：`Filename -> BlockSequence(FsImage)`、`Block -> DatanodeList(BlockReport)`
4. 单点(NameNode)风险

#### 2.4.3.3. Secondary NameNode
1. 不是备用NameNode，而是秘书
2. 合并和保存EditLog、FSImage
   1. Checkpoint.period
   2. Checkpoint.size
  
#### 2.4.3.4. Datanode
文件存储的基本单位。它存储文件块在本地文件系统中，保存了文件块的meta-data，同时周期性的发送所有存在的文件块的报错给Namenode

#### 2.4.3.5. HDFS文件读写
读文件：读取完之后会校验(Check Sum)，未通过则告知错误

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/5.png)

写文件:复制的策略，冗余数据放置在机柜中，跨机柜要经过交换机等设备

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/6.png)

# 3. HBase
1. HBase以谷歌的BigTable为模型，并用Java编写
2. HBase是在HDFS上开发，提供了一种容错的方式存储大量的稀疏数据
3. 一个HBase系统包括一组表，每个表包含行和列，就像传统的数据库一样。每个表都必须有一个定义为主键的元素，所有对HBase表的访问尝试都必须使用这个主键。一个HBase Column表示一个对象属性。

## 3.1. 什么是HBase
1. HBase是一个分布式、非结构化、稀疏、面向列的数据库。
2. HBase是基于HDFS，山寨版的BigTable，继承了可靠性、高性能、可伸缩性

## 3.2. HBase架构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/10.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/11.png)

## 3.3. HBase角色
| 角色 | 内容描述 |
| - | - |
| ZooKeeper | 1. 一个高效的、可扩展的协调系统<br>2. Hadoop的子项目，不属于HBase |
| HMaster |1. 管理网络对Table的增、删、改、查操作<br>2. 管理HRegionServer负载均衡 |
| HRegionServer | 1. 管理一系列HRegion<br>2. Region读写的场所|

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/12.png)

| 角色 | 内容描述 |
| - | - |
| HRegion| 1. 对应Table的Region<br>2. HStore和HLog|
| HStore | 1. 对应了Table中的一个Column Family的存储<br>2. MemStore<br>3. StoreFile(HFile)|
| StoreFile |1. Compact<br>2. Split|

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/13.png)

## 3.4. HBase数据模型
> Table & Column Family
1. RowKey:Table的主键, 记录按照RowKey排序
2. Timestamp:每次数据操作对应的时间戳,可以看作是数据的version number(垃圾清理)
3. Column Family:Table在水平方向由一个或者多个Column Family组成,一个Column Family中可以由任意多个Colum组成

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/14.png)

> Table & Region
1. 记录数不断增多后,Table会逐渐分裂成多份splits,成为regions
2. 一个region由[startkey,endkey)表示
3. 不同的region会被Master分配给相应的RegionServer进行管理.

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/15.png)

1. `.META.`:记录用户表的Region信息,可以有多个regoin
2. `-ROOT-`:记录.META.表的Region信息,只有一个region
3. `Zookeeper`:记录了-ROOT-表的location

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/16.png)

## 3.5. 数据导入
1. Sybase -> HBase
   1. bcp out
   2. importtsv

```sh
hadoop jar ~/hbase-0.92.1/hbase-0.92.1.jar importtsv \
-Dimporttsv.separator= "," # 指定输入文件的分隔符为;\
-Dimporttsv.bulk.output=/output # 输出hfile到/output
-Dimporttsv.columns=HBASE ROW KEY,cf1:USER NAME
#源文件的第一列为rowkey ，第二列为cf1:USER NAME\
users /bulkload/users.txt #导 入hbase的users表中,输 入文件在/bulkload\
hadoop jar ~/hbase-0.92. 1/hbase-0.92.1.jar completebulkload/output users
```

## 3.6. 访问接口
1. Hadoop & HBase提供JAVA接口
2. Thrift支持多语言访问HBase，C++、C#、Cocoa、Erlang、Haskell、Java、Ocami、Perl、PHP、Python、Ruby、Smalltalk

# 4. Hive
1. Hive是基于Hadoop的数据仓库工具，提供完整的SQL查询功能，可以将结构化的数据文件映射为一张数据库表。
   1. 可以将SQL语句转换为MapReduce任务进行运行。
   2. 可以通过类SQL语句快速实现简单的MapReduce统计，不必开发专门的MapReduce应用
2. 学习成本低

## 4.1. Hive体系结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec3/19.png)

## 4.2. Hive运维要点
> Hive相当于一套Hadoop的访问接口，运维如下几个问题需要注意

1. 使用单独的数据库存储元数据
2. 定义合理的表分区和键
3. 设置合理的bucket数据量
4. 进行表压缩
5. 定义外部表使用规范
6. 合理的控制Mapper，Reducer数量

# 5. Pig
> Apache Pig架构

1. 严格用于使用Pig分析Hadoop中的数据的语言称为Pig Latin是一种高级数据处理语言。它提供了一组丰富的数据类型和操作符来对数据执行各种操作。
2. 要执行特定任务时，程序员使用Pig，需要用Pig Latin语言编写Pig脚本,并使用任何执行机制( Grunt Shell，UDFs，Embedded )执行它们。执行后,这些脚本将通过应用Pig框架的一系列转换来生成所需的输出。
3. 在内部, Apache Pig将这些脚本转换为一系列MapReduce作业,因此,它使程序员的工作变得容易。

## 5.1. Pig组成组成

1. Parser (解析器)：最初, Pig脚本由解析器处理,它检查脚本的语法,类型检查和其他杂项检查。解析器的输出将是DAG(有向无环图),它表示Pig Latin语句和逻辑运算符。在DAG中,脚本的逻辑运算符表示为节点,数据流表示为边。
2. Optimizer (优化器)：逻辑计划(DAG)传递到逻辑优化器,逻辑优化器执行逻辑优化,例如投影和下推。
3. Compiler (编译器)：编译器将优化的逻辑计划编译为一系列MapReduce作业。
4. Execution engine (执行引擎)：最后,MapReduce作业以排序顺序提交到Hadoop。这些MapReduce作业在Hadoop上执行,产生所需的结果。

## 5.2. Pig与SQL区别
1. 使用延迟评价、使用ETL、能够在管道中任何时刻存储数据、支持管道分裂
2. Pig Latin是程序性的,它在管道范例中非常自然,而SQL则是声明性的。在SQL用户中,可以指定要连接两个表的数据,但不能指定要使用的连接实现。
3. Pig Latin允许用户指定一个实现或实现的各个方面 ,以在多个方面执行脚本。Pig Latin编程类似于 指定查询执行计划。

# 6. 参考
1. <a href = "https://blog.csdn.net/qq_41848129/article/details/99720517">HBase存储方式</a>