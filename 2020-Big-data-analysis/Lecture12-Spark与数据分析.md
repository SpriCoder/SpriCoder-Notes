lecture12-Spark与数据分析
---

[TOC]

# 1. 复习
1. MapReduce
   1. 轻松编写应用程序，以可靠，容错的方式在大型集群上并行处理大量数据
   2. 负责安排任务，监视任务并重新执行失败的任务
2. HDFS和MapReduce：在同一组节点上运行`->`计算节点和存储节点相同(使数据接近计算)`->`高吞吐量
3. YARN&MapReduce：一个主资源管理器，每个节点一个从属节点管理器，每个应用程序一个AppMaster

# 2. 数据处理的目标
1. **低延迟(交互式)历史数据查询**：做出更快的决策，例如，确定网站运行缓慢的原因并进行修复。
2. **对实时数据(流)的低延迟查询**：启用对实时数据的决策，例如，实时检测和阻止蠕虫(蠕虫可能在1.3秒内感染100万台主机)。
3. **先进的数据处理**：实现"更好"的决策，例如，异常检测，趋势分析。

# 3. 现在的开源分析框架
1. 主要针对大型磁盘数据集：非常适合批处理，但速度较慢

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/1.png)

# 4. 目标
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/2.png)

1. 易于组合批处理，流式处理和交互式计算
2. 易于开发复杂的算法
3. 与现有开源生态系统(Hadoop/HDFS)兼容

# 5. 支持互动和流媒体压缩

## 5.1. 积极使用内存
1. 为什么？内存传输率远远快于磁盘或SSD，许多数据集的大小已经适合内存
   1. Facebook，Yahoo！和Bing群集中超过90％的工作输入适合内存
   2. 例如1TB = 10亿条记录，每个记录大小为1KB
2. 内存密度(仍)随摩尔定律增长：即将推出的RAM/SSD混合存储器

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/3.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/5.png) |
| ------------------- | ------------------- |

## 5.2. 增加并行度
1. 为什么？减少每个节点的工作量 -> 改善延时
2. 技术：
   1. 实现高局部性的低延迟并行调度程序
   2. 优化的并行通信模式(例如，随机播放，广播)
   3. 从故障和缓解混乱中有效恢复

## 5.3. 在**结果准确性**和**响应时间**之间进行权衡
1. 为什么？内存中处理不能保证交互式查询处理
   1. 例如，内存仅10秒就可以扫描512 GB RAM！
   2. 内存容量与传输速率之间的差距增大
2. 挑战：准确估算错误和运行时间，以任意计算

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/6.png)

# 6. Berkeley Data Analytics Stacks(BDAS)，伯克利数据分析堆栈
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/7.png)

## 6.1. 伯克利AMP实验室
1. 2011年1月"启动"：6年计划，由8名计算机职工，大约40名学生，3名软件工程师组成，组织协作如下图

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/8.png)

2. 资助:DARPA：数据，NSF：补助金
3. 工业，创始赞助商
4. 其他18个赞助商，包括

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/9.png)

5. 目标：面向工业和研究的下一代分析数据堆栈：
   1. 伯克利数据分析堆栈(BDAS)
   2. 发布为开源

# 7. Hadoop和Spark的历史
> 谷歌的三家马车

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/10.png)

## 7.1. Apache的Hadoop和Spark
> Spark可以不抛弃HDFS，只需要在其基础上添加一个YARN来完成操作。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/11.png)

## 7.2. Apache Spark
> Spark可以连接到多种类型的集群管理器(Spark自己的独立集群管理器，Mesos或YARN)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/12.png)

## 7.3. Apache Hadoop:没有统一的愿景
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/13.png)

1. 稀疏模块
2. API的多样性
3. 更高的运营成本

## 7.4. Spark生态:统一的管道
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/14.png)

## 7.5. Spark 和 MapReduce：数据流
> 将下面的三个部分合并，省略了多次的HDFS read和HDFS write的时间

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/15.png)

## 7.6. 数据访问率
1. 在节点中：
   1. CPU至内存：10 GB /秒
   2. CPU到硬盘：0.1 GB /秒
   3. CPU到SSD：0.6 GB /秒
2. 网络之间的节点：0.125 GB /秒至1 GB /秒
3. 同一机架中的节点：0.125 GB /秒至1 GB /秒
4. 机架之间的节点：0.1 GB /秒

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/16.png)

## 7.7. Spark:高表现和简单的数据流
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/17.png)

# 8. 性能表现：Spark 和 MapReduce
1. 迭代算法
   1. Spark更快，简化了数据流
   2. 避免在每次迭代后在HDFS上实现数据
2. 示例：k均值算法，1次迭代
   1. HDFS读取
   2. 映射(将样本分配给最接近的质心)
   3. GroupBy(Centroid_ID)
   4. 网络随机轮转
   5. 减少(计算新质心)
   6. HDFS写

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/18.png)

3. 简单/更少代码
4. 多阶段 `->` Pipeline
5. 运营
   1. 转换：将用户代码应用于并行分发数据
   2. 动作：组装最终输出分布式数据

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/19.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/20.png)

## 8.1. 驱动

### 8.1.1. MapReduce：Hadoop生态系统的原始可扩展通用处理引擎
1. **基于磁盘的数据处理框架(HDFS文件)**
2. 将中间结果持久化到磁盘
3. 每次查询都会从磁盘重新加载数据->成本很高的I/O
4. 最适合ETL之类的工作负载(批处理)
5. **昂贵的I/O`->`不适合迭代或流处理工作量**

### 8.1.2. Spark：通用计算框架，可大幅提高MapReduce的性能，并保留基本模型
1. 基于内存的数据处理框架`->`通过将中间结果保留在内存中避免了昂贵的I/O
2. 利用分布式内存，记录应用于数据集的操作
3. 基于数据局部性的计算->高性能
4. 最适合迭代(或流处理)和批处理工作负载

### 8.1.3. 总结
1. 软件工程观点
   1. Hadoop代码量巨大
   2. 对Hadoop的贡献/扩展很繁琐
   3. 仅Java妨碍广泛采用，但Java支持是基础
2. 系统/框架的观点
   1. 统一管道
   2. 简化的数据流
   3. 更快的处理速度
3. 数据抽象的观点
   1. 新的基础抽象RDD
   2. 易于扩展新的运营商
   3. 更具描述性的计算模型

## 8.2. 简单的历史
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/21.png)

### 8.2.1. MapReduce的历史
1. 大约1979年–斯坦福大学，麻省理工学院，CMU等，在LISP，Prolog等中设置/列出操作，以进行并行处理
2. 2004年左右– Google，MapReduce：简化大型集群上的数据处理
3. 大约在2006年– Apache，Hadoop，源自Nutch项目
4. 大约2008年–雅虎，网络规模搜索索引
5. 大约2009年– AmazonAWS，弹性MapReduce，Hadoop修改为EC2/S3，并支持Hive，Pig，Cascading等。
6. 公开讨论：列举自2002年以来数据中心技术的几项变化

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/22.png)

- MapReduce用例显示出两个主要限制：
  - 很难直接在MR中编程
  - 性能瓶颈，或批量不适合使用情况
- 简而言之，MR不适用于大型应用
- 因此，人们建立了专门的系统作为解决方法……

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/23.png)

### 8.2.2. Spark
1. Spark:具有工作集的集群运算
2. 用于内存中的集群运算的容错抽象
3. 与各种专用系统不同，Spark的目标是推广MapReduce以在同一引擎中支持新应用
4. 两个相当小的添加就足以表示以前的模型：
   1. 快速数据共享
   2. 常规DAG
5. 这允许一种对引擎更有效，对最终用户更简单的方法

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/24.png)

6. 关于Spark的一些关键点：
   1. 在单个框架内处理批处理，交互式和实时
   2. 与Java，Python，Scala的本机集成
   3. 更高抽象级别的编程
   4. 更笼统：map / reduce只是一组受支持的构造

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/25.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/26.png)

# 9. 为什么会选择Spark(重要)
1. Apache Spark是一个开放源代码集群计算框架，最初是在加利福尼亚大学伯克利分校的AMPLab中开发的，但后来捐赠给了Apache软件基金会，至今仍在使用。与Hadoop的基于磁盘的分析范例相反，Spark具有多阶段内存中分析。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/27.png)

1. 速度快：相同的任务、硬件设备上，在内存中，Spark要比Hadoop快100倍，在硬盘中，Spark要比Hadoop快10倍左右。因为是基于内存的，Spark提出了数据内存抽象，RDD允许用户在查询过程中将集合存放在内存中。
2. 使用方便：可以很快的使用Java、Scala、Python和R进行开发。
3. 通用性：集合了SQL、Streaming和复杂的分析。

## 9.1. MapReduce和Spark
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/28.png)

## 9.2. Spark生态系统
> RDD：resilient distributed datasets，弹性分布式数据集

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/29.png)

1. RDD(弹性分布式数据集)是Spark中的主要逻辑数据单元。RDD是对象的**分布式集合**。分布式方式，每个RDD分为多个**分区**。这些分区中的每个分区都可以驻留在内存中或存储在群集中不同计算机的磁盘上。RDD是**不可变的(只读)数据结构**。您无法更改原始RDD，但可以随时将其更改为具有所有所需更改的RDD。
2. 在Spark中，所有工作都表示为
   1. 创建新的RDD
   2. 转换现有的RDD
   3. 对RDD调用操作以计算结果
3. 转换按需执行。这意味着它们是惰性计算的。 例如：过滤，加入，排序
4. 动作将返回RDD计算的最终结果。 Actions使用沿袭图触发执行，以将数据加载到原始RDD中，执行所有中间转换并将最终结果返回到Driver程序或将其写到文件系统中。 例如：collect()，count()，take()

# 10. Spark工作流(重要)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/30.png)

1. Spark应用程序在群集上作为独立的进程集运行，由主程序(称为驱动程序)中的SparkContext对象协调。
2. 要求集群管理器在各个应用程序之间分配资源。
3. 连接后，Spark会在集群中的节点上获取执行程序，这些节点是运行计算并为您的应用程序存储数据的进程。
4. 接下来，它将您的应用程序代码(由传递给SparkContext的JAR或Python文件定义)发送给执行者。最后，SparkContext将任务发送给执行程序以运行。

## 10.1. 概述
1. Apache spark是一个应用于大规模数据处理的快速通用引擎
   1. **快**：基于内存的MapReduce计算比Hadoop快100x倍，基于硬盘的则快10x倍
   2. **易用**：支持Scala、Java、Python和R语言开发
   3. **功能强**：Spark SQL、Spark Streaming、Spark GraphX、Spark MLlib
2. 更加通用
   1. 适用于多种不同的集群管理框架：Standalone cluster mode、Apache Mesos、Hadoop YARN、in the Cloud(EC2)
   2. 适用于多种不同的数据存储方式：数据读取接口：HDFS、HBase、MongoDB、Cassendra

## 10.2. 功能
1. Spark SQL
   1. 前身是Shark，基于Hive的Spark SQL，代码量大、复杂，难优化和维护
   2. 交互式查询、标准访问接口、兼容Hive
   3. 专门用于处理结构化数据：分布式SQL引擎；在Spark 程序中调用API
2. Spark Streaming：实时对**大量数据进行快速处理**，处理周期短
3. Spark GraphX：**以图为基础**数据结构的算法实现和相关应用
4. Spark MLlib：为解决**机器学习**开发的库，包括分类、回归、聚类和协同过滤等

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/34.png)

## 10.3. 集群管理框架
1. Standalone mode：独立集群管理功能：任务调度、资源分配等
2. Apache Mesos：从分布式计算节点上抽象CPU, memory, storage, and other compute resources给其他框架使用，实现了静态资源分配功能
3. Hadoop Yarn：Hadoop MapReduce的第二个版本架构，把资源管理和任务管理剥离开；实现了静态资源分配和动态资源分配功能；
4. EC2：Amazon EC2云平台，提供一个安装了Spark、Shark 和HDFS的集群，可直接登录到集群，把它当作你实验室的集群使用

## 10.4. 集群管理框架图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/31.png)

## 10.5. 存储方式
1. HDFS:Hadoop分布式文件系统
2. HBase：基于HDFS的非关系型数据库(NoSQL数据库)
3. MongoDB：
   1. 基于分布式存储的数据库，介于关系型和非关系型数据库之间
   2. 是NoSQL数据库中最像关系型数据库的一个
   3. 功能非常强大：支持多种开发语言、支持完全索引、支持查询等
4. Cassendra：基于列的分布式数据库，易扩展、模式灵活、按照范围查询等
5. 它们和Spark的关系：Spark是一个计算程序，需要读取数据和存储数据，它们就是数据存储的地方

## 10.6. Spark生态系统
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/32.png)

# 11. 实践目标

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/33.png)

## 11.1. 系统搭建
1. 安装HDFS
   1. <a href = "http://hadoop.apache.org/releases.html">下载Hadoop</a>
   2. <a href = "http://hadoop.apache.org/docs/r3.0.0-alpha4/hadoop- project-dist/hadoop-common/ClusterSetup.html">配 置 Hadoop 集 群</a> 
2. 安装Spark
   1. <a href= "http://spark.apache.org/downloads.html">下载Spark</a>
   2. <a href = "http://spark.apache.org/docs/latest/spark-standalone.html">配置Spark Standalone集群</a>
3. 安装MongoDB
   1. <a href = "https://www.mongodb.com/download- center?jmp=nav#community">下载MongoDB</a>
   2. <a href = "https://www.mongodb.com/products/spark-connector">下载Mongo Spark Connector</a>
4. 确定物理机并安装操作系统(推荐Redhat)
5. 如果没有网络要事先下载所有安装包
6. 设置SSH无密码登陆
7. 安装JDK、Scala

## 11.2. 利用Spark处理数据
1. 理解Spark原理
   1. 开发Spark程序：开发环境、程序提交、运行模式
   2. 内核讲解：RDD
   3. 工作机制：任务调度、资源分配
2. 使用Spark
   1. Spark读取、存储HDFS、MongoDB
   2. Spark Streaming
   3. Spark GraphX
   4. Spark MLlib

# 12. Spark原理

## 12.1. Spark提交应用程序
```
./bin/spark-submit \
   --class <main-class> \
   --master <master-url> \
   --deploy-mode <deploy-mode> \
   --conf <key>=<value> \
   ...
   <application-jar> \
   [application-arguments]
```
1. main-class:main方法所在的类的路径
2. master-url:集群管理器的地址
3. deploy-mode:应用程序部署的模式，是交互式还是集群式
4. Key=value:Spark的配置参数与值
5. application-jar:应用程序打包后

## 12.2. Driver程序
1. 应用执行过程：Spark应用的入口程序：Driver，在**集群模式**下用户开发的Spark程序称为Driver
2. 应用的执行位置
   1. Local
   2. 集群
3. 应用的部署模式
   1. 集群模式：如果在远离(网络远离)计算节点的本地机器上提交Spark程序到集群内部执行，称为集群模式，当程序提交后，本地机器就结束了和集群的交互，程序的运行结果也不会返回到本地，只保存在集群内部。
   2. 客户端模式：如果在靠近计算节点的机器上执行(Master或者就是Worker)程序，可以选择客户端模式，就是通过Spark 提供的Shell执行，程序会和集群产生持续的通信，集群的任务执行完成后，会把执行结果返回到客户端。

## 12.3. SparkContext
1. SparkContext对象
   1. 使得应用程序能够和集群进行沟通，实现CPU、内存等资源的分配
   2. 每个Driver程序都有一个SC对象
   3. 如果是交互式编程，则Spark Shell会自动创建一个SC对象
   4. 程序启动后，SC会告诉集群管理器在Worker Node上创建执行器，执行器是每一个Spark程序在计算节点上专属的进程
   1. 程序代码会发送到对应的Worker Node上
   2. SC分发任务(Task)到各个执行器

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/35.png)

## 12.4. 其他相关名词
1. Application：独立的Spark程序
2. Master(Cluster Manager)，Worker
3. 执行器(Executor)：Spark程序在对应计算节点上启动的专属线程，负责执行Task
4. Job：一次RDD Action称为一个Job，是一个概念
5. Stage：介于Job和Task之间，是一个Task集合
6. Task：在执行器上执行的最小单元，例如在某个计算节点对一个RDD的分区进行的Transformation操作

## 12.5. 具体执行过程
1. 分为两部分
   1. Driver程序
      1. 客户端模式下，Driver在本地，不会把Driver提交给Master，而直接提交任务
      2. 集群模式下，首先Driver被提交给Master，Master首先找一个Worker运行Driver
   2. 集群节点
2. 执行器启动后运行Driver程序的节点不需要和管理器有太多交互，而与worker间交互密切，因此Driver程序应该放在距离
Worker节点较近的地方。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/36.png)

### 12.5.1. 详细的应用执行过程展示
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/37.png)

- <a href = "https://blog.csdn.net/thomas0yang/article/details/50352261">Spark任务处理流程</a>

### 12.5.2. 结合源代码分析的Spark执行过程解读
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/38.png)

- <a href = "https://blog.csdn.net/u011007180/article/details/52388783">源码-spark运行流程分析</a>
- <a href = "https://blog.csdn.net/zero__007/article/details/53121003">Spark运行流程源码走读</a>

## 12.6. RDD
1. Job、Task、DAGScheduler的定义均依赖RDD
2. Resilient Distributed Dataset 弹性分布式数据集
3. 是Spark的核心数据结构
   1. 是一个数据集，就像Array、List和Set等一样的数据结构
   2. 内容是平铺的，可以顺序遍历，像Array和List一样
   3. RDD是分布式存储的，支持并行计算
   4. RDD的分布是弹性的，某些操作使不同的数据块重新汇聚和分布
   5. RDD是只读的
   6. RDD可以缓存在内存中
   7. RDD可以通过重复计算获得(实现高可靠性)
4. RDD定义：包含5个属性
   1. 分区列表：记录了数据块所在的分区位置；一个RDD对应的数据是切分为数据块存储在集群的不同节点上的，`@transient def getPartitions_ : Array[Partition] = null`
   2. 依赖列表：记录了当前这个RDD依赖于哪些其它的RDD，`private var dependencies_ : Seq[Dependency[_]] = null`
   3. 计算函数compute，用于计算RDD各个分区的值`def compute(split: Partition, context: TaskContext): Iterator[T]`
   4. 可选：分区器，子类可以重新指定新的分区方式：Hash 和Range,`@transient val partitioner: Option[Partitioner] = None`
   5. 可选：计算各分区时优先的位置列表
      1. 例如从HDFS文件生成RDD时，HDFS文件所在位置就是对应生成的RDD分区所在位置的优先选择
      2. `protected def getPreferredLocations(split: Partitiion): Seq[String]=Nil`
5. RDD的种类：继承自基础的RDD类
   1. HadoopRDD,newAPIHadoopRDD
   2. MapperedRDD
   3. FlatMappedRDD
   4. FilteredRDD
   5. PairedRDD
6. 从外部数据读入并初始化为RDD
   1. 文件系统：单个文件(textFile)、文件目录(wholeTextFiles)
   2. Hadoop Input format：不同的读取函数返回HadoopRDD
   3. 从Driver数据集生成RDD,SparkContext的parallelized函数
   4. 对RDD的一些操作后产生新的RDD
7. 对RDD的操作
   1. Transformation
      1. 接收一个RDD作为输入，返回一个新的RDD
      2. 但是并不会真实执行计算，只是定义生成的新RDD并且设置其与前一个RDD的依赖关系
      3. 操作对RDD依赖关系的区分
         1. 窄依赖：只依赖前一个RDD的确定的几个分区
         2. 宽依赖：依赖前一个RDD的所有分区
   2. Action
      1. 输入还是RDD，但是输出就不是RDD了\
      2. 调用了Action之后，整个从输入RDD到输出值的Transformation链条会被执行

| Transformation操作 | 说明                                                  |
| ------------------ | ----------------------------------------------------- |
| map(func)          | 对源RDD中的每个元素调用func，生产新的元素，这些元素构 | 成新的RDD并返回 |
| flatMap(func)                   | 与map类似，但是func的返回是多个成员     |
| filter(func)                    |  对RDD成员进行过滤，成员调用func返回True的才保留，保留的构成新RDD返回 |
| mapPartitions(func)            | 和map类似，但是func作用于整个分区，类型是`Iterator<T> => Iterator<T>`     |
| mapPartitionsWithIndex(func)   |      |
| union(otherDat aset)            |      |
| reduceByKey(func, [numTasks])  |  对`<key, value>`结构的RDD聚合，相同key的value调用reduce, func是(v,v)=>v   |
| join(otherDataset, [numTasks]) |      |

> Transformation操作对应的依赖关系

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/39.png)

| Action操作   | 说明                                                  |
| ------------ | ----------------------------------------------------- |
| reduce(func) | 对RDD成员使用func进行reduce操作，func接收两个值只返回 |一个值；reduce只有一个返回值。func会并发执行 |
| collect()                 | 将RDD读取到Driver程序里面，类型是Array，要求RDD不能太大 |
| count()                   | 返回RDD成员数量     |
| first()                   | 返回RDD第一个成员，等价于take(1)     |
| take(n)                   |      |
| saveAsTextFile(path)     | 把RDD转换成文本内容并保存到指定的path路径下，可能有多个文件；path可以是本地文件系统路径，也可以是HDFS路径，转换方法是RDD成员的toString方法 |
| saveAsSequenceFile(path) |      |
| foreach(func)             | 对RDD的每个成员执行func方法，没有返回值     |

### 12.6.1. Spark Map-Reduce实例
```scala
object MyFunctions{
   def lineSplit(line: String) : Array[String] = {
      line.split(" ")
   }
}
val textFile = sc.textFile("README.md")
val words = textFile.flatMap(MyFunctions.lineSplit)
#先func再map
val wordPairs = words.map(word => (word, 1))
#先func再map
val wordCounts = wordPairs.reduceByKey((a, b) => a
+ b) wordCounts.collect()
```

## 12.7. DAG 排程器
1. 把一个Spark Job转换成Stage的DAG(Directed Acyclic Graph有向无环图)
2. 根据RDD和Stage之间的关系找出开销最小的调度方法， 然后把Stage以TaskSet的形式提交给TaskScheduler
3. Job:一次Action的所有工作就是一个Job
4. 如何划分Stage?
   1. 以宽依赖为分界
   2. 宽依赖之前的所有Transformation为一个Stage
5. 数据是否需要重组
   1. 一个Stage包括一个或多个Transformation
   2. 一个Transformation在一个RDD分区上执行

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/40.png)

1. 从Action开始构造Stage DAG
2. 最后的Action构造一个ResultStage
3. 填补Stage需要的输入RDD,并根据对RDD的依赖关系划分Stage
4. 直到所有的RDD依赖关系都补充完整
5. 开始按照DAG计算需要的RDD
6. 将每一个Stage封装程TaskSet交给TaskScheduler调度

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/41.png)

## 12.8. 任务排程器

1. DAGScheduler最后一步:计算Task最佳执行位置；为每一个RDD分区创建Task；将一个Stage的Task封装成TaskSet交给TaskScheduler
2. TaskScheduler为每个Stage的TaskSet创建一个TaskSetManager,负责跟踪Task Set中所有Task,包括失败重启等
3. 使用SchedulerBuilder管理TaskSetManager,决定Task Set的调度顺序
   1. FIFOSchedulerBuilder:先来先调度
   2. FairSchedulerBuilder:公平调度,按照资源情况调度
4. DriverEndpoint通过makeOffers找出计算资源
5. TaskScheduler根据计算资源为TaskSet中每一个Task分配Executor
   1. 遍历TaskSet
   2. 使用TaskSetManager遍历TaskSet里面的Task
   3. 按照"本地性"分配Executor
6. DAGScheduler
7. TaskSet
8. TaskSetManager
9. SchedulerBuilder
   1. FIFOSchedulerBuilder
   2. FairSchedulerBuilder
10. DriverEndpoint:makeOffers
11. TaskScheduler:resourceOffers
12. TaskSetManager:resourceOffer

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/42.png)

## 12.9. 资源分配
1. 只考虑Standalone集群:最简单的集群模式
2. Application调度
   1. 只支持先进先出(FIFO)的应用调度方式
   2. 如何给应用分配资源？
      1. 静态分配：简单，一次性分配所有资源，直到应用退出才回收
      2. **不支持**：动态分配：复杂
      3. 在运行过程中按照需要进行分配，有请求、移除策略
3. Job调度
   1. FIFO
   2. Fair：调度池共享资源，Job加入一个池默认行为(池内Job按照FIFO调度)
4. TaskSet调度
   1. FIFO
   2. Fair

# 13. 使用Spark处理数据

## 13.1. 数据读取、存储
1. 从数据源到RDD
   1. parallelize()
   2. textFile(path)
   3. hadoopFile(path)
   4. sequenceFile(path)
   5. objectFile(path)
   6. binaryFiles(path)
2. 从RDD目标数据
   1. saveAsTextFile(path)
   2. saveAsSequenceFile(path)
   3. saveAsObjectFile(path)
   4. saveAsHadoopFile(path)
3. 读取存储MongoDB例子

```java
import com.mongodb.hadoop.MongoOutputFormat;

Configuration config = new Configuration(); config.set("mongo.input.uri",
"mongodb://10.1.50.124:27017/ligf.student"); config.set("mongo.output.uri",
"mongodb://10.1.50.124:27017/ligf.test");

JavaPairRDD<Object, BSONObject> mongoRDD = sc.newAPIHadoopRDD(config, com.mongodb.hadoop.MongoInputFormat.class, Object.class, BSONObject.class);

rdd.saveAsNewAPIHadoopFile("file:///bogus", classOf[Any], classOf[Any], classOf[com.mongodb.hadoop
.MongoOutputFormat[Any, Any]], config)
```

## 13.2. Spark Streaming
1. 实时对大量数据进行快速处理：处理周期短；连续不断地计算
2. 计算基本过程

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/43.png)

3. 数据分批

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/44.png)

4. StreamingContext (类似SparkContext)
5. Dstream (类似RDD)
   1. 内部是通过RDD实现的
   2. 每个时间点对应一个RDD
6. 程序执行过程
   1. 初始化StreamingContext
   2. 创建Dstream
   3. 对DStream的操作
      1. Transformation操作
         1. 参考RDD
         2. transform操作：直接操作内部RDD
         3. 窗口(Window)操作：合并几个时间点的RDD
      2. Output操作
         1. print()
         2. saveAsTextFiles/saveAsObjectFiles()
         3. foreachRDD(func): func一般是对RDD的Action操作

## 13.3. Spark GraphX
1. 图计算:以图为数据结构基础的相关算法及应用
2. 数据结构——图
   1. G=`<V, E>`
   2. V表示顶点集合；E表示边集合
   3. 两个顶点u,v相连，表示为边(u,v)
   4. 无向边；任意边为无向边则称为无向图
   5. 有向边；每一条都为有向边则称为有向图
3. GraphX提供的API
   1. 图生成
   2. 图数据访问:查询顶点数、边数；计算某个点的入度、出度等。
   3. 图算法:遍历顶点、边；计算连通性；计算最大子图；计算最短路径； 图合并等
4. GraphX的实现
   1. 核心是Graph数据结构，表示有向多重图
   2. 两个顶点间允许存在多条边，表示不同含义
   3. Graph由顶点RDD和边RDD组成
   4. Graph的分布式存储方式

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/45.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/46.png)

5. 图生成
   1. 读入存储关系信息的文件，构造EdgeRDD：eRDD = sc.textFile()
   2. 从Edge RDD构造Graph：graph = Grapth.fromEdges(eRDD)
6. 基本接口
   1. 获取边数：numEdges;获取节点数：numVertices
   2. 获取入度、出度：inDegrees, outDegrees
   3. 吉构操作：reverse，subgraph, mask
7. 关联类操作
   1. joinVertices:
   2. outerJoinVertices:
8. 聚合类操作
   1. 分布式遍历所有的边，执行自定义的sendMsg函数;
   2. 在节点上执行mergeMsg函数
   3. <a href = "http://spark.apache.org/docs/latest/graphx-programming-guide.html#summary-list-of-operators">官网API说明</a>

## 13.4. Spark MLlib
1. Spark为机器学习问题开发的库:分类、回归、聚类和协同过滤等
2. 机器学习简介

### 13.4.1. 学习方法的类别-按输入数据分
1. 监督学习
   1. Decision trees, neural networks, nearest-neighbor algorithms,Bayesian learning, hidden Markov models, SVM
   2. 分类问题：输出是非连续的有限集合
   3. 回归问题：输出是连续的实数集合
2. 无监督学习
   1. 聚类问题：基于元素的相似度计算规则
   2. 半监督学习
   3. 强化学习：Markov Decision Processes, temporal difference learning, Q-learning

### 13.4.2. 分类问题的例子
1. 判定一个给定案件的案由
2. 目标：离婚纠纷、产品质量纠纷、债务纠纷、其它
3. 输入：给定的案件情况描述

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Big-data-analysis/img/lec12/47.png)

### 13.4.3. Spark中相关库
1. Spark为机器学习问题开发的库
   1. 分类、回归、聚类和协同过滤等
2. 机器学习简介
3. MLlib简介
   1. 基础数据类型
      1. 向量
      2. 带标注的向量:用于监督学习
      3. 模型:训练算法的输出
   2. 主要的库
      1. mllib.classification:分类算法，二分类、多分类、逻辑回归、朴素贝叶斯、SVM等
      2. mllib.cluster:聚类，K-Means、LDA等
      3. mllib.recommendation:使用协同过滤的方法做推荐
      4. mllib.tree:决策树、随机森林等算法
   3. 其它常用库
      1. mllib.evaluation:算法效果衡量方法

# 14. 作业

## 14.1. 流数据处理
1. 第一阶段
   1. 数据爬取和存储到MongoDB(作为以后实验的数据源)
   2. 流数据模拟
2. 第二阶段
   1. 流数据处理
   2. 结果展示
3. 选题范围
   1. 京东不同种类商品的评论——统计关注点变化曲线
   2. 笔记本电脑、手机、微单
   3. "雪球网"每支股票的评论和用户拥有的股票信息——情绪曲线
   4. 阿里商品销售数据集(商店和用户)——按时间排序后统计店铺销售单数曲线
   5. 豆瓣用户小组信息——更新用户画像(假设爬取顺序就是加入顺序)

## 14.2. GraphX
1. 笫一阶段
   1. 构造图
   2. 展示图
2. 笫二阶段
   1. 基于图的操作方法作计算
      1. 例如：好友推荐、股票推荐、对给定的句子分词
      2. 发挥想象力，寻找有趣的、有意义的、有价值的图计算应用
3. 选题范围
   1. 如作业1

## 14.3. MLlib
1. 分类
   1. 利用抓取的数据构建一个可以使用分类方法解决的需求
   2. 整理训练集、测试集
   3. 使用MLlib工具训练分类器
   4. 展示效果
2. 聚类
   1. 同样，提出一个聚类能够解决的需求
   2. 整理数据
   3. 执行分类算法
   4. 展示结果

