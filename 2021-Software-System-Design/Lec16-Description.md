lec16-Description
---
1. 梁鹏 武汉大学计算机学院

# 1. Overview
1. 什么是架构描述？ What is an architecture description?
2. ISO标准的体系结构描述 ISO standard for architecture description
3. 架构视图中的表示形式 Arch. representation in architecture views
4. 如何获取一组架构视图 How to obtain a set of architecture views

# 2. 什么是架构描述？What is an architecture description?

## 2.1. UML中的软件设计 Software design in UML
1. 类图，状态图，顺序图等 Class diagrams, state diagrams, sequence diagram, etc
2. 谁能看懂那些图表？ Who can read those diagrams?
3. 他们回答哪种类型的问题？Which type of questions do they answer?
4. 他们提供足够的信息吗？ Do they provide enough information?

### 2.1.1. Who can read those diagrams?
1. 设计人员，程序员，测试人员，维护人员等 Designer, programmer, tester, maintainer, etc
2. 客户？Client?
3. 用户？User?

### 2.1.2. 他们回答哪种类型的问题？Which type of questions do they answer?
1. 它要花多少钱？How much will it cost?
2. 系统的安全性和可靠性如何？How secure and reliable will the system be?
3. 维修费用如何？How about maintenance cost?
4. 如何发展系统以满足新的需求？How to evolve the system to meet new requirements?
5. 如果将需求A替换为需求B怎么办？What if requirement A is replaced by requirement B?

## 2.2. 建筑结构 Building architecture
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/1.png)

## 2.3. 类比建筑 Analogy with building architecture
1. 建筑物总体图（客户）Overall picture of building (client)
2. 前视图（客户，“美容”委员会）Front view (client, "beauty" committee)
3. 水的独立图片（水管工）Separate picture for water supply (plumber)
4. 电气接线图（电工）Separate picture for electrical wiring (electrician)
5. 等等 etc

## 2.4. 实践中的架构演示 Architecture presentations in practice
1. 大体上有两种口味：By and large two flavors:
   1. Powerpoint幻灯片（框和行）–适用于经理，用户，顾问等 Powerpoint slides (box and line) – for managers, users, consultants, etc
   2. 适用于技术人员的UML表示法中的UML图 UML diagrams in UML notations, for technicians
2. 实践中的一小部分 A small sample in practice …

### 2.4.1. Eclipse 1.0 architecture
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/2.png)

### 2.4.2. Eclipse 3.0 architecture (evolution)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/3.png)

### 2.4.3. 问题
1. 从Eclipse 1.0到3.0，其软件体系结构设计的主要变化是什么？为什么？

### 2.4.4. Earth Observing System
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/4.png)

### 2.4.5. Decision-Making System
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/5.png)

### 2.4.6. ebXML Framework
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/6.png)

### 2.4.7. So
1. 不同的表示 Different representations
2. 对于不同的人 For different people
3. 为了不同的目的 For different purposes

# 3. ISO标准的体系结构描述 ISO standard for architecture description

## 3.1. 架构描述的概念模型[摘自ISO Std 42010] Conceptual model of architecture description [from ISO Std 42010]
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/7.png)

## 3.2. 考虑将模型作为模板 Think about model as template
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/8.png)

## 3.3. 问题
1. 不同涉众（stakeholders）有不同的关注点，从不同的视角（viewpoints）来看待系统的体系结构设计，是否能采用同一种描述方式来描述系统？

## 3.4. 一些术语/定义（来自ISO标准）Some terms/definitions (from ISO standard)
1. 系统利益相关者：个人，团队，组织或其类，对系统感兴趣的任何人 System stakeholder: individual, team, organization, or classes thereof, anyone having an interest in a system
2. 视图：从特定系统关注点的角度表达系统的体系结构 View: expresses the architecture of a system from the perspective of specific system concerns
3. 视角：建立用于构造，解释和使用体系结构视图的约定，以构架特定的系统问题 Viewpoint: establishes the conventions for the construction, interpretation and use of architecture views to frame specific system concerns
4. view : viewpoint :: program : programming language
5. view : viewpoint :: map : legend

## 3.5. 可能的担忧（ISO标准的质量保证） Possible concerns (QAs from ISO standard)
1. 外部质量 External quality
   1. 开发费用 Development cost
   2. 客户体验（可用性）Customer experience (usability)
   3. 可用性 Availability
   4. 表现 Performance
2. 内部质量 Internal quality
   1. 进化性 Evolvability
   2. 可维护性 Maintainability
   3. 可测性 Testability
   4. 可变性 Changeability

## 3.6. The twin peaks 双子峰
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/9.png)

## 3.7. 质量属性方案 Quality attribute Scenarios
1. 通过定义适当的方案，可以使质量属性更智能 Quality attributes can be made SMART by defining appropriate scenarios
2. 质量属性方案的定义如下：Quality attribute scenarios are defined by:
   1. 刺激的源头：人还是机器 The source of the stimulus: Human or machine
   2. 刺激（事件）The stimulus (event)
   3. 刺激发生的环境或条件 The environment or condition where the stimulus occurs
   4. 响应度量：时间，价值和位置 The response measure: Time, value and location
3. 系统的非功能属性可以基于应用场景（scenarios）来量化

## 3.8. 建筑设计中的场景是什么 What is a scenario in architecture design
1. 场景是从开发和最终用户的角度对系统的预期或预期使用的简要叙述。Scenarios are brief narratives of expected or anticipated use of a system from both development and end-user viewpoints.
2. 从开发和用户视角来看系统的使用
3. 是关于系统使用的具体描述
4. 超市系统每晚12点备份当天交易数据
5. 查看双11 22点峰值的红包堵塞节点

## 3.9. 性能方案示例 Example Performance Scenarios
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/10.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/11.png)

## 3.10. 重要的业务相关质量保证 Important business-related QAs
1. 上市时间 Time-to-market
2. 成本价 Cost price
3. 投资回报率（ROI） Return on Investment (ROI)
4. 总拥有成本（TCO） Total Cost of Ownership (TCO)
5. 系统寿命 Lifetime of the system
6. 与现有（旧版）系统集成 Integration with existing (legacy) systems
7. 营销特色 Marketing features
8. 等等。Etc.

## 3.11. 重要的设计时质量保证 Important Design-time QAs
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/12.png)

## 3.12. 重要的运行时质量保证 Important Run-time QAs
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/13.png)

## 3.13. 体系结构描述的上下文[摘自Std 42010] Context of architecture description [from Std 42010]
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/14.png)

## 3.14. 利益相关者 Stakeholders
1. 顾客 Customer
2. 用户 User
3. 建筑师 Architect
4. 需求工程师 Requirements engineer
5. 设计师 Designer
6. 实施者 Implementer
7. 测试仪，积分仪 Tester, integrator
8. 维护者 Maintainer
9. 产品经理 Product manager
10. 质量保证人 Quality assurance people

## 3.15. 视角规范 Viewpoint specification
1. 视点名称 Viewpoint name
2. 利益相关者 Stakeholders addressed
3. 解决的问题 Concerns addressed
4. 语言，建模技巧 Language, modeling techniques

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/15.png)

### 3.15.1. 示例视图：Sagitta 2000的上下文视图 Example view: context view of Sagitta 2000
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/16.png)

### 3.15.2. 视点定义示例 Example viewpoint definition
1. 名称：上下文视角 Name: Context viewpoint
2. 利益相关者：系统所有者，维护者 Stakeholders: system owners, maintainers
3. 关注点：系统边界，变更影响 Concerns: system boundaries, effect of changes
4. 语言：UML变体 Language: UML variant

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/17.png)

# 4. 架构视图 Architecture views

## 4.1. 视角和视角的关键概念 Key concepts of views and viewpoints
1. 视角涵盖一个或多个关注点 A viewpoint (视角) covers one or more concerns
2. 视角分离关注点 Viewpoints separate concerns (关注点)
3. 视图（view）符合观点 A view (视图) conforms to a viewpoint
4. 视图由一个或多个模型（模型）组成 A view consists of one or more models (模型)
5. 架构描述以一个或多个视图（一个或多个视图构成）进行组织 An architecture description is organized in one or more views (一个或一组视图构成)

## 4.2. 4 + 1视图模型 The 4 + 1 view model
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/18.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/19.png)

## 4.3. 5种架构视图 The 5 architecture views
1. 用例视图（外部-参与者查看的系统）推动架构发展的关键场景。 发现，设计和验证定义功能和QA并转化为需求 Use–case view (external - the system viewed by an actor) Key scenarios that drive arch. discovery, design & validation Define functionality & QAs and translate into requirements
2. 逻辑视图（内部）：系统的功能，结构和行为 Logical view (internal)：Functionality, structure and behavior of the system
3. 进程视图（内部）：并发，通信。 和运行时同步 Process view (internal)：Concurrency, comm. & synchronization at runtime
4. 部署视图（内部）：将组件映射到处理平台 Deployment view (internal)：Mapping of components onto processing platforms
5. 实施视图（内部）：实施细节 Implementation view (internal)：Implementation details
6. 用例定义了待开发系统的范围

## 4.4. UML用于 4+1 软件体系结构视图描述

### 4.4.1. Example of use case view 用例视图示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/20.png)

### 4.4.2. （4 +1）：逻辑/概念观点 (4 + 1): Logical/Conceptual Viewpoint
1. 逻辑观点支持功能需求，即系统应向最终用户提供的服务。 The logical viewpoint supports the functional requirements, i.e., the services the system should provide to its end users.
2. 通常，它显示关键抽象（例如，类和它们之间的交互）。 Typically, it shows the key abstractions (e.g., classes and interactions amongst them).

### 4.4.3. 逻辑视图示例 Example of logical view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/21.png)

### 4.4.4. （4 +1）：流程观点 (4 + 1): Process Viewpoint
1. 流程观点提供了功能到运行时元素的映射 The process viewpoint gives the mapping of functions to runtime elements
2. 它考虑了一些非功能性需求，例如性能，系统可用性，并发和分发，系统完整性和容错能力。It takes into account some nonfunctional requirements, such as performance, system availability, concurrency and distribution, system integrity, and fault-tolerance.

### 4.4.5. 流程视图示例 Example of process view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/22.png)

### 4.4.6. （4 +1）：实施观点 (4 + 1): Implementation Viewpoint
1. 实施观点着眼于软件开发环境中实际软件模块的组织。 The implementation viewpoint focuses on the organization of the actual software modules in the software-development environment.
2. 该软件打包在一个小块的程序库或子系统中，可以由一个或多个开发人员开发。 The software is packaged in small chunks-program libraries or subsystems-that can be developed by one or more developers.

### 4.4.7. 实施视图示例 Example of implementation view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/23.png)

### 4.4.8. （4 +1）：部署视点 (4 + 1): Deployment Viewpoint
1. 部署视点定义了逻辑，流程和实现视点中标识的各种元素如何将网络，流程，任务和对象映射到各个节点上。 The deployment viewpoint defines how the various elements identified in the logical, process, and implementation viewpointsnetworks, processes, tasks, and objects-must be mapped onto the various nodes.
2. 它考虑了系统的非功能性需求，例如系统可用性，可靠性（容错），性能（吞吐量）和可伸缩性。 It takes into account the system's nonfunctional requirements such as system availability, reliability (fault-tolerance), performance (throughput), and scalability.

### 4.4.9. 部署视图示例 Example of deployment view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/24.png)

## 4.5. 在UML中使用4 + 1视图 Using 4 + 1 view in UML
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/25.png)

## 4.6. 模型的可追溯性 Traceability of Models
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/26.png)

## 4.7. 4 + 1视图中的Rational Rose Rational Rose in 4+1 view
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/27.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/28.png) |
| -------------------- | -------------------- |

## 4.8. 横切观点 Crosscutting viewpoints (交叉的体系结构视图)
1. 安全性在功能视图中显示为用户身份验证，在部署视图中显示为防火墙 Security shows up in functional view as user authentication, and in deployment view as firewall
2. 性能在组件耦合的功能视图中显示，在部署视图中作为分布式拓扑显示 Performance shows up in functional view in component coupling, in deployment view as distributed topology
3. 架构视图之间的一致性很重要，但是很难维护（可追溯性会有所帮助）Consistencies between architecture views are important , but difficult to maintain (traceability helps)

## 4.9. 架构视图中的问题/陷阱 Problems/pitfalls in architecture views
1. 接口定义不正确 Poorly defined interfaces
2. 对责任的理解不深 Poorly understood responsibilities
3. 重载视图 Overloading the view
4. 只是画图 Just drawing the picture
5. 详细程度不当 Inappropriate level of detail
6. “上帝”元素 "God" elements

## 4.10. 示例重载视图 Example overloaded view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/29.png)

## 4.11. 项目中的架构视图 Architectural views in your projects
1. 一种观点应该从（部分或全部）外部利益相关者的角度关注系统 One viewpoint should focus on the system from the perspective of (some or all) external stakeholders
2. 观点之一应该是技术观点。 One of the viewpoints should be a technical viewpoint.
3. 如何以一种易于理解的方式表达利益相关者的业务问题？ How to express business concerns of stakeholders in an understandable way?
4. 往年的一些很好的例子：Some good examples from previous years:
5. 软件体系结构文档中的视图要求

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/30.png)

# 5. 如何获得一套体系结构视图 How to obtain a set of arch. views

## 5.1. 如何决定哪些观点 How to decide on which views
1. 从业务目标入手 Start with business goals
2. 利益相关者及其关注的是什么？ What are the stakeholders and their concerns?
3. 哪些观点解决了这些问题？ Which views address these concerns?
4. 优先考虑并可能合并视图（关键驱动因素）Prioritize and possibly combine views (key drivers)

## 5.2. 业务目标类别[第16章] Categories of business goals [Ch 16]
1. 组织的成长和连续性 Organization’s growth and continuity
2. 达到财务目标 Meeting financial objectives
3. 达到个人目标 Meeting personal objectives
4. 履行员工责任 Meeting responsibility of employees
5. 履行对国家的责任 Meeting responsibility to country
6. 履行对社会的责任 Meeting responsibility to society
7. 履行对股东的责任 Meeting responsibility to shareholders
8. Managing market position
9. Improving business processes
10. Managing product’s quality and reputation

## 5.3. Example business goal
1. Stakeholder: we want to provide users with a reliable, securer way to access government services online
   1. Goal subject: project manager
   2. Goal object: population
   3. Environment: user population’s computing skills
   4. Goal: provide users with reliable access
   5. Goal measure: system operates 24/7, no loss of confidential data
   6. Possible architectural approach: quality reqs for usability, data confidentiality, reliability, availability

## 5.4. Define a viewpoint
1. Primary presentation (graphical or textual)
2. Element catalog
3. Variability guide
4. Glossary of terms
5. Other information

## 5.5. Documentation using views
1. What the architecture is using views
2. Why the architecture is the way it is

## 5.6. Example of context viewpoint
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/31.png)

## 5.7. Example of context view
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec16/32.png)

## 5.8. What is a good arch. description?
1. Explicit vision, design decisions, and rationales
2. Essential information only on a minimum of pages
3. Traceability & up-to-date

## 5.9. Read
1. Bass et al, Ch 18: Documenting SA
2. ISO standard 42010
3. Kruchten’s IEEE Software article
4. Bass et al, Ch 16: Architecture and Requirements

# 6. Summary
1. An architecture has different stakeholders, with different concerns
2. To properly address these stakeholders and their concerns, we need different architecture views and representations