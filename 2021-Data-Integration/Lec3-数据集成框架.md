数据集成
---

# 1. 数据集成概述

## 1.1. 数据集成的必要性
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/1.png)

1. 历史数据的价值
2. 异构环境数据源
   1. 不同时期、不同的公司、不同的工具、不同的平台
   2. 购买供应上应用包的数量日益增加
   3. 冗余数据、垃圾数据，数据一致性问题
3. 企业需要将内部数据进行发布和交换
4. 大数据和虚拟化的催化剂

## 1.2. 数据集成的概念
1. 对各种异构数据提供统一的表示、存储和管理, 以实现逻辑或物理上有机地集中
   1. 集成是指维护数据源整体上的数据一致性、提高信息共享利用的效率
   2. 透明的方式是指用户不必再考虑底层数据模型不同、位置不同等问题,能够通过一个统一的查询界面实现对网络上异构数据源的灵活访问
2. 以一种统一的数据模式描述各数据源中的数据,屏蔽它们的平台、数据结构等异构性,实现数据的无缝集成
3. 数据样例
   1. 运动的数据：数据治理、数据质量管理、集成
   2. 集成为通用格式——数据转换
   3. 数据从一个系统迁移到另一个系统
   4. 在组织内部移动数据
   5. 从非结构化数据中抽取信息
   6. 将处理移动到数据段。
4. 简单场景：在下图的PPT下面

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/2.png)

5. 上图中是最全的一个场景
   1. 主数据：决定数据类
   2. 描述数据：描述数据的信息

## 1.3. 数据集成的特征
1. 分布性：网络传输的性能和安全性
2. 自治性：在不通知集成系统的前提下改变自身的结构和数据
3. 异构性：运行环境、数据模型和数据语义

## 1.4. 数据集成的分类
1. 批处理数据集成：将数据以成组的方式从源应用周期性地传输到目标应用
2. 实时数据集成：为了完成一个业务事务处理而需要即时地贯穿多个系统的接口
3. 大数据集成
4. 数据虚拟化：使用多种数据集成技术以对多种数据源和技术的数据进行实时整合,而不仅仅结构化数据

### 1.4.1. 批处理数据集成
1. 数据转换方法：松散集成, 通过转换工具实现应用系统之间的数据转换和交换,较低层次的集成
2. 数据聚合方法：借助于中间件系统构造一个虚拟的全局数据模式, 是一种集中式管理、分布式存储的较高层次的集成模式
3. 析取、转换和装载(ETL)：通过对异构数据源中的数据进行分析、转换和装载, 建立一个数据仓库,面向企业决策的数据集成方法

#### 1.4.1.1. 数据转换方法
1. DBMS自带的转换、迁移工具
   1. Oracle的Migration Workbench
   2. Microsoft SQL Server的DTS
   3. 通用性不强
2. 应用系统内部集成的转换工具
   1. 系统与其他应用系统之间的数据接口
   2. 两种规范，EDI
3. 通用的、集成的数据转换工具

#### 1.4.1.2. 数据聚合方法
1. 将多个数据库集成为一个统一的数据库视图
2. 利用中间件集成异构数据源,不需要改变原始数据的存储和管理方式
3. 中间件系统位于异构数据源和应用程序之间
   1. 向下协调各数据库系统
   2. 向上为访问集成数据的应用系统提供统一的全局数据模式和数据访问的通用接口

#### 1.4.1.3. ETL方法
1. 从多个数据源中抽取数据, 然后进行数据转换和加载, 最终得到统一的、完备的数据仓库
2. 原来分散的应用系统仍然独立运作, 原来存在的异构数据源仍然为各自的应用系统提供数据服务
   1. 不会破坏企业原有的应用架构, 比较适合于大量数据的迁移
   2. 可以提供复杂的数据转换功能
   3. 可以集成多种数据源和复杂的商业规则, 能容忍数据在时间上的延迟

## 1.5. 数据集成开发生命周期
1. 项目范围：数据移动的基本需求、基本设置
2. 概要设置：要和数据拥有者以及安全团队谈判持续到达一个可以接受的方案
3. （被盖住了）

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/3.png)

## 1.6. 关键问题
1. 集成范围问题：一方面权限有限
2. 数据资源所有权问题
3. 全局模式问题：A、B、C三种数据源如何合并的问题
4. 模式映射问题：冲突的规则如何进行确认
5. 数据动态集成问题

## 1.7. XML在数据集成中的作用
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/4.png)

1. 定义结构的好处
   1. 标准可以指定
   2. 方便进行管理
2. SHA法：进行文件生成

## 1.8. 基于XML的异构数据集成
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/5.png)

# 2. 元数据与数据映射

# 3. 数据库访问接口

## 3.1. 固有调用VS. 访问接口
1. 数据库引擎带有自己的包含用于访问数据库的APl函数的动态链接库,应用程序可利用操纵数据库
   1. 执行效率
   2. 不通用
2. 访问接口：透明连接
   1. 网络透明
   2. 服务器透明
   3. 语言透明

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/6.png)

## 3.2. 主流的数据访问技术
1. ODBC
2. OLE DB
3. ADO
4. JDBC
5. Hibernate

### 3.2.1. ODBC (Open DataBaseConnectivity )
1. 应用程序：执行处理并调用ODBC API函数,以及提交SQL语句并检索结果
2. 驱动程序管理器：根据应用程序需要加载/卸载驱动程序,处理ODBC函数调用,或把他们传送到驱动程序
3. 驱动程序：处理ODBC函数调用,提交SQL请求到一个指定的数据源,并把结果返回到应用程序
4. 数据源：包含了数据库位置和数据库类型等信息,实际上是一种数据连接的抽象

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/7.png)

#### 3.2.1.1. ODBC的API
1. 核心级
   1. 最基本的功能：分配、释放环境句柄、数据库连接、执行SQL语句等
   2. 满足最基本的应用程序要求
2. 扩展1级：增加一些函数,可在应用程序中动态了解表的模式,可用的概念模型类型等
3. 扩展2级
   1. 主关键字和外来关键字的信息、表和列的权限信息、数据库中的存储过程信息等
   2. 游标和并发控制功能

#### 3.2.1.2. ODBC接口函数
1. 分配和释放内存
2. 连接
3. 执行SQL语句
4. 接收结果
5. 事务控制
6. 错误处理和其他事项

#### 3.2.1.3. 工作流程
1. 调用驱动程序管理器,把目标数据源对相应的驱动程序调入动态连接库;
2. 根据SQL语句,调用动态连接库中若干个相应的ODBC函数;
3. 执行ODBC函数,把SQL语句以字符串的形式传到数据源处;
4. 数据源执行所收到的SQL语句,把结果返回应用程序。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/8.png)

##### 3.2.1.3.1. SQL语句的执行
```java
main()
{
  ASD asd;/*说明asd是一个环境型变量*/
  LZJ lzj;/*说明lzj是一个连接型变量*/
  JDK jdk;/*说明jdk是一个语句句柄变量*/
  RETCODE retcode;/*说明retcode是一个返回变量*/
  SQLAllocEnv(&asd);/*分配一个环境句柄*/
  SQLAllocConnect(asd,&lzj);/*分配一个连接句柄*/
  SQLConnect(lzj,"学生",SQL_NTS,NULL,0,NULL,0);/*连接数据源*/
  SQLAllocStmt(lzj,&jdk);/*分配一个语句句柄*/
  retcode=SQLExecDirect(jdk,"SELECT*FROMS",SQL_NTS);/*执行语句*/
  ……/*结果集处理*/
  SQLDisconnect(lzj);/*断开数据源*/
  SQLFreeStmt(jdk,SQL_DROP)/*释放一个语句句柄*/
  SQLFreeConnect(lzj);/*释放一个连接句柄*/
  SQLFreeEnv(asd);/*当应用完成后,释放环境句柄*/
}
```

##### 3.2.1.3.2. 执行SQL语句的函数
1. SQL语句预备函数：SQLPrepare(jdk,szSqlStr,cbSqlStr)。其中,参数hstmt是一个有效的语句句柄,参数szSqlStr和cbSqlStr分别表示将要执行的SQL语句的字符串及其长度
2. SQL语句执行函数：SQLExecute(jdk)。其中参数jdk是一个有效的语句句柄
3. SQL语句查询结果的获取：

```java
while(RETCODE_IS_SUCCESSFUL(retcode){
  retcode=SQLFetch(jdk);
  if(RETCODE_IS_SUCCESSFUL(retcode){
    do{
      rcGetData=SQLGetData(jdk,1,SQL_C_CHAR,szBuffer,sizeof(szBuffer),&cbValue);
      DISPLAY_MEMO(szBuffer,cbValue);/*显示*/
    }while(rcGetData!=SQL_NO_DATA_FOUND);
  }
}
```

#### 3.2.1.4. ODBC数据库独立性
1. ODBC是为最大的互用性而设计的，要求一个应用程序有用相同的源代码（不用重新编译或重新链接）访问不同的数据库管理系统(DBMS)的能力
2. ODBC定义了一个标准的调用层接口（CLI）。包含X/Open和ISO/IEC的CLI规范中的所有函数，并提供应用程序普遍需要的附加函数
3. 每个支持ODBC的DBMS需要不同的库或驱动程序，驱动程序实现ODBC API中的函数。当需要改变驱动程序时，应用程序不需要重新编译或者重新链接，只是动态加载新的驱动程序，并调用其中的函数即可。如果要同时访问多个DBMS系统，应用程序可加载多个驱动程序
4. 如何支持驱动程序取决于操作系统，例如，在Windows操作系统上，驱动程序是动态链接库（DLL）

#### 3.2.1.5. DBMS特有功能的支持
1. ODBC为所有DBMS功能都定义了公共接口。这些DBMS功能比多数DBMS支持的更多，但只要求驱动程序实现这些功能的一个子集
2. ODBC定义了API和SQL语法一致层，它规定驱动程序应支持的基本功能
3. ODBC还提供两个函数（SQLGetInfo和SQLGetFunctions）返回关于驱动程序和DBMS能力的一般信息及驱动程序支持的函数列表。因此，应用程序可以检查DBMS支持的特殊功能

### 3.2.2. OLE DB
1. 基于COM的数据存储对象，与ODBC 属于底层的数据库编程接口，对ODBC进行了扩展，可以访问非关系型数据库源
2. OLEDB对ODBC进行了两个方面的扩展
   1. 提供了一个数据库编程的OLE接口，即COM
   2. 提供了一个可用于关系型和非关系型数据源的接口
3. ODBC数据源是OLEDB的子集：ODBC OLE DB Provider
4. OLEDB只针对C++的API

#### 3.2.2.1. OLE DB中的COM对象
1. 数据源（Data Source）：对应于一个数据提供者，负责管理用户权限，建立与数据源的连接等初始操作
2. 会话（Session）：提供事务控制机制
3. 命令（Command）：执行各种数据操作，如查询命令、修改
4. 行集（RowSet）：数据的抽象表示，是应用程序的操作对象

### 3.2.3. ActiveX Data Object（ADO）
1. 建立在OLE DB之上,为操作OLE DB数据源提供了一套高层次自动化接口。ADO实际上是一个OLE DB客户程序，使用ADO的应用程序要间接地使用OLE DB
2. 提供了一种数据库编程对象模型，简化OLE DB，属高层的数据库接口，适用的编程语言更多

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/9.png)

#### 3.2.3.1. ADO（ActiveX Data Objects）
1. 一种与编程语言无关的面向对象的编程接口

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/10.png)

#### 3.2.3.2. ADO对象
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/11.png)

### 3.2.4. JDBC

#### 3.2.4.1. JDBC VS. ODBC
1. ODBC并不适合在Java中直接使用
2. 完全精确地实现从C代码ODBC到JavaAPI写的ODBC的翻译也并不令人满意
3. ODBC并不容易学习，它将简单特性和复杂特性混杂在一起，甚至对非常简单的查询都有复杂的选项；而JDBC刚好相反，它保持了简单事物的简单性，但又允许复杂的特性
4. JDBC这样的JavaAPI对于纯Java方案来说是必须的

#### 3.2.4.2. 四种JDBC驱动
1. 基于JDBC-ODBC桥的java驱动
2. 基于数据源本地驱动程序的虚拟java驱动
3. 基于网络驱动协议的java驱动
4. 纯java驱动

#### 3.2.4.3. 常用的JDBC接口/类
1. Java.sql.Driver：驱动程序实现的接口，提供连接数据库的基本方法
2. Java.sql.DriverManager：管理JDBC驱动程序，提供获取连接对象的方法，建立于数据库的连接
3. Java.sql.Connection：用于Java应用程序与数据库建立通信的对象，通过它进而创建Statement对象，执行SQL语句
4. Java.sql.Statement：对SQL语句进行封装的特定对象，用来执行SQL语句进行数据库操作
5. Java.sql.ResultSet：用于封装SQL语句查询的结果，是一个包含数据库记录的特殊对象

#### 3.2.4.4. 直接连接数据库的步骤
1. 建立数据源
2. 装载驱动程序
3. 建立连接
4. 建立语句对象
5. 执行SQL语句
6. 查询结果处理
7. 获取元数据
8. 关闭对象
9. 处理异常和警告

#### 3.2.4.5. 示例
```java
connection con=DriveManager.GetConnection("jdbc:odbc:people","examle","password");
//建立与数据库的连接
Statement stmt=con.createstatement();
//建立语句对象
ResultSet rs=stmt.executeQuery("SELECT a,b,c FROM Table1");
//运行SQL语句，返回数据//库操作结果
while(rs.next()){
  intx=getInt("a");//获得数据库表记录a项的值
  strings=getstring("b");//获得数据库表记录b项的值
  floatf=getFloat("c");//获得数据库表记录c项的值
}
```

### 3.2.5. Hibernate
1. 一种Java语言下的对象关系映射解决方案，一种自由、开源的软件
2. 用来把对象模型表示的对象映射到基于SQL的关系模型结构中去，为面向对象的领域模型到传统的关系型数据库的映射，提供了一个使用方便的框架
3. 不仅管理Java类到数据库表的映射，还提供数据查询和获取数据的方法

#### 3.2.5.1. Hibernate API中的接口
1. 提供访问数据库的操作（如保存、更新、删除和查询对象）的接口：Session、Transaction和Query
2. 用于配置Hibernate的接口：Configuration
3. 回调接口，使应用程序接收Hibernate内部发生的事件，并作出相关的回应：Interceptor、Lifecycle和Validatable
4. 用于扩展Hibernate的功能的接口，如UserType、CompositeUserType和IdentifierGenerator接口。需要时应用程序可以扩展这些接口。

#### 3.2.5.2. 个核心接口
1. Hibernate内部封装了JDBC、JTA和JNDI
2. Configuration接口：配置hibernate，根启动hibernate，创建SessionFactory对象
3. SessionFactory接口：初始化hibernate，充当数据存储源的代理，创建Session对象
4. Session接口：负责保存、更新、删除、加载和查询对象
5. Transaction：管理事务
6. Query和Criteria接口：执行数据库查询

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/12.png)

#### 3.2.5.3. 使用Hibernate的步骤
1. 创建Hibernate的配置文件
2. 创建持久化类
3. 创建对象-关系映射文件
4. 通过Hibernate API编写访问数据库的代码

# 4. 元数据与数据映射

## 4.1. 数据编码
1. 字符集
2. ASCII
3. 汉字编码
4. Unicode
5. UTP-8
6. 编码之间的关系

### 4.1.1. 字符集
1. Samuel F.B.Morse在1838年到1854年间发明了电
2. Braille代码：一种6位代码，它把字符、常用字母组合、常用单字和标点进行编码
3. Telex、Baudot以及CCITT #2代码都是包括字符和数字的5位代码
4. 6位字符码系统BCDIC（Binary-Coded Decimal Interchange Code），8位EBCDIC IBM大型主机
5. 美国信息交换标准码ASCII，1967年
6. DBCS：double-byte character set
7. Unicode解决方案

### 4.1.2. ASCII
1. 7个位所能提供的128个编码位置
2. 94个图形字符码和34个控制字元码
   1. 图形字符包括52个大小写英文字母﹑10个阿拉伯数字﹑9个标点符号﹑6个括号，以及17个其它符号，编码范围从33到126
   2. 控制字符则包括10个传输控制字符、6个版面调整字符、4个设备控制字元、4个信息分隔字符和10个特殊控制字符，其编码为0～32和127
3. 扩展ASCII

### 4.1.3. 汉字编码
1. GB2312 ：小于127的字符的意义不变，两个大于127的字符连在一起表汉字7000
   1. 高字节从0xA1用到0xF7，把01-87加上0xA0
   2. 低字节从0xA1到0xFE，把01-94加上0xA0
2. GBK：GB2312的扩展，主要扩展了繁体中文字的支持27000
3. GB18030：解决汉字、日文假名、朝鲜语和中国少数民族文字组成的大字符集计算机编码问题。总编码空间超过150万个编码位，收录了27484个汉字
4. BIG5：13,053个中文字，高位字节的编码范围0xA1-0xF9，低位字节的编码范围0x40-0x7E及0xA1-0xFE

### 4.1.4. Unicode
1. Universal Multiple-Octet Coded Character Set的简称，支持世界上超过650种语言的国际字符集
2. Unicode允许在同一服务器上混合使用不同语言组的不同语言
3. 由一个名为Unicode 学术学会(Unicode Consortium)的机构制订的字符编码系统，支持现今世界各种不同语言的书面文本的交换、处理及显示
4. Unicode是一种在计算机上使用的字符编码，为每种语言中的每个字符设定了统一且唯一的二进制编码，以满足跨语言、跨平台进行文本转换、处理的要求
5. Unicode通过增加一个高字节对ISO Latin-1字符集进行扩展，当这些高字节位为0时，低字节就是ISO Latin-1字符
6. Unicode中不同部分的字符都同样基于现有的标准，便于转换
7. 中国、日本和韩国的象形文字（总称为CJK）占用了从0x3000到0x9FFF的代码
8. Unicode只有一个字符集，没有歧
9. Unicode在制订时没有考虑与任何一种现有的编码方案保持兼容

### 4.1.5. 通用转换格式UTF-8
1. 用ASCII表示的字符使用UNICODE并不高效
2. 网络通讯时数据高低位的解读方式，核对双方对于高低位的认识是否是一致，标志符FEFF，EFBBBF for UTF-8。Byte Order Mark

```
UNICODE UTF-8
00000000 -0000007F 0xxxxxxx
00000080 -000007FF 110xxxxx 10xxxxxx
00000800 -0000FFFF 1110xxxx 10xxxxxx 10xxxxxx
```

3. 以转换后第1字节起头连续设为"1"的标记位的数目表示转换成几个字节，第2～第4字节起头两个位被设为10当做识别

### 4.1.6. 一个例子
1. 联通的内码
   1. c1 1100 0001
   2. aa 1010 1010
   3. cd 1100 1101
   4. a8 1010 1000
2. UTF8编码
   1. 0000 0000 0110 1010：j
   2. 0000 0011 0110 1000

## 4.2. 元数据在集成中的作用
1. 中央集线器确保Oracle电子商务套件与3个老的ERP系统之间一致的数据映射
2. 大量的企业数据要么深锁在数据库中，要么就被封闭在应用中
3. 随着企业跨应用组合不同的功能，这些数据模型也被混合在一起
4. 对数据而言，始终存在一种上下文关系甚至当一个字段为空白时，不同应用会对它的含意做出不同的假设

## 4.3. 什么是元数据
1. data about data
2. 通过一组属性或元素来描述特定的资源
3. 元数据模型提供了描述一类资源的具体对象时所有规则的集合
   1. 描述资源属性的术语：元数据元素
   2. 关系、结构约束、语法表示等
4. 提供规范、普遍的描述方法和检索工具，为分布的、由多种资源组成的信息体系提供整合的工具与纽带

## 4.4. DBMS的元数据
1. 某个数据库中的表和视图的个数以及名称
2. 某个表或者视图中列的个数以及每一列的名称、数据类型、长度、精度、描述等
3. 某个表上定义的约束
4. 某个表上定义的索引以及主键/外键的信息

## 4.5. SQL Server系统表与元数据
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/13.png)

## 4.6. 元数据的分类
1. 从元数据的作用角度
   1. 描述型元数据
   2. 结构型元数据
   3. 管理型元数据
2. 从信息系统的角度
   1. 业务元数据
   2. 技术元数据
   3. 操作元数据

### 4.6.1. 业务元数据
```
Title="Metadata Demystified"
Creator="Brand, Amy"
Subject="metadata"
Description="Presents an overview ofmetadataconventions inpublishing."
Publisher="NISO Press"
Date="2003-07"
Type="Text"
Format="application/pdf"
Identifier="http://www.niso.org/standards/resources/Metadata_Demystified.pdf"
Language="en"
```

## 4.7. 元数据的层次
1. 分层管理是解决复杂问题的一种思路。将资源按照一定的层次进行分类，便于管理
2. 元数据可应用于不同层次，可以定义全局的元数据，也可以定义某一层次资源的元数据
3. 可以在"计算机图书"类中加上"相关编程语言"这样一个属性

## 4.8. 元数据的功能
1. 描述和发现资源
2. 管理资源集合
3. 保存数字化资源
4. 提供数据互操作和数据转换方面的信息

### 4.8.1. 描述和发现资源
1. 允许通过相关的标准来发现资源
2. 标识资源
3. 把相似的资源放在一起
4. 识别不一样的资源
5. 提供定位（位置）信息

### 4.8.2. 保存数字化资源
1. 以一种统一和稳定的方式描述和组织存储在不同介质上的信息
2. 创建描述性元数据的一个重要原因就是要使相关信息的发现更加容易
3. 元数据是确保未来资源将存在并持续被访问的关键
4. 通过资源发现，元数据可以有助于电子资源的组织，使交互操作和遗产资源集成，提供数据标识和支持存档和保存变得更加容易

### 4.8.3. 数据互操作
1. 采用元数据来描述一个资源，允许资源在提升交互操作性的途径下被人和机器所理解
2. 交互操作就是在多个不同硬件和软件平台、数据结构和接口的系统之间最小内容和功能丢失的交换数据的能力
3. 利用被定义的元数据模式，被共享的协议和元数据模式之间的关联，跨网络的资源可以被无缝的查询

## 4.9. 元数据管理
1. 元数据创建
2. 元数据存储
3. 元数据交换
4. 元数据集成
5. 元数据监督
6. 元数据优化

## 4.10. 元数据管理的五种成熟度
1. 第一级随机状态
2. 第二级发现
3. 第三级管理控制
4. 第四级优化
5. 第五级自动化

## 4.11. Resource Description Framework
1. 一个用于描述Web 上的资源的框架
2. 针对数据的模型以及语法，供不同的用户来交换和使用
3. 使用XML 编
4. W3C 语义网络活动的组成部分，是一个W3C 推荐标准(2004 年2 月)
   1. 描述购物项目的属性，如价格以及可用性
   2. 描述Web 事件的时间表
   3. 描述有关网页的信息，比如内容、作者以及被创建和修改的日期
   4. 描述网络图片的内容和等级
   5. 描述针对搜索引擎的内容

### 4.11.1. RDF 规则
1. RDF 使用属性和属性值来描述资源
   1. 资源是可拥有URI 的任何事物，比如"http://www.w3school.com.cn/rdf"
   2. 属性是拥有名称的资源，比如"author" 或"homepage属性值是某个属性的值，比如"David" 或http://www.w3school.com.cn
   3. 描述资源"http://www.w3school.com.cn/rdf" 的RDF 文档

```xml
<?xml version="1.0"?>
<RDF>
  <Description about="http://www.w3school.com.cn/RDF">
    <author>David</author>
    <homepage>http://www.w3school.com.cn</homepage>
  </Description>
</RDF>
```

### 4.11.2. RDF 陈述
1. 资源、属性和属性值的组合形成一个陈述
2. 陈述："The author of http://www.w3school.com.cn/rdf is David."
   1. 主体：http://www.w3school.com.cn/rdf
   2. 谓语：author
   3. 客体：David

### 4.11.3. RDF 陈述
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/14.png)

### 4.11.4. 标准的资源描述框架
1. 描述所有元数据格式,解决元数据互操作性
   1. XML以一种标准化的方式来建立数据表示的结构
   2. RDF明确表达元数据的语义、句法和结构
2. 采用RDF Schema为RDF资源的属性和类型提供词汇表

## 4.12. 元数据映射
1. 信息系统的整合与交互性问题
   1. 同一领域的元数据标准
   2. 不同领域不同专业
2. 元数据标准映射：元数据分析、建立元数据对应关系字典、编制转换程序
3. 非实时映射：将源元数据系统的数据映射到目标元数据系统
4. 实时映射：根据元数据映射表建立转换接口

## 4.13. 元数据映射表
1. 元数据语义映射描述元数据标准中元素的对应关系
   1. 一对一关系
   2. 一对多关系
   3. 多对一关系
   4. 无对应关系
2. 元数据取值内容的映射关系
   1. 数据类型、取值范围、受控词汇
   2. 文本和数值类型间或文本和日期类型
   3. 自由文本和受控词，不同的受控词汇表

## 4.14. 元数据匹配差异
1. 必备元素与可选元素的差异
2. 可重复元素与不可重复元素的差异
3. 子元素差异
4. 元素层次错位

## 4.15. 元数据映射局限性
1. 元素之间无法完全映射，信息丢失
2. 随着元数据格式数量的增多，映射的工作量将大大增加

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/15.png)

## 4.16. 基于XSLT实现元数据映射
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/16.png)

## 4.17. 实施步骤
1. 盘点各系统的数据库,提取出元数据,设计出Schema确定其编码属性
2. 开发适配器,将源信息从关系数据库向XML文件转换
3. 确定集成信息的映射规则和编码属性的对照关系,利用XSLT实现源XML 文件向目标文件转换
4. 集成目标XML文件中的资源信息

## 4.18. 数据异构冲突
1. 命名冲突
   1. 同名异义、异名同义
   2. 全局命名映射
2. 格式异构
   1. 类型转换函数
3. 类型冲突
   1. 同一种数据类型精度不同
   2. 取舍

# 5. ETL技术

## 5.1. Extraction-Transformation-Loading
1. 原本是构建数据仓库的一个环节：将分布的、异构数据源中的数据如关系数据、平面数据文件等抽取到临时中间层后进行清洗、转换、集成，最后加载到数据仓库或数据集市中，成为联机分析处理、数据挖掘的基础
2. ETL是BI项目重要的一个环节,BI项目中，通常情况下ETL会花掉整个项目的1/3的时间
3. ETL也越来越多地应用于一般信息系统中数据的迁移、交换和同步

## 5.2. 数据仓库
1. 为决策支持服务的面向主题的、集成的并随时间变化的、相对稳定的数据集合
2. 面向主题：数据仓库中的数据按照主题进行组织
3. 集成：从多个数据源将数据集合到数据仓库中，并集成为一个整体；
4. 稳定：数据仓库中的数据通常是历史数据，很少进行更新；
5. 时变：数据仓库中的所有数据都有特定的时间标识.

## 5.3. 数据仓库、ODS和数据库的比较
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/17.png)

## 5.4. 数据仓库概念模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/18.png)

## 5.5. 数据仓库的结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/19.png)

## 5.6. 数据分析方法
1. 切片和切块(Slice and Dice)：多维数据结构中,按二维进行切片,按三维进行切块,可得到所需要的数据。如在"城市、产品、时间"三维立方体中进行切块和切片,可得到各城市、各产品的销售情况
2. 钻取(Drill)：钻取包含向下钻取(Drill-down)和向上钻取(Drill-up)/上卷(Roll-up)操作，钻取的深度与维所划分的层次相对应
3. 旋转(Rotate)/转轴(Pivot)：通过旋转可以得到不同视角的数据

### 5.6.1. 切片、切块
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/20.png)

### 5.6.2. 钻取
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/21.png)

### 5.6.3. 旋转
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/22.png)

## 5.7. 数据仓库的体系结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/23.png)

## 5.8. 数据仓库的元数据
1. 管理元数据
   1. 所有建立使用DW的信息，源数据库
   2. 综合数据、维、层次信息
   3. 预定义的查询、报表和数据组织、分段
   4. 数据抽取、清洗、转换的规则
2. 业务元数据
   1. 业务流程、数据的所有关系和存取控制策略
3. 操作元数据
   1. 运行时管理信息
   2. 即时数据信息、监测信息

## 5.9. 数据仓库的数据组织
1. 虚拟存储
   1. 语义层工具转换
   2. 适用理想状况
2. 基于关系表存储
   1. 模型定义、数据抽取
3. 多维数据库存储
   1. 多维数据文件存储数据
   2. 维索引管理

## 5.10. 维表（星型）
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/24.png)

## 5.11. 维表（雪花型）
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/25.png)

## 5.12. 数据仓库组成部分
1. 数据源
2. 数据抽取（extraction）、转换（transformation）和转载（load）工具
3. 数据建模工具
4. 核心仓储（Central Repository）
5. 数据仓库的目标数据库
6. 前端数据访问和分析工具
7. 数据仓库管理工具

## 5.13. 体系结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/26.png)

## 5.14. 数据集成领域中ETL
1. 数据的差异性更大, 不仅是结构化数据, 可能还涉及到半结构数据和无结构数据, 并实现某些情况下的相互转换
2. 数据抽取、转换和加载操作往往不在同一个地方, 在抽取和加载之间需要进行数据的远程传输
3. 抽取和加载两个操作可能是完全独立的, 分别属于不同的企业或部门,具有高度的自治性
4. 在数据仓库中一般只进行数据的增加,而数据集成应用可能还涉及到数据的删除和修改, 保证抽取方和加载方数据的一致性

## 5.15. ETL的过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/27.png)

1. 抽取、转换和加工、装载
2. 节点代表操作：过滤，转变，传输，压缩，加密等
3. 增量、转换、调度和监控等处理

### 5.15.1. 数据的抽取
1. 与目标数据库系统相同的数据源：建立链接关系就可以写Select语句直接访问
2. 与目标数据库系统不同的数据源
   1. 通过程序接口来完成
   2. 将数据导出成txt或者是xls文件，然后再将这些源系统文件导入到ODS中
3. 文件类型数据源(txt, xls)
4. 全量抽取和增量抽取：增量更新的问题

### 5.15.2. 数据的清洗
1. 数据格式不一致、数据输入错误、数据不完整
2. 源数据和目标数据需要进行数据模式或语义映射的转换
3. 在数据库中进行数据加工
   1. 利用数据库本身提供的SQL、函数
   2. 在SQL查询语句中添加where条件进行过滤
   3. 重命名字段名与目的表进行映射
   4. substr函数、case条件判断
4. ETL引擎：以组件化的方式实现数据转换：字段映射、数据过滤、数据清洗、数据替换、数据计算、数据验证、数据加解密、数据合并、数据拆分等

### 5.15.3. 数据装载
1. 将转换后的数据装载到目标库
2. 最佳方法取决于所执行操作的类型以及需要装入多少数据
3. 目的库是关系数据库有两种装载方式
   1. 直接SQL语句进行insert、update、delete操作，进行了日志记录并且可恢复
   2. 采用批量装载方法，如bcp、bulk、关系数据库特有的批量装载工具或api，批量装载操作易于使用，并且在装入大量数据时效率较高

## 5.16. ETL中的关键技术
1. 增量复制
2. 数据的清洗转换

### 5.16.1. 增量复制
1. 触发器
2. 时间戳
3. 快照方式
4. 日志法

#### 5.16.1.1. 控制表法（触发器）
1. 插入、修改、删除建trigger，每当源表中的数据发生变化，就被相应的触发器将变化的数据写入一个临时表
2. 控制表（变化表名、操作、主键、时间戳）

```sql
Create trigger tri_insert_teacher on teacher
  For insert
    As
      Begin
        Declare @KeyId in
        Select @ KeyId = id from inserted
        Insert into Record values(teacher,"insert",@KeyId ,getdate())
End
```

#### 5.16.1.2. 时间戳
1. 一种基于快照比较的变化数据捕获方式
2. 在源表上增加一个时间戳字段，系统中更新修改表数据的时候，同时修改时间戳字段的值
3. 当进行数据抽取时，通过比较系统时间与时间戳字段的值来决定抽取哪些数据
4. 有的数据库的时间戳支持自动更新，即表的其它字段的数据发生改变时，自动更新时间戳字段的值
5. 不支持时间戳的数据库则触发器方式

#### 5.16.1.3. 快照方式
1. 快照是数据在某个时刻的一个备份
2. 在上次发送时保留其快照, 在当前发送时, 可以通过比较当前数据与上次发送时的快照, 得到数据的增加、删除和修改情况
3. 将二者的区别按照要求发送出去

#### 5.16.1.4. 根据主键判断
1. 当前实视图为New，上次发送时的快照为Old, t为当前实视图中的一条记录
   1. 若$t_{key} \in New_{key}$但$t_{key} \notin Old_{key}$, 则t是增加数据
   2. 若$t_{key}\in Old_{key}$但$t_{key} \notin New_{key}$, 则t是删除数据
   3. 当$t_{ny} \not = \emptyset$时, 若$t_{key}\in New_{key}$且$t_{key}\in Old_{key}$, 但$t_{ny}\in New_{ny}$且$t_{ny} \notin Old_{ny}$, 或者$t_{ny}\in Old_{ny}$且$t_{ny} \notin New_{ny}$, 则t是修改数据

### 5.16.2. 数据的清洗转换
1. 过滤不符合要求的数据，将过滤的结果交给业务主管部门，确认是否过滤掉还是由业务单位修正之后再进行抽取
2. 数据清洗是一个反复的过程，注意不要将有用的数据过滤掉，对于每个过滤规则认真进行验证，并要用户确认
3. 数据转换主要进行不一致的数据转换、数据粒度的转换，以及一些商务规则的计算

#### 5.16.2.1. 数据清洗
1. 不完整的数据：一些应该有的信息缺失，如供应商的名称、客户的区域信息缺失、业务系统中主表与明细表不能匹配等；过滤出来写入不同Excel文件向客户提交，要求在规定的时间内补全
2. 错误的数据：业务系统不够健全，在接收输入后没有进行判断直接写入后台数据库造成的，比如数值数据输成全角数字字符、日期格式不正确、日期越界等；需要去业务系统数据库用SQL的方式挑出来，交给业务主管部门要求限期修正，修正之后再抽取
3. 重复的数据：将重复数据记录的所有字段导出，让客户确认并整理

#### 5.16.2.2. 姓名常见的错误和变化
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/28.png)

#### 5.16.2.3. 数据质量问题示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/29.png)

### 5.16.3. 清理、匹配、标准化
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/30.png)

### 5.16.4. 数据匹配与合并
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/31.png)

## 5.17. 数据转换
1. 不一致数据转换：将不同业务系统的相同类型的数据统一，如同一个供应商在结算系统的编码是XX0001,而在CRM中编码是YY0001，这样在抽取过来之后统一转换成一个编码
2. 数据粒度的转换：业务系统一般存储非常明细的数据，而目标数据是用来分析的，不需要非常明细的数据
3. 商务规则的计算：不同的企业有不同的业务规则、不同的数据指标，这些指标有时需要在ETL中将这些数据指标计算后存储在目标数据库中，以供分析使用

## 5.18. ETL的三种实现方法
1. 借助ETL工具：Oracle的ODI,SQL server 的SQL Server Integration Service：可以快速建立ETL工程，屏蔽了复杂的编码任务，提高的速度，降低的难度，但是缺少灵活
2. SQL方式实现：灵活，提高ETL运行效率，但是编码复杂，对技术要求比较
3. ETL工具和SQL相结合

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/32.png)

## 5.19. 提高ETL的性能
1. 如果条件允许利用数据中转区对运营数据进行预处理，保证集成与加载的高效性
2. 如果ETL的过程是主动"拉取"，而不是从内部"推送"，其可控性将大为增强
3. ETL之前应制定流程化的配置管理和标准协议
4. 关键数据标准至关重要

## 5.20. 实施ETL的例子
1. 往oracle数据库中插入excel文件中的数据

# 6. 基于XML的数据集成
1. 整个系统位于异构数据源和应用程序之间,向下协调各种数据源,向上为访问集成数据的应用提供了统一的模式和访问的通用接
2. 数据抽取层
3. 中介层
4. 用户接口层

## 6.1. 系统结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Data-Integration/img/integration/33.png)

## 6.2. 数据抽取层
1. 处于系统的最低层,是系统的数据提供者
2. 提取和集成分布在多个异构数据源(数据库,知识库及构件库) 上的数据
3. 采用Wrapper (包装器) 技术实现将一个从中介层得到的查询,翻译成能在经过封装的数据源上执行的操作,将查询结果抽取并打包到一个XML 文档,最后将该文档返回给中介层

## 6.3. 中介层
1. 一方面对上接受用户通过DOM(Document Object Model ,文档对象模型客户端API 向系统提交的或应用程序发出的查询,将其转换成对XML 的查询,并将查询结果返回给用户或应用程序
2. 另一方面对下将XML 查询分发给各个包装器,并将查询结果通过DTD 说明再转换成XML 格式

## 6.4. 用户接口层
1. 用户接口层(User Interface Layer) 在中介层之上,负责将用户的查询命令提交给中介层,获得并解释查询结果,并将结果显示给用户
2. 定义了XML文档的逻辑结构,访问及操作方法。由于数据显示与内容分开,XML 定义的数据允许指定不同的显示方式,使数据更合理的表现出来
3. 本地的数据能够以客户配置,使用者选择或其他标准决定的方式动态的表现出来