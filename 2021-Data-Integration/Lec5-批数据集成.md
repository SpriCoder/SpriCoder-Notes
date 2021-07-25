批数据集成
---

# 1. 批数据集成简介

## 1.1. 批数据集成
1. 批数据集成
   1. 静态数据集
   2. 数据被组织成"批"地（时间窗口）
   3. 周期性的迁移到另一个系统（专门的数据端）
   4. 抽取、转换、集成为通用数据格式
   5. 持久化集成数据
2. 应用
   1. 数据仓库
   2. 数据分析等数据服务应用

## 1.2. 特征
1. 特点
   1. 时效性要求不高（时间窗口较大）
   2. 数据精确性要求高
   3. 数据有长久的价值
2. 必要性
   1. 整合分散、过量冗余、不一致的数据，提供完整、准确、易共享的数据系统。
   2. 解决信息孤岛问题，提高数据使用价值
   3. 提供高支持管理决策能力的数据服务
3. 优点
   1. 底层数据结构透明：对数据访问等消费应用提供了统一接口，无需暴露底层数据结构
   2. 高性能和扩展性：把数据集成和数据访问分成了两个过程，因此访问时数据已经处于准备好的状态。
   3. 数据集成后提供真正单一数据视图
   4. 高可重用性：由于有了实际的物理存储，数据可以为各种应用提供可重用的数据视图，而不用担心底层实际的数据源的可用性。
   5. 数据管控能力加强，降低管理成本


## 1.3. 基本问题
1. 一致性
   1. 数据一致性
   2. 语义一致性
2. 异构性
   1. 数据源的异构性
   2. 数据模式的异构性
   3. 数据类型的异构性（eg:浮点数float/double）
   4. 取值的异构性（eg:性别0/1 F/M）
   5. 语义的异构性（eg:不同数据的id）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/1.png)

3. 容错性:各个数据源有很强的自治性,它们可以在不通知集成系统的前提下改变自身的结构和数据，不要`select *`这样子发生迁移、扩展时不会出现问题。
4. 可伸缩性

## 1.4. 框架
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/2.png)

1. spark的数据库如何确定
2. spark的文件节点的确定
   1. sqoop
   2. flume

## 1.5. 案例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/3.png)

# 2. 采集、迁移工具

## 2.1. Sqoop

### 2.1.1. Sqoop简介
1. 什么是Sqoop
   1. Sqoop：SQL–to–Hadoop
   2. Sqoop项目始于2009年，早期为Hadoop的第三方模块，后来成为Apache的独立项目
   3. Sqoop是一个主要在Hadoop和关系数据库之间进行批量数据迁移的工具

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/4.png)

2. 版本：Sqoop1与Sqoop2完全不兼容

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/5.png)

#### 2.1.1.1. Sqoop1
1. 优点
   1. 架构简单
   2. 部署简单
   3. 功能全面
   4. 稳定性较高
   5. 速度较快
2. 缺点
   1. 访问方式单一
   2. 命令行方式容易出错，格式紧耦合
   3. 安全机制不够完善，存在密码泄露风险

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/6.png)

#### 2.1.1.2. Sqoop2
1. 优点
   1. 访问方式多样
   2. 集中管理连接器
   3. 安全机制较完善
   4. 支持多用户
2. 缺点
   1. 架构较复杂
   2. 部署较繁琐
   3. 稳定性一般
   4. 速度一般

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/7.png)

### 2.1.2. Sqoop原理
1. 数据导入：RDBMS->Hadoop

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/8.png)

2. 数据导出：Hadoop->RDBMS

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/9.png)

### 2.1.3. Sqoop使用
1. Sqoop安装
   1. 需要准备Java JDK和Hadoop
   2. 需要准备数据库驱动，比如：下载mysql的数据库驱动，移动到Sqoop的lib目录中
2. 下载安装Sqoop，修改配置
3. 验证Sqoop，输入命令：`sqoop version`

### 2.1.4. Sqoop基本用法

#### 2.1.4.1. 列出databases
- 明文密码：

```
sqooplist-databases \
--connect jdbc:mysql://IP:PORT/ \
--username USER \
--password PASSWD;
```

- 输入密码：

```
sqooplist-databases \
--connect jdbc:mysql://IP:PORT/ \
--username USER \
-P
```

- 密码文件

```
sqooplist-databases \
--connect jdbc:mysql://IP:PORT/ \
--username USER \
--password-file file:/temp
```

#### 2.1.4.2. 列出数据库的所有表
- 明文密码：
```
sqooplist-tables \
--connect jdbc:mysql://IP:PORT/testDB\
--username USER \
--password PASSWD;
```

- 输入密码：

```
sqooplist-tables \
--connect jdbc:mysql://IP:PORT/ testDB\
--username USER \
-P
```

- 密码文件：

```
sqooplist-tables \
--connect jdbc:mysql://IP:PORT/testDB\
--username USER \
--password-file file:/temp
```

#### 2.1.4.3. 全量数据导入
```
sqoop import \
  --connect jdbc:mysql://IP:PORT/testDB\
  --username USER \
  --password PASSWD \
  --query "select * from testdbwhere \$CONDITIONS" \
  --target-dir/input \
  --fields-terminated-by "\\01" \
  --hive-drop-import-delims\
  --null-string "\\N" \
  --null-non-string "\\N" \
  --split-by id \
  -m 6 \
```

- 参数说明
  - `--query`：sql查询语句
  - `--target-dir`：hdfs目标目录
  - `--hive-drop-import-delims`：删除数据中包含的Hive默认分隔符（^A, ^B, \n）
  - `--null-string`：string类型空值的替换符（Hive中Null用\n表示）
  - `--null-non-string`：非string类型空值的替换符
  - `--split-by`：数据切片字段（int类型，m>1时必须指定）
  - `-m`：Mapper任务数，默认为4

#### 2.1.4.4. 基于递增列的增量数据导入(Append)
```
sqoop import \
  --connect jdbc:mysql://IP:PORT/testDB\
  --username USER \
  --password PASSWD \
  --query "select * from table1 where \$CONDITIONS" \
  --target-dir/input \
  --split-by id \
  -m 6 \
  --incremental append \
  --check-column id \
  --last-value 4
```

- 参数说明
  - `--incremental append`：基于递增列的增量导入（将递增列值大于阈值的所有数据增量导入Hadoop）
  - `--check-column`:递增列（int）
  - `--last-value`:阈值（int）

#### 2.1.4.5. 基于时间列的增量数据导入（LastModified方式）
```
sqoop import \
  --connect jdbc:mysql://IP:PORT/testDB\
  --username USER \
  --password PASSWD \
  --query "select * from table1 where \$CONDITIONS" \
  --target-dir/input \
  --split-by id \
  -m 1 \
  --incremental lastmodified\
  --merge-key id \
  --check-column time \
  --last-value "2020-05-01 00:00:00"
```

- 参数说明
  - `--incremental lastmodified`：基于时间列的增量导入（将时间列大于等于阈值的所有数据增量导入Hadoop）
  - `--merge-key`:合并列（主键，合并键值相同的记录）
  - `--check-column`:时间列（timestamp）
  - `--last-value`:阈值（timestamp）

## 2.2. Flume

### 2.2.1. Flume简介
1. 什么是Flume
   1. Flume是一个分布式海量日志采集、聚合和传输系统
   2. Flume是由cloudera软件公司产出的可分布式日志收集系统，后与2009年被捐赠了apache软件基金会，为hadoop相关组件之一。
2. 特点
   1. 基于事件的海量数据采集
   2. 数据流模型：Source->Channel->Sink
   3. 事务机制：支持重读重写，保证消息传递的可靠性
   4. 内置丰富插件：轻松与各种外部系统集成
   5. 高可用：Agent主备切换
   6. Java实现：开源，优秀的系统框架设计，模块分明，易于开发
3. 应用场景

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/10.png)

### 2.2.2. Flume原理

#### 2.2.2.1. 基本概念
1. Event：事件，最小数据传输单元，由Header和Body组成

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/11.png)

2. Agent
   1. 代理，JVM进程，最小运行单元
   2. 由Source、Channel、Sink三个核心组件构成
   3. 负责将外部数据源产生的数据以Event的形式传输到目的地
3. Source
   1. 对接各种外部数据源，将采集到的数据封装成Event，然后写入Channel
   2. 一个Source可向多个Channel发送Event
   3. Flume内置类型丰富的Source，包括avro、exec、jms、spooldir、netcat、sequence generator、syslog、kafka、http、legacy、自定义。
4. Channel
   1. Event暂存容器，负责保存Source发送的Event，直至被Sink成功读取，可以存放在memory、jdbc、file、kafka channel等
   2. 为了平衡Source采集、Sink读取的速度，可视为Flume内部的消息队列
   3. 线程安全并具有事务性，支持Source写失败重写和Sink读失败重读
5. Sink
   1. 负责从Channel读取Event，然后将其写入目的地，目的地既可以是外部存储，也可以是下一阶段的Agent。包括hdfs、logger、avro、ipc、file、null、hbase、Kafka Sink自定义。
   2. 一个Sink只能从一个Channel中读取Event
   3. Sink成功读取Event后，向Channel提交事务，Event被删除，否则Channel会等待Sink重新读取
6. 映射关系：
   1. 1个Source --> 多个Channel
   2. 1个Channel --> 多个Sink
   3. 1个Sink --> 1个Channel

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/12.png)

#### 2.2.2.2. 数据流
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/13.png)

- 越长越容易出错

| 扇入流                | 扇出流                |
| --------------------- | --------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/14.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/15.png) |

### 2.2.3. Flume使用
1. 安装
   1. 运行环境：JDK1.7及以上版本
   2. 下载安装Flume，修改配置
   3. 验证Flume
      1. 在Flume安装目录下，运行命令./bin/flume-ng version，查看Flume版本信息
2. Agent配置示例

```
/*定义Agent组件名*/
a1.sources = r1
a1.sinks= k1
a1.channels= c1 
/*配置Souce */
a1.sources.r1.type = netcat // Source类型为netcat, 监听指定的Socket端口
a1.sources.r1.bind = localhost
a1.sources.r1.port= 44444
/*配置Sink */
a1.sinks.k1.type = logger // Sink类型为logger, 将Event输出到控制台
/*配置Channel */
a1.channels.c1.type = memory // Channel类型为memory, Event缓存在内存中
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity= 100
/*设置Source、 Sink和Channel的关系*/
a1.sources.r1.channels= c1
a1.sinks.k1 channel=c1 //一个Sink只能连接一个Channel
```

3. 针对不同source、channel、sink类型的配置自行搜索
4. Flume运行步骤
   1. 编写Agent配置文件（*.conf）
   2. 运行Agent，命令如下：
      1. `# bin/flume-ng agent --confconf--conf-file example.conf--name a1 -D flume.root.logger= INFO, console`
      2. `--conf`：Agent配置文件目录
      3. `--conf-file`：Agent配置文件名（*.conf）
      4. `--name`：Agent名称
      5. `-D`：JVM参数

# 3. ETL

## 3.1. ETL 简介
1. 全称：Extract-Transform-Load
2. 定义：
   1. 用来描述数据从来源端，经过萃取、转换、加载，至目的端的过程。
   2. 将数据从孤立的数据源中采集出来，汇集到可被计算平台高效访问的目的地。
3. 其他
   1. 常用在**数据仓库**，但不限于数仓。
   2. 整个流程可用**任何语言**开发完成。
   3. 常与**ELT**（Extract-Load-Transform）混用，通常数据量越大、转换逻辑越复杂、目的端数据库运算能力越强，越倾向使用ELT，以便运用目的端数据库的并行处理能力。

## 3.2. ETL 应用
1. 业务场景
   1. 汇总业务交易数据
   2. 将应用数据从旧系统迁移到新系统
   3. 整合近期公司收购或合并的数据
   4. 整合来自外部供应商、合作伙伴的数据
2. 技术领域
   1. 数据仓库（Data Warehouse）
   2. 决策支持系统（Decision Support System）
   3. 联机分析处理（Online Analytical Processing）
   4. 数据挖掘（Data Mining）
   5. 商务智能（Business Intelligence）

## 3.3. ETL 过程
1. Extract（不同的数据源 —> OperationalDataStore）
   1. 大量调研
      1. 数据来自几个业务系统？
      2. 系统各自数据库服务器运行什么DBMS？
      3. 存在多少手工数据？
      4. 存在多少非结构化数据？
   2. 抽取方案
      1. 与DW的数据库系统相同的数据源：直接连接，select 语句直接访问
      2. 与DW的数据库系统不同的数据源
         1. 直接连接
         2. 将源数据导出.txt/.xls后，再将这些文件导入ODS
         3. 通过程序接口完成
      3. 增量更新：对于数据量大的系统，利用时间戳，增量抽取
2. Transform（Cleaning、Transform）
   1. 数据清洗（是一个反复的过程，需要不断修正）
      1. 不完整的数据（名称、区域信息等）
         1. 补全
      2. 错误的数据（数值输成全角字符、日期越界等）
         1. 用SQL语句找出后，在业务系统修正后抽取
      3. 重复的数据：
         1. 将重复字段导出，交由客户确认
   2. 数据转换
      1. 转换不一致数据
         1. 不同业务系统相同类型的数据要统一
      2. 转换数据粒度
         1. 将业务系统数据按照数据仓库粒度进行聚合
      3. 商务规则计算
         1. 数据指标
3. Load
   1. Transform 的工作量约占2/3
   2. 数据的加载一般是数据清洗了之后，直接写入数据仓库中去

## 3.4. ETL工具
1. Datastage
   1. IBM 公司的商业软件，最专业的ETL工具
   2. 价格不菲，适合大规模的ETL 应用
   3. 使用难度：★★★★
2. Informatica
   1. 商业软件，相当专业的ETL 工具
   2. 价格比Datastage 便宜一点，也适合大规模的ETL 应用
   3. 使用难度：★★
3. Kettle
   1. 免费，开源
   2. 纯Java 编写，只需JVM 即可部署，可跨平台、扩展性好
   3. 使用难度：★★
4. 其他
   1. DatePipeline、Talend、Datax、Oracle Goldengate
   2. 自己探索

## 3.5. ETL 注意事项
1. 数据连接：数据源的数据库技术不一致
2. 性能
   1. 集中式架构扩展性差
   2. 分布式架构扩展性强
3. 转换灵活
   1. 匹配、合并、更改数据非常重要
4. 数据质量
   1. 数据质量决定产品质量上界
5. 批、流一体的数据融合
   1. 数据是按触发器获取，还是按时间间隔获取
   2. 若企业对数据的实时性要求高，则需考虑流处理能力

# 4. 数据存储

## 4.1. 文件存储系统HDFS

### 4.1.1. HDFS简介
1. 什么是HDFS
   1. Hadoop分布式文件系统（Hadoop Distributed File System）
   2. HDFS是Apache Hadoop的核心子项目
   3. HDFS是GFS的开源实现
   4. Master/slave架构
2. 设计目标
   1. 运行在大量廉价商用机器上，提供容错机制：故障检测、快速自动恢复机制
   2. 简单可靠的聚合模型：一次写入多次读取，支持追加，不允许修改，保证数据一致性
   3. 流式数据访问：批量读而非随机读，关注吞吐量而非时间
   4. 可靠存储和处理大量数据的可伸缩性
   5. 通过分布数据和逻辑到数据所在的多个节点上进行平行处理来提高效率
3. 优点
   1. 高容错、高可用、高扩展
      1. 数据冗余，多Block多副本，副本丢失后自动恢复（一般三副本）
      2. NameNodeHA、安全模式
   2. 海量数据存储
      1. 典型文件大小GB~TB，百万以上文件数量，PB以上数据规模
   3. 构建成本低、安全可靠
      1. 构建在廉价的商用服务器上
      2. 提供了容错和恢复机制
   4. 适合大规模离线批处理
      1. 流式数据访问
      2. 数据位置暴露给计算框架
      3. 处理逻辑接近数据，而不是数据接近处理逻辑
4. 缺点
   1. 实时性差，不适合低延迟数据访问
   2. 小文件问题，不适合大量小文件存储
      1. 元数据占用NameNode大量内存空间
         1. 每个文件、目录和Block的元数据都要占150Byte
         2. 存储1亿个元素，大约需要20GB内存
         3. 如果一个文件为10KB，1亿个文件大小仅有1TB，却要消耗掉20GB内存
      2. 磁盘寻道时间超过读取时间
   3. 不支持并发写入
      1. 一个文件同时只能有一个写入者
   4. 文件修改问题，不支持文件随机修改
      1. 仅支持追加写入
5. 系统架构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/16.png)

6. 写操作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/17.png)

7. 读操作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/18.png)

### 4.1.2. HDFS文件管理
1. Shell命令
   1. `Hadoop fs <args>`（使用面最广，可以操作任何文件系统）
   2. `hdfs dfs<args>` （只能操作HDFS文件系统）
2. 简单示例
   1. hadoopfs –help
   2. hadoopfs –ls/tmp
   3. hadoopfs –text /tmp/*|less
   4. hadoopfs –get /tmp/file localfile
   5. hadoopfs –put localfile/tmp/
   6. 等

## 4.2. 存储方式

### 4.2.1. 概述
1. 大数据文件存储格式
   1. 面向行（Row-Based）存储
   2. 面向列列（Column-Based）存储
   3. 混合存储
2. 选择焦点
   1. 更有效处理海量数据，存储量要求
   2. 安全、可靠、完整性
   3. 更适合存储、压缩、读取、查询，节约存储，保证效率等

### 4.2.2. 行存储
1. 行存储
   1. 同一行的数据存储在一起，即连续存储
   2. 如果只需要访问行的一小部分数据，亦需要将整行读入内存
   3. 面向行的存储适合于整行数据需要同时处理的情况。
2. 举例
   1. <a href = "https://blog.csdn.net/en_joker/article/details/79648861">SequenceFile文件</a>
   2. MapFile文件
   3. <a href = "https://stackoverflow.com/questions/24236803/difference-between-avrodata-file-and-sequence-file-with-respect-to-apache-sqoop">Avro Datafile</a>

### 4.2.3. 列存储
1. 列存储
   1. 整个文件被切割为若干列数据，每一列数据一起存储
   2. 面向列的格式使得读取数据时，可以跳过不需要的列，适合于只处于行的一小部分字段的情况
   3. 读写需要更多的内存空间，因为需要缓存行在内存中（为了获取多行中的某一列）
   4. 不适合流式写入，因为一旦写入失败，当前文件无法恢复，而面向行的数据在写入失败时可以重新同步到最后一个同步点，所以Flume采用的是面向行的存储格式。
2. 举例
   1. <a href = "https://www.cnblogs.com/ITtangtang/p/7677912.html">ORCFile</a>
   2. Parquet
      1. <a href = "https://www.cnblogs.com/ITtangtang/p/7681019.html">参考一</a>
      2. <a herf = "https://blog.csdn.net/colorant/article/details/53699822">参考二</a>

### 4.2.4. 对比
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/19.png)

1. 行存储的优点
   1. 一次性完成，消耗的时间比列存储少
   2. 能够保证数据的完整性
2. 列存储的优点
   1. 可以跳过不符合条件的数据，只读取需要的数据，降低IO数据量
   2. 压缩编码可以降低磁盘存储空间。由于同一列的数据类型是一样的，因此可以使用更高效的压缩算法，进一步节约存储空间。
   3. 只读取需要的列，不用全表扫描，不会产生冗余数据
   4. 支持向量运算，能够获取更好的扫描性能

## 4.3. 数据仓库及Hive

### 4.3.1. 数据仓库简介
1. 什么是数据仓库：数据仓库是一个面向主题的、集成的、随时间变化的、非易失的数据集合，用于支持管理者的决策过程。
2. 特点
   1. 面向主题
      1. 系统业务级别主题
      2. 决策时关心的重点方面
   2. 集成
      1. 多个异构数据源
      2. 经过ETL处理
   3. 随时间变化
      1. 历史操作数据周期性迁移至数仓
      2. 反映了某一历史时间点的数据快照
   4. 非易失
      1. 一旦进入数仓，数据就不应再有改变
      2. 保留数据变化的历史轨迹

### 4.3.2. 数据仓库基本架构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/20.png)

1. 缓冲层（数据接入层）
   1. 概念
      1. 业务系统与ODS层之间的临时缓冲区，用于临时接入业务系统的原始细节数据
      2. 是否设立缓冲层，视情况而定
   2. 数据
      1. 细粒度：与业务系统保持一致的原始细节数据，不做任何处理
      2. 有效期：临时（1~2天），并定期清除
   3. 作用：当ODS层需做简单清洗，且数据导入速度较快时，缓冲层用于临时性地快速接收业务数据
2. ODS层（贴源层）
   1. 概念
      1. ODS：Operational Data Store，操作数据存储，一个面向主题的、集成的、可变的、当前的细节数据集合，用于支持即时性、操作型、集成性的信息需求
      2. 业务系统和基础明细层之间的过度区，用于存储业务系统的当前原始细节数据
   2. 数据
      1. 来源：业务系统或缓冲层
      2. 细粒度：数据结构、数据间逻辑关系、数据粒度均与业务系统保持一致的原始细节数据
      3. 高集成：按主题进行全面集成，拥有业务数据的完整视图
      4. 低质量：不做处理或仅做简单清洗，并加时间戳（一般不做数据清洗、聚合和汇总）
      5. 有效期：短期（1~2个月），并定期清除
   3. 作用
      1. 当作为业务系统与数仓之间的隔离区，避免数仓直接从业务系统抽取数据，最小化对业务系统的干扰
      2. 承接部分业务系统的原始细节数据（低粒度）的查询和报表功能，降低业务系统的查询和分析压力
3. 基础明细层（DWD层）
   1. 概念
      1. DWD：Data Warehouse Detail
      2. 数据仓库的中间层，从ODS层获取数据，按主题进行组织，经过清洗、校验、转换、合并等规范化处理，形成业务数据的完整视图
   2. 数据
      1. 来源：ODS层
      2. 细粒度：与ODS基本一致，不做聚合和汇总
      3. 高质量：经过清洗、校验、转换、合并（根据业务进行数据关联形成宽表）等规范化处理
      4. 高集成：按主题进行组织，拥有业务数据的完整视图
      5. 有效期：永久
   3. 作用：为数据分析（宏观趋势性分析、在线交互式分析）提供最完整的基础明细数据支撑
4. 轻度汇总层
   1. 面向业务分析需求，对基础明细层的细节数据进行细粒度（轻度）的聚合、汇总和统计
   2. 提前计算出细粒度的基础汇总指标，减轻后期数据分析的压力
5. 主题模型层：针对企业级宏观主题，构建相关的多个主题域模型，从基础明细/轻度汇总层中获取数据，按主题模型进行数据组织，为业务分析应用、数据集市构建提供直接的数据支撑
6. 数据集市
   1. 数据集市是面向单一主题域（如销售、财务等）、为特定业务部门构建的小规模数据集合
   2. 数据源可以是数据仓库（从属数据集市），也可以是业务系统（独立数据集市）
   3. 数据集市是数据仓库的子集
   4. 用于在线交互式分析（秒级响应）

### 4.3.3. Hive

#### 4.3.3.1. Hive简介
1. 什么是Hive
   1. 基于Hadoop的一个数据仓库工具
   2. 将结构化的数据文件映射为一张数据库表
   3. 提供SQL查询功能，将SQL语句转变成MapReduce任务来执行。
2. 特点
   1. 通过类SQL来分析大数据，而避免了写MapReduce程序来分析数据，这样使得分析数据更容易。
   2. 数据底层存储在HDFS上，Hive本身并不提供数据的存储功能
   3. Hive是将数据映射成数据库和一张张的表，库和表的元数据信息一般存在关系型数据库上（比如MySQL）。
   4. 数据存储方面：它能够存储很大的数据集，并且对数据完整性、格式要求并不严格。
   5. 数据处理方面：因为Hive语句最终会生成MapReduce任务去计算，所以不适用于实时计算的场景，它适用于离线分析
3. Hive架构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/batch/21.png)

#### 4.3.3.2. 重要概念
1. 内部表
   1. 默认创建的是内部表（managed table），存储位置在hive.metastore.warehouse.dir设置，默认位置是/user/hive/warehouse。
   2. 导入数据的时候是将文件剪切（移动）到指定位置，即原有路径下文件不再存在
   3. 删除表的时候，数据和元数据都将被删除
   4. 默认创建的就是内部表create table xxx (xx xxx)
2. 外部表
   1. 外部表文件可以在外部系统上，只要有访问权限就可以
   2. 外部表导入文件时不移动文件，仅仅是添加一个metadata
   3. 删除外部表时原数据不会被删除
   4. 分辨外部表内部表可以使用DESCRIBE FORMATTED table_name命令查看
   5. 创建外部表命令添加一个external即可，即create external table xxx (xxx)
   6. 外部表指向的数据发生变化的时候会自动更新，不用特殊处理
3. 分区
   1. 有些时候数据是有组织的，比方按日期/类型等分类，而查询数据的时候也经常只关心部分数据，比方说我只想查2017年8月8号，此时可以创建分区，查询具体某一天的数据时，不需要扫描全部目录，所以会明显优化性能
   2. 一个Hive表在HDFS上是有一个对应的目录来存储数据，普通表的数据直接存储在这个目录下，而分区表数据存储时，是再划分子目录来存储的
   3. 使用partionedby (xxx)来创建表的分区
4. 分桶
   1. 分桶是相对分区进行更细粒度的划分。分桶将整个数据内容安装某列属性值得hash值进行区分，按照取模结果对数据分桶。如取模结果相同的数据记录存放到一个文件。
   2. 桶表也是一种用于优化查询而设计的表类型。创建通表时，指定桶的个数、分桶的依据字段，hive就可以自动将数据分桶存储。查询时只需要遍历一个桶里的数据，或者遍历部分桶，这样就提高了查询效率
   3. clustered by (user_id) sorted by(leads_id) into 10 buckets

#### 4.3.3.3. Hive操作
1. 写入数据
   1. 从本地文件系统中导入：`load data local inpath'xxx.txt' into table xxx；`
   2. 从HDFS上导入：
      1. `load data inpath'/home/xxx/add.txt' into table xxx`
      2. `alter table db.access_logadd partition (dt=‘2020-06-01') location 'hdfs://ns/hive/warehouse/access_log/dt=2020-06-01 ';`
   3. 查询结果导入：`insert overwrite table db.log_v2 partition(dt=‘2020-06-01') select uid,model,key,value,timefrom db.log where dt=‘2020-06-01';`
2. HiveSQL
   1. 与关系型数据库的SQL 略有不同，但支持了绝大多数的语句如DDL、DML 以及常见的聚合函数、连接查询、条件查询。
   2. HIVE不适合用于联机(online)事务处理，也不提供实时查询功能。
   3. 适合应用在基于大量不可变数据的批处理作业。
3. 具体命令可以自行查询资料