Lec6-软件架构演化与最新进展
---

# 1. 架构历史
1. C/S架构，进一步改进得到B/S架构(Broswer/Server架构)
2. B/S架构
3. 服务端MVC架构
4. 客户端MVC架构
5. 服务端-N层架构：展示层、业务层、持久层、数据库

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/1.png)

6. SOA架构
   1. 服务封装
   2. 服务松耦合：服务之间的关系最小化，仅互相知道
   3. 服务契约：服务按照服务描述文档所定义的服务契约行事
   4. 服务抽象：除了服务契约中所描述的内容，服务将对外部隐藏逻辑
   5. 服务的重用性：将逻辑分布在不同的内容中，以提供服务的重用性
   6. 服务的可组合性：一组服务可以协调工作并组合起来形成一个组合服务
   7. 服务自治：服务对所封装的逻辑具有控制权
   8. 服务无状态：服务将一个活动所需保存的资讯最小化
   9. 服务的可被发现性：服务需要对外部提供描述资讯，这样可以通过现有的发现机制发现并访问这些服务
7. ESB(Enterprise Service Bus)

# 2. 应用架构演进趋势
1. 企业应用机构演进：大型机时代 -> 客户端服务端时代 -> Web时代 -> 分布式时代

## 2.1. 单体架构
1. 优点：为人熟知、IDE友好、便于共享、易于测试、容易部署。
2. 缺点：不顾灵活、妨碍持续交付、受技术栈限制、技术债务积累、性能、可用性、伸缩性、扩展性、安全性。

## 2.2. 架构设计策略
1. 缓存与读写分离

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/2.png)

2. 动静分离

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/3.png)

3. 集群化高可用架构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/4.png)

4. 业务拆分与分布式

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/5.png)

5. 微服务架构

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/6.png)

## 2.3. 微服务架构
1. 微服务架构的特点
   1. 每个微服务可独立运行在自己的进程中
   2. 每个微服务只服务于某个特定的业务进程
   3. 微服务之间通过一些轻量的通信机制进行通信，如REST API
   4. 可以使用不同的语言和数据存储技术
   5. 全自动的部署/监控/运维机制
2. 微服务的理念：分而治之

## 2.4. AKF可扩展性模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/7.png)

1. AKF扩展原则
   1. 理论上按照三种扩展模式可以将单体系统进行无限扩展。
   2. X轴：水平复制，配合负载均衡
   3. Z轴：数据分区，不同地区有不同的数据分区
   4. Y周：微服务的拆分模式，基于不同的业务进行拆分
2. 微服务的原则
   1. 围绕业务概念建模
   2. 自动化文化
   3. 隐藏内部实现细节
   4. 一切都去中心化
   5. 独立部署
   6. 隔离失败
   7. 高度可观察

## 2.5. 应用架构比较
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/8.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/9.png) |
| ------------------- | ------------------- |

# 3. 云原生简介
1. 云原生的代表技术包括**容器、服务网格、微服务、不可变基础设施和声明式API**。
2. 云原生是一种基于微服务的软件架构思想以及基于Devops进行软件开发实践的一组方法论，其实现了以分布式和容器技术为核心在异构云平台环境下利用云计算交付模型优势来快速构建、部署和进行企业应用。
3. 业界选择云原生的原因
   1. 更高的资源效率可以用更少的服务器运行相同数量的服务
   2. 云原生基础设施提高了开发速度
   3. 云原生支持多种云和混合云开发
   4. 云原生使得快速部署成为可能

## 3.1. K8S
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/10.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/11.png) |
| -------------------- | -------------------- |

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/12.png)

## 3.2. 应用上云
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/13.png)

1. Devops的本质：文化建设、流程规范、技术规范、工具支撑。

# 4. 微服务治理

## 4.1. 微服务架构转型遇到的挑战
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/14.png)

## 4.2. 分布式追踪
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Devops-introduction/img/lec6/15.png)

1. Skywalking核心概念和组件
   1. 两个维度
      1. Tracing 追踪链路数据
      2. Metrixs 指标数据
   2. 三个层级
      1. Receiver 接收器：解析和适配不同协议
      2. Analysis Core 分析内核：OAL
      3. Query Core 内核：多维度数据查询

# 5. 微服务设计

## 5.1. 微服务设计原则
1. 大平台
   1. 以业务分层方式将核心业务功能沉淀到平台中
   2. 采用微服务架构,支持互联网使用场景
   3. 采用持续交付平台,更好支撑先有研发流程,并提升效率
   4. 采用敏捷基础架构,更好支撑微服务架构应用
   5. 采用统一监控运维平台,提升运维自动化水平和效率
2. 微应用
   1. 只包含特定业务逻辑和展现
   2. 支持多种触点方式
   3. 支持快速创新与试错
