lec13-Quality Attributes
---

# 1. 软件架构 Software Architecture
1. **软件架构**是结构和系统结构，包含了软件**元素**、这些**组件**的外部可视化**属性**以及他们之间的**关系**。Software Architecture is the structure or structures of the system, which comprise software elements, the externally visible properties of these components, and the relationship among them.(In pratice书中的定义)
2. 单独的盒式模型不是架构，但是是一个开始的点 Box-and-line drawings alone are not architecture, but a starting point.
3. 架构包含了组件的行为 Architecture includes behaviour of components.

## 1.1. 架构扮演的角色 Role of Architecture
1. 架构是代表决定**如何实现需求**的决策的**第一批人工制品**。作为早期设计决策的体现，架构代表了那些**最难**更改的设计决策，因此值得**最仔细的考虑** An architecture is one of the first artefacts that represents decision on how requirements are to be achieved. As the manifestation of early design decisions, the architecture represents those design decisions that are hardest to change and hence deserve the most careful consideration.
2. 架构是成功完成产品线工程，与独立开发每个系统相比，以较少的工作量，成本和风险来有序地开发一系列相似系统的关键要素 An architecture is the key artefact in achieving successful product line engineering, the disciplined development of a family of similar system with less effort, expense, and risk than developing each system independently.
3. 当有人开始在系统上工作时，架构通常是首先要检查的设计工件 An architecture is usually the first design artefact to be examined when someone starts working on a system.
4. 软件架构为**维护和修改**决策提供了参考**框架** Software architecture provides a framework of reference for maintenance and modification decisions.

## 1.2. 为什么软件架构是重要的 Why is software architecture important?
1. 软件架构提供了**沟通的工具** Software architecture provides a vehicle for communication
   1. 软件架构是一个可以确定和谈判利益冲突的参考框架 It is a frame of reference in which competing interests may be identified and negotiated
      1. 和用户**讨论需求** Negotiating requirements with users
      2. **保证**客户获取到过程和成本的**信息** Keeping customer informed of progress, cost etc.
      3. **实现决策**和分配的管理 Implementing management decisions and allocations.
2. 软件架构表现了**最早期的决策集合** Software architecture manifests the earliest set of design decisions
   1. 约束着实现和开发者 It constraints the implementation and developers
      1. 实现必须要**符合架构** Implementation must contorm to architecture
      2. **资源分配的决策**约束着单独模块的实现 Resource allocation decisions constrain implementations of individual components
3. 表现了早期的设计决策 Manifestation of early design decisions
   1. 软件架构体现为了开发和维护工作的**组织结构** Software architecture dictates organisational structure for development & maintenance efforts, e.g.
      1. 划分为**团队** Division into teams
      2. **预算**，计划单位 Units for budgeting, planning
      3. 基础的**工作拆分架构** Basis of **W**ork **B**reakdown **S**tructure
      4. **文档**的组织 Organisation for documentation
      5. **CM**库的组织 Organisation for CM libraries
      6. **集成**的基础 Basis of integration
      7. **测试**计划、测试的基础 Basis of test plans, testing
      8. 运维的**基础** Basis of maintenance
4. 架构促进/阻碍**质量属性的实现**，比如灵活性、安全性、易用性 Architecture facilitates/ hinders achievement of quality attributes, e.g.modifiability, security, usability etc.
5. 架构会影响质量，但由于涉及许多其他因素，因此可能**无法保证**质量。Architecture influences qualities, but may not guarantee them as there are a number of other factors involved.
6. 架构引发有关**潜在变更**的讨论(系统的80％的工作是**部署后**的工作) An architecture invokes discussion about potential change ( 80% of effort for a system is post-deployment effort)
7. 架构将**更改**分为三种类型 Architecture categorise changes into three types:
   1. **本地**：信号组件修改 Local: signal component moditication
   2. **非本地**：几个组件修改。Non-local: several component moditication.
   3. **架构**：修改系统的基本结构，通信和协调机制 Architectural: modification of the system's basic structure, communication, and coordination mechanism
8. 架构是一种**可迁移**和**可重用**的抽象：**一对多映射**(一种架构，许多系统) Architecture is a transferable and reusable abstraction one-to-many mapping (one architecture, many systems)
9. 架构是**产品通用性**的基础。整个产品线共享一个架构 Architecture is the basis for product commonality. A whole product line shares a single architecture
10. 可以通过体系结构集成独立开发的组件来开发系统(基于Component的软件工程-CBSE) Systems can be developed by integrating independently developed components via architecture ((Component-Based Software Engineering - CBSE)

## 1.3. 软件架构过程 Software Architecture Process
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/1.png)

1. 通过StackHolder获取到ASRs(架构攸关的需求)
2. 通过分析得到Prioritized Quality Attribute Scenarios(高优先级质量属性解决方案)和Requirements，Constraints(需求和约束)
3. 将上述部分，结合模式和策略，综合可以得到架构的设计
4. 根据架构的设计得到由模式决定的候选视图的示意图，之后完成文档化
5. 选择、组合视图，将文档进行进一步的评估，这一部分需要StackHolders的参与、也需要Prioritized Quality Attribute Scenarios和文档等作为参考。

### 1.3.1. 移动手机系统架构 Mobile Phone System Architecture
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/2.png)

### 1.3.2. 洗衣机架构 Washing Machine Architecture
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/3.png)

## 1.4. 讨论 Discussion
1. 科学和工程有什么不同？What is Difference between Science and Engineering? 
   1. 科学的研究是研究这个世界既有的部分
   2. 工程是研究的是人类创造新的世界(是不是因为人才产生的)
2. 软件和硬件有什么不同？What is Difference between 'Software' and 'Hardware' ?
   1. 软件是不可见的：软件是虚拟的，而硬件是实体的。
   2. 软件制作出来就是为了被修改和改变的(软件的演化是他的本质属性)
3. 体系结构和设计有什么不同？What is Difference between Architecture and Design?
   1. 所有的体系结构都是软件设计，但是不是所有的软件设计都是体系结构
   2. 体系结构是设计过程的一个过程。
   3. 其他观点
      1. 体系结构是更高层的设计，是为了修改的
      2. 体系结构是设计决策的组合
4. 体系结构和结构有什么不同？What is Difference between Architecture and Structure?
   1. 体系结构定义了组件(Component)的接口，Component之间如何交流以及如何相互依赖，Component的职责。
   2. 体系结构提供了设计的更高层抽象视角，隐藏设计的复杂性和实现，更强调非功能性需求。
   3. 【标准】架构是包括结构信息的，因为结构是一种静态的、逻辑的、是关于系统如何构成。但是架构除了包含结构，还会增加组件的相互之间的关系接口，还会定义一些动态的行为(一个组件可能和谁进行交互)
5. 为什么要在架构中使用抽象？Why Abstraction in Architecture?
   1. 更高层的视角，更关注本身的结构而不是本身的实现。
   2. **降低**架构设计时的系统复杂度，可以屏蔽和**隐藏**一些细节。

# 2. 需求 Requirements
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/4.png)

需求中往往存在有开发人员和用户的矛盾，我们需要将这一个部分进行转化

## 2.1. 功能性需求 Functional Requirements
1. 功能性需求定义了**系统必须做什么**并且强调了**系统如何提供价值**给涉众 Functional requirements state what the system must do and address how the system provides value to the stakeholders.
2. 功能性需求意味着**系统的行为** Functional requirements means the behaviour of the system.
3. 功能是系统**完成其预期工作**的能力，例如，使学生能够在线注册。Functionality is the ability of the system to do the work for which it was intended, e.g., enable students to enrol online.
4. 通过使用**许多可能的结构**可以实现功能。Functionality may be achieved through the use of any
number of possible structures.
5. 功能在很大程度上与结构无关，因为它可以作为单个整体系统存在而没有任何内部结构。Functionality is **largely independent of structure**, because it could exist as a single monolithic system without any internal structure.

## 2.2. 质量需求 Quality Requirements
1. 质量需求是系统应**在其功能要求之上**提供的整个系统的**合乎需要的特性**(又称质量属性) Quality requirements are desirable characteristics of the overall system (aka. quality attrilbutes) that system should provide on the top of its functional requirements.
2. 质量要求是功能要求或整个产品的**资格**。软件体系结构限制了分配 Quality requirements are qualifications of the functional requirements or of the overall product.
3. 如果质量属性很重要，则将**功能**(映射)到各种**结构**上。Software architecture constrains the allocatio (mapping) of the functionality onto various structures if quality attributes are important.

### 2.2.1. 非功能性需求 Non-functional Requirements
1. **非功能**要求或**体系结构**要求是用于**质量属性**的替代术语 Non-functional requirements or architectural requirements are alternative terms used for quality attributes.
2. 无法正确使用功能，然后尝试适应非功能性要求(**不具备翻新质量**)。It is not possible to get the functionality right and then try to accommodate non-functional requirements (NO retro-fitting quality).
3. 在任何设计决策中都必须考虑非功能性要求。Non-functional requirements must be taken into account during any design decision.
4. 非功能性需求分为两大类：There are two broad categories ot non-functional requirements:
   1. 在执行过程中**可观察**(**外部**)：系统满足其行为要求的程度如何？ 例如性能，安全性，可用性，可用性等。Observable (External) during execution: How well a system satisties its behavioural requirements? e.g., performance, security, availability, usability etc.
   2. 执行期间**不可观察**(**内部**)：系统的维护，集成或测试有多容易？ 例如，可修改性，可移植性，可重用性，可测试性等。Not observable (Internal) during execution: How easily a system can be maintained, integrated, or tested? e.g., modifiability, portability, reusability, testability etc.
5. 约束了限定的边界，之后的架构是在这个边界内找到最优的解。

### 2.2.2. 质量属性 Quality Attributes
1. **开发完成后**，质量**不能**添加到软件密集型系统中 Quality isn't something that can be added to a software intensive system after development finishes.
2. 在**软件开发的所有阶段**都需要解决质量问题 Quality corncerns need to be addressed during ALL phases of the software development.
3. 业务目标确定系统必须具备的质量。Business goals determine qualities that a system must posses.
4. 质量属性是**系统功能的基础**，而功能是系统功能，服务和行为的基本说明 Quality attributes are over and above of system's functionality, which is the basic statement of the system's capabilities, services, and behaviours.
5. 功能通常在开发计划中占据**重要位置** Functionality usually takes the front seat in the development plan.
6. 但是，系统通常是**重新设计**的，因为它们**缺乏所需的质量级别**，即难以维护，移植或扩展 However, systems are usually redesigned because they lack desired level of quality, i.e. difficult to maintain, port, or scale.
7. 软件体系结构限制了各种质量属性的实现，例如性能，安全性，可用性等 Software architecture constrains the achievement of various quality attributes, e.g., performance, security, usability etc.
8. 这就是为什么软件体系结构被认为是解决质量问题的最合适的层次 That is why software architecture is considered the most appropriate level of addressing the quality Issues.
9. 质量属性不完全取决于**设计**，也不取决于**实现或部署** No quality attribute is entirely dependent on design, nor is it dependent on implementation or deployment.

### 2.2.3. 确定质量属性 Specifying Quality Attributes
1. 要在架构级别对其进行**评估**，必须对质量属性进行**精确定义**。Precise definition of a quality attribute is necessary to evaluate it at the architecture level.
2. 质量属性**方案**用于定义所需的质量属性。Quality attribute scenarios are used to define the desired quality attribute.
3. 方案是具有一定结构的简单句子。场景的两个主要类别是：Scenarios are simple descriptions with certain structure. Two main classes of scenarlos are:
   1. **通用方案**是与**系统无关**的方案，用于指导质量属性要求的规范 General scenarios are system independent scenarios to guide the specification of quality attribute requirements.
   2. **具体方案**是系统**特定**方案，用于指导特定系统的质量属性要求的规范。它们是一般方案的**实例** Concrete scenarios are system specitic scenarios to guide the specification of quality attribute requirements tor a particular system. They are instances ot general scenarlos.
4. 这个方案就是4+1视图中的1(Use Case)

#### 2.2.3.1. 通用方案 General Scenarios
1. 通用方案提供了一个**框架**，用于生成**大量**通用的，独立于系统的，质量属性特定的方案。General scenarios provide a framework for generating a large number of generic, system- independent, quality attribute specific scenarios.
2. 每种情况都可能但不一定与我们所关注的系统相关。Each scenario is potentialy but not necessarily relevant to the system We are concerned with.
3. 为了使一般情况对特定系统有用，我们必须使它们**特定于系统**。To make the general scenario useful for a particular system, We must make them system specific.
4. 使通用场景系统特定于特定环境意味着将其**转换**为特定系统的具体术语。Making a general scenario system specific means translating it into concrete terms for the particular system.

#### 2.2.3.2. 质量属性方案建模 Modeling Quality Attribute Scenarios 重要
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/5.png)

1. 刺激(Stimulus)：到达系统时需要考虑的**条件** Stimulus: A condition that needs to be considered when it arrives at a system.
2. 刺激源(Source of Stimulus)：产生刺激的**实体**(人，系统或任何促动器) Source of Stimulus: An entity (human, system, or any actuator) that generates the stimulus.可能是输入、消息等等，对当前的状态有一个变化。
3. 应对(Response)：刺激措施到来之后开展的**活动** Response: The activity undertaken after the arrival of the stimulus.
4. 响应度量(Response Measure)：对刺激的响应应以某种方式进行**测量**，以便可以**测试**需求。Response Measure: The response to the stimulus should be measurable in some fashion so that the requirement can be testable.多长时间系统有反馈
5. 环境(Environment)：发生刺激时系统的状况，例如过载，运行等 Environment: A system's condition when a stimulus occurs, e.g. overloaded, running etc.
6. 工件(Artifact)：需求适用的**整个**系统或系统的一部分。Artifact: The whole system or the portion of the system to which the requirement applies.可能是一个软件制品
7. 只有定义好这6个元素，就能锁定架构的一个场景，之后可以用来进行架构的设计
8. 刺激和响应发生在一个环境中：系统正常运行、系统过载、系统受到攻击、系统网络等出现了故障。

#### 2.2.3.3. Tactics 策略(原子级别的最小的决定)
1. 风格或样式运用策略来提供预期的收益 Style or pattern applies tactics to provide the promised benefit.
2. 策略是影响质量属性响应**控制**的**设计决策**，例如冗余。A tactic is a design decision, .e.g. redundancy, that influences the control of a quality attribute response.
3. 策略的**集合**称为体系结构策略。A collection of tactics is called an architectural strategy.
4. 系统设计包括一组设计决策，其中一些决策可帮助控制**质量**属性响应；其他确保系统**功能**的实现 A system design consists of a collection of design decisions: some of these decisions help control the quality attribute response; others ensure achievement of system functionality.
5. 像模式一样，策略也可以由其他策略组成，例如，冗余可以由数据的冗余，计算的冗余组成。设计人员根据需求选择一个或另一个 Like patterns, tactics may also be composed of other tactics, e.g., redundancy may be composed of redundancy of data, redundancy of computation-Designer chooses one or other depending upon requirements.
6. 策略可以用作**策略等级** Tactics can be used as hierarchy of tactics.

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/6.png)

#### 2.2.3.4. 质量设计决策 Quality Design Decisions
1. 架构是设计决策的集合。Architecture is a collection of design decisions. 
2. 七类设计决策(可能重叠) Seven categories of design decisions (may overlap):
   1. **职责分配** Allocation of responsibilities：将大的职责进行分配
   2. **协调模型** Coordination model：各部分之间的沟通、交互
   3. **数据模型** Data model：数据格式、存储方式(缓存等)
   4. **资源管理** Management of resources：CPU、网络、内存、**时间(部分时间敏感的场景)等资源**
   5. **架构元素之间的映射** Mapping among architecture elements：将架构元素如何映射到软件的实现上
   6. **绑定时间决策** Binding time decisions：
      1. 系统的变化可以在什么时间点前需要固定下来，也就是这个时间前，系统还是可以变化的，但是这个时间之后就不可以变化了
      2. 比如选择安装环境是需要在一个时间点前完成的，技术是否添加、编译时间、初始化时间，运行时绑定，但运行时是弹性最大的
      3. 实际上我们希望绑定时间越往后越好，但是也就要付出相应的代价。
   7. **技术选择** Choice of technology：前面的部分都确定后，我们可以选择技术栈相对比较局限，解空间已经被压缩了。

#### 2.2.3.5. 特性
1. Adaptability
2. Extensibility
3. Availability
4. Modularity
5. Configurability
6. Portability
7. Flexibility
8. Reusability
9. Interoperability
10. Testability
11. Performance
12. Auditability
13. Reliability
14. Maintainability
15. Responsiveness
16. Manageability
17. Recoverability
18. Sustainability
19. Scalability
20. Supportability
21. Stability
22. Usability
23. Security

## 2.3. 约束 Constraints
1. 约束是具有**零自由度**的设计决策。A constraint is a design decision with **ZERO** degrees of freedom.
2. 约束是已经做出的**预先**指定的设计决策。Constraints are pre-specified design decisions that have been already made.
3. 通过**接受**设计决策并将其与其他受影响的设计决策进行**协调**，可以满足约束条件。Constraints are satisfied by accepting the design decision and reconciling it with other affected design decisions.

# 3. 质量属性和策略 Quality Attributes & Tactics

## 3.1. 可用性 Availability
1. 可用性是应用程序的**关键**要求 Key requirement for most IT applications
2. 度量方式：以**所需**的可用**时间**比例来衡量，例如 Measured by the proportion of the required time it is useable, e.g.
   1. 营业时间内100％可用 100% available during business hours
   2. 每周计划的停机时间不超过2个小时-24x7x52(100％可用性) No more than 2 hours scheduled downtime per week - 24x7x52 (100% availability)
3. 相关性：与应用程序的**可靠性**有关 Related to an application's reliability
   1. 不可靠的应用程序的可用性较差 Unreliable applications suffer poor availability
   2. 可用性、可靠性不同：
      1. 可用性是指可以使用，但是不保证正确
      2. 可靠性是指可以稳定正确的使用。
4. 可用性损失的时间由以下因素决定：Period of loss of availability determined by:
   1. **发现**故障的时间 Time to detect failure
   2. **纠正**故障的时间 Time to correct failure
   3. **重启**应用的时间 Time to restart application
   4. 例子(时间序)：发生故障-检测到故障-纠正故障-重启应用，这三个代表的是not available的时间(N/A)
   5. 提高可用性的方案
      1. 尽可能降低N/A的时间
         1. 机器尽可能缩短failure到detect时间
         2. 机器尽可能缩短correct到restart的时间
      2. 尽可能提高Available的时间
5. 高可用性策略 Strategies for high availability
   1. 消除**单点故障** Eliminate single points of failure
   2. **复制**和**故障转移** Replication and failover
   3. 自动**检测**并**重启** Automatic detection and restart
6. 可恢复性(例如数据库)Recoverability (e.g.. a database)
   1. 在应用程序或系统出现故障后，可以重新建立**性能级别**并**恢复**受影响的数据的功能。The capability to re-establish performance levels and recover affected data after an application or system failure.
7. 可将**可用性**计算为在**指定的时间间隔**内它将在要求的范围内**提供指定服务**的概率。Availability can be calculated as the probability that it will provide the specified services within required bounds over a specitied time interval.
   1. **MTBF**(平均无故障时间) MTBF (mean time between failures)
   2. **MTTR**(平均维修时间) MTTR (mean time to repair)

$$
\frac{MTBF}{MTBF + MTTR}
$$

8. 计算可用性时，可能不考虑**计划内的停机时间**。Scheduled downtimes may not be considered when calculating availability.

### 3.1.1. Outage, Failure, Fault, Error
1. 可用性是指通过**减少**故障来最大程度地减少服务**中断**时间。Availablity is about minimizing the service outage time by mitigating faults.
2. **Failure的原因**称为**Fault**。A failure's cause is called a fault.
3. 当系统无法交付该系统期望的服务时，将发生Failure。A failure occurs when a system cannot deliver a service that is expected of that system.
4. Failure是系统状态的**可观察**特征。A failure is an observable characteristics of a system's state.
5. 系统任何部分中的Fault都有可能导致Failure。系统可以从Failure中修复或恢复。A fault in any part of a system has a potential to cause a tailure; a system can be repaired or recovered from a failure.
6. Fault发生与Failure之间的**中间状态**称为Error。Intermediate states between the occurrence of a fault and a ftailure are called errors.
7. 名词辨别
   1. Outage是系统不可用的情况，scheduled downTime就是一种Outage。
   2. Failure：系统不可用失效
   3. Fault：是系统导致Failure的原因，Fault不会立即导致Failure
   4. Error：在Fault发生与Failure的中间状态。

### 3.1.2. 服务水平协议 Service-Level Agreement
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/8.png)

1. Amazon EC2的SLA Amazon EC2's SLA
2. AWS将通过商业上合理的努力来使Amazon EC2在服务年度内的年度正常运行率至少达到99.95％。如果Amazon EC2不符合年度正常运行时间百分比承诺，您将有资格获得服务信用。AWS will use commercially reasonable efforts to make Amazon EC2 available with an Annual Uptime Percentage of at least 99.95% during the Service Year. In the event Amazon EC2 does not meet the Annual Uptime Percentage commitment, you will be eligible to receive a Service Credit.
3. 99.95%的是99.9%的一半

### 3.1.3. 对于Failure的计划 Planning for Failure
1. 危害分析 Hazard analysis: 对Failure进行分类
   1. 灾难性的/危险 Catastrophic/ Hazardous
   2. 重大的/轻微的 Major/ Minor 
   3. 没有效果 No effect
2. 故障树分析：Fault tree analysis:

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/9.png)

- 分级处理Failure

1. 故障模式，影响和严重性分析(Failure Mode, Effects, and Criticality Analysis：FMECA) Failure Mode, Effects, and Criticality Analysis (FMECA)
   1. FMECA依靠过去类似系统的故障历史。FMECA relies on the history of failure of similar systems in the past.
   2. $5 * 10^{-5} = 1 * 10^{-3} * 5\%$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/10.png)

### 3.1.4. 可用性通用方案 Availability General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/11.png)

1. source：可能是内部的，也可能是外部的，可能是人、设施、硬件等等，无论是哪一类都会引起可用性的问题，都能发出一个刺激
2. Stiumulus：Failure，不正确的时间、不正确回复(超过边界)
3. 工件：在进程中、交流通道中等等
4. 环境：各种不同的系统环境，正常的错误的等等
5. 反应：错误发生后一些的可能反应，recover是correct的时间
6. 反应度量：时间上、可用性的描述(多长时间，可以用多少)

### 3.1.5. 可用性具体方案 Availability Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/12.png)

1. Source没有收到Heartbeat认为出现了一个Failure
2. 将Stimulus发送给正在处理的进程
3. 进程会通知Operation(人和服务器，来检查是否可以运行)
4. 最后会发送一个回复
5. 整体发生在一个正常运转的环境中

### 3.1.6. 可用性策略 Availability Tactics
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/13.png)

1. 这个树说明了对于可用性可以采用哪些手段来解决可用性：很重要
2. 每一个树的分支代表了我们考虑的时间点：尽可能的延长可用时间
3. 不同的检测服务可用的手段
   1. 主动发送心跳：Heart Beat
      1. 资源的损耗有一次通讯
      2. 可以同时承担更多的业务(定期更新状态)
      3. 自动化检测，更为定时的服务
      4. 单向更为安全
   2. 被动接受检测：Ping/Echo 或 Minotor
      1. 资源损耗有两次通讯
      2. 更加灵活自助，根据自己的情况进行检测
      3. 双向确认
   3. TimeStamp
      1. 收到一系列的消息应该在时间上有先后顺序
      2. 进行常识的信息的检查，如果和常识不符合那么可能是出现了问题
   4. 自检：检查一下自己是否有问题
4. Preparation and Repair
   1. Active Redundancy 冗余部分是都在工作的，如果没有发现问题时，我们只接受Primary的输入，而Secondary的输入会被抛弃，有明显的downTime
   2. Passive Redundancy：Primary同步到Secondary上，而如果Primary挂掉了，则启用Secondary，并快速操作(从上一个状态)，不一定有明显的DownTime，一般选择使用Passive的方式
   3. Spare：组合在一起使用
   4. Rollback：回滚解决不一致的问题
   5. Retry
   6. Ignore Faulty Behavior
   7. Degradation：服务降级，比如Windows的安全模式，让目前已经发生的问题不再影响系统的修复
   8. Reconfiguration：
5. Reintroduction：
   1. shadow
   2. State Retry Resynchronized
   3. Escalating Restart
   4. Non-Stop Forwarding
6. Denial of Service：Dos攻击：大量无效的请求将资源耗尽以阻止提供正常的服务
7. 上述的操作可能不仅仅涉及到一个质量属性

### 3.1.7. Fault

#### 3.1.7.1. Fault 探测 Fault Detection
1. Ping/Echo
   1. 一个组件发出ping命令，并期望在预定时间内在另一个组件上产生回波。One component issues a ping and expects, an echo from another component within a pre-detined time.
   2. Ping/Echo可以在负责一项任务的一组组件中使用。Ping/Echo can be used within a group of components responsible for one task.
2. 心跳(死人时间) Heartbeat(dead man time)
   1. 一个组件定期发出心跳消息(也可以携带数据)，而另一个组件侦听该消息。One component emits a heartbeat message (can also carry data) periodically and another component listens for it.
   2. 如果心跳失败，则假定始发组件已失败，并通知故障纠正组件。If the heartbeat fails, the originating component is assumed to have failed and a fault correction component is notified.
3. 异常 Exception
   1. 识别故障的一种方法是遇到异常。One method for recognising faults is to encounter an exception.
   2. 异常处理程序通常在引入异常的同一过程中执行。The exception handler typically executes in the same process that introduces the exception.
4. ping和心跳策略在不同的进程中运行，异常策略在单个进程中运行。The ping and heartbeat tactics operate among distinct processes, and the exception tactic operates within a single process.

#### 3.1.7.2. Fault 恢复 Fault Recovery
1. 表决 Voting
   1. 在冗余处理器上运行的进程每个都接受等效输入并计算一个简单值，该值将发送给投票者。Processes running on redundant processors each take equivalent input and compute a simple value that is sent to a voter.
   2. 如果投票者从单个过程中检测到异常行为，则它会使失败。If the voter detects deviant behaviour from a single process, it fails it.
2. 主动冗余 Active redundancy
   1. 所有冗余组件均以并行方式响应事件-所有组件均处于相同状态。All redundant components respond to events in parallel - there are all in the same state.
   2. 仅使用了一个组件的响应，其余组件则被丢弃。The response from only one component is used, and the rest are discarded.
   3. 发生故障时，通常不存在停机时间，因为备份是最新的，唯一的切换时间是恢复时间。When a failure occurs, the downtime is usually non-existent as backup is current and the only switching time is the recovery time.
3. 被动冗余 Passive redundancy
   1. 一个组件(主要)响应事件，并通知其他组件(辅助)它们必须进行的状态更新。One component (primary) responds to events and informs the other components (secondary) of state updates they must make.
   2. 发生故障时，系统必须首先确保备份状态足够新，然后才能恢复服务。When a failure occurs, the system must first ensure that the backup state is sufficiently recent before resuming services.
4. 备件 Spare
   1. 备用备用计算平台配置为替换许多不同的故障组件。A standby spare computing platform is configured to replace many different failed components.
5. 影子操作 Shadow operation
   1. 先前发生故障的组件可能会在“影子模式”下运行一小段时间，以确保它可以模仿工作组件的行为，然后再将其恢复正常工作。A previously failed component may be run in  "shadow mode" for a short time to make sure that it mimics the behaviour of the working components before restoring it to service.
6. 状态重新同步 State re-synchronisation
   1. 被动和主动冗余策略要求要恢复的组件在恢复服务之前对其状态进行升级。The passive and active redundancy tactics require the component being restored to have its state upgraded before its return to service.
7. 检查点/回滚 Checkpoint/ Rollback
   1. 检查点记录的是定期或响应特定事件创建的一致状态。A checkpoint is recording of a consistent state created either periodically or in response to specific events.
8. 从服务中删除 Removal from service
   1. 该策略将系统的某个组件从运行中移除，以进行一些活动以防止预期的故障。This tactic removes a component of the system from operation to undergo some activities to prevent anticipated failure.
9. 交易 Transaction
   1. 事务是几个连续步骤的捆绑，这样就可以一次撤消整个捆绑。A transaction is the bundling of several sequential steps such that the entire bundle can be undone at once.
10. 过程监控器 Process monitor
    1. 一旦检测到流程中的故障，监视流程就可以检测到不良流程并为其创建新实例，并按照备用策略将其初始化为适当的状态。Once a fault in a process has been detected, a monitoring process can detect the non- pertorming process and create a new instance ot it, initialised to some appropriate state as in the spare tactic.

### 3.1.8. 可用性设计和分析的检查列表 Checklist for Availability Design & Analysis
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/14.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/15.png) |
| -------------------- | -------------------- |

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/60.png)

## 3.2. 互操作性 Interoperability
1. **互操作性**是指两个或多个系统可以在特定上下文中**通过接口**完全**改变**有意义的信息的程度 Interoperability is about the degree to which two or more systems can usefully exchange meaningful information via interfaces in a particular context.
   1. **交换**数据的能力(**语法**互操作性)Ability to exchange data (syntactic interoperability)
   2. 能够正确**解释**数据(**语义**互操作性)Ability to correctly interpret the data (semantic interoperability)
2. 互操作性需要确定与**谁，什么以及在什么情况**下(上下文)。Interoperability needs to identify with whom, with what, and under what circumstances (the context). 
3. 互动 Interface
   1. 夏琳说金告诉她特雷弗听说希瑟想参加你的聚会。Charlene said that Kim told her that Trevor heard that Heather wants to come to your party.
4. 互操作性的两个重要方面：Two important aspects of interoperability:
   1. **发现**：服务的使用者必须发现服务的**位置，身份和接口**。Discovery: the consumer of a service must discover the location, identity, and the interface of the service.
   2. **处理回应**：Handling of the response:
      1. 向请求者**报告**并做出**响应**。reports back to the requester with response.
      2. 将其响应**发送**到另一个系统。sends its response on to another system.
      3. 向任何感兴趣的各方**广播**其回复。broadcasts its response to any interested parties.

### 3.2.1. 互操作性的通用方案 Interoperability General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/16.png)

### 3.2.2. 互操作性的样本方案 Interoperability Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/17.png)

### 3.2.3. 互操作性的策略 Interoperability Tactics
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/18.png)

1. 定位 Locate
   1. **发现**服务：通过搜索已知目录服务来找到服务Discovery service: locate a service through searching a known directory service.
      1. 多级间接 multiple levels of indirection
2. 管理界面 Manage interfaces
   1. **编排**：使用控制机制来协调，管理和排序特定服务的调用。Orchestrate: uses a control mechanism to coordinate and manage and sequence the invocation of particular services.
   2. **定制界面**：添加或删除界面功能 Tailor interface: adds or removes capabilities to an interface.
3. Orchestrate：请求，一个请求会涉及到多个Service，我们需要按照一定顺序进行处理请求

### 3.2.4. 互操作性的检查列表 Checklist for Interoperability Design & Analysis
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/19.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/20.png) |
| -------------------- | -------------------- |


## 3.3. 可修改性 Modifiability
1. 可修改性涉及**更改**以及进行更改所**花费的时间或金钱**，包括这种可更改性影响其他功能或质量属性的程度。Modifiability deal with change and the cost in time or money of making a change, including the extent to which this modifiability affects other functions or quality attributes.
2. 为变更做**准备**是有代价的，而**进行**变更则要付出代价。There is a cost of prepraring for change as well as a cost of making a change.
3. 计划可修改性的四个问题 Four questions to plan for modifiability
   1. 有什么可以改变的？What can change?
   2. 变化的**可能性**是多少？What is the likelihood of the change?
   3. **何时**进行更改，谁进行更改？When is the change made and who makes it?
   4. 变更的**费用**是多少？What is the cost of the change?
4. 如果更改少于预期，则可能不需要昂贵的修改机制。If fewer changes than expected come in, then an expensive modification mechanism may not be warranted.
5. 计算公式：N * 不使用机械装置进行更改的成本 $\leq$ 安装机械装置的成本 +(N *使用机械装置进行更改的成本)
6. 降低的成本可以用于提高可修改性

### 3.3.1. 可修改性的通用方案 Modifiability General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/21.png)

### 3.3.2. 可修改性的样本方案 Modifiability Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/22.png)

### 3.3.3. 可修改性的策略 Modifiability Tactics
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/23.png)

1. Reduce Size of a Module：**拆分模块**：如果要修改的模块包含**大量功能**，则修改成本可能会很高(尽可能的控制包的大小)。Split module: If the module being modified includes a great deal of capabilities, the modification costs will likely be high.
2. Increase Cohesion：**增加语义一致性**：如果模块中的职责A和B不能达到**相同的目的**，则应通过创建新模块或将职责移至现有模块将它们放置在不同的模块中。Increase semantic coherence: If the responsibilities A and B in a module do not serve the same purpose, they should be placed in different modules by creating a new module or moving a responsibility to an existing module.
3. Reduce Coupling：
   1. **封装**为模块引入了显式**接口**，并减少了对一个模块的更改**传播**到其他模块的可能性。Encapsulation introduces an explicit interface to a module, and reduces the probability that a change to one module propagates to other modules.
   2. 使用**中介**打破**依赖**：所有的组件都要通过中间的组件进行通信，使用反模式等方法解决。Use an intermediary breaks a dependency.
   3. 当两个模块受到相同更改的影响时，请进行**重构**：不同于代码重构 Refactor when two modules are affected by the same change.
4. Defer Binding：**延迟绑定**：在生命周期中与初始定义阶段**不同的阶段**绑定某些参数的值。Defer binding: Binds the value of some parameters at a different phase in the life cycle than the one in which they are initially defined.

### 3.3.4. Checklist for Modifiability Design and Analsis

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/24.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/25.png) |
| -------------------- | -------------------- |

## 3.4. 性能 Performance
1. 性能与**时间**有关，软件与系统满足时序要求的能力有关。(单位时间内能做多少事情) Performance is about time and the software system's ability to meet timing requiements.
2. 所有系统都有性能要求，即使未明确表示也是如此。All systems have pertormance requirements, even it they are not explicitly expressed.
3. 响应时间的两个基本因素 Two basic contributors to the response time
   1. 处理时间(系统**正在**响应时) processing time (when the system is working to response)
   2. 阻塞时间(系统**无法**响应时) blocked time (when the system is una able to response)

### 3.4.1. 性能的通用方案 Performance General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/26.png)

### 3.4.2. 性能的样本方案 Performance Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/27.png)

### 3.4.3. 性能的策略 Tactics for Performance
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/28.png)

1. 在**需求**方面 On the demand side
   1. 管理**采样率**(降低采样频率) Manage sampling rate (reducing sampling frequency)
   2. 限制事件响应：当离散事件到达系统的速度太快而无法处理时，必须将事件**排队**，直到可以处理它们为止。Limit event response: When discrete events arrive at the system too rapidly to be processed, the events must be queued until they can be processed.
   3. 如果不是所有事件都同样重要，则对事件进行**优先级**排序。Prioritize events if not all events are equally important.
   4. 通过使用**中介**来增加处理事件流的资源，从而减少开销 Reduce overhead by using intermediaries to increase the resources in processing an event stream
2. 在**资源**方面 On the resource side
   1. 增加**资源**(更快的处理器，更多的内存，更快的网络...)Increase resources(faster processor, additional memory, faster network..)
   2. 如果可以**并行**处理请求，请引入并发性。Introduce concurrency if requests can be processed in parallel.
   3. 维护多个计算副本：使用负载平衡器将新工作分配给可用的**重复**服务器之一。Maintain multiple copies of computations: Use load balancer to assign new work to one of the available duplicate servers.
   4. 维护数据的多个副本：Maintain multiple copies of data:
      1. 快取 caching
      2. 资料复制 data replication

### 3.4.4. Checklist for Performance Design and Analysis

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/29.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/30.png) |
| -------------------- | -------------------- |

## 3.5. 安全性 Security
1. 安全性衡量系统**保护**数据和信息免遭**未授权访问**的能力，同时仍提供对授权人员和系统的访问权限。Security measures system's ability to protect data and information from unauthorized access while still providing access to people and systems that are authorized.
2. 安全性的三个特征：(CIA) Three characteristics of security: (CIA)
   1. 机密性，Confidentiality：防止**未经授权**访问数据和服务。Confidentiality: Data and services are pretected from unauthorized access.
   2. 完整性，Integrity：数据和服务不会受到**未经授权**的操纵。Integrity: Data and services are not subject to unauthorized manipulation.
   3. 可用性，Availability：系统将可供**合法使用**。Availability: The system will be available for legitimate use.

### 3.5.1. 安全性的通用方案 Security General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/31.png)

### 3.5.2. 安全性的样本方案 Security Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/32.png)

### 3.5.3. 安全性的策略 Security Tactics
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/33.png)

1. 通过将系统内的网络流量或服务请求模式与一组签名或已知模式进行比较来检测**入侵** Detect intrusion by comparing network traffic or service request patterns within a system to a set of signatures or known patterns.
2. 检测服务**拒绝** Detect service denial
3. 使用校验和或哈希值验证**消息的完整性**。Verify message integrity using checksums or hash values.
4. 确定参与者-系统的任何**外部**输入的**来源**。ldentify actors - source of any external input to the system.
5. **验证**演员或他们所要扮演的角色。Authenticate actors who or what they purport to be.
6. **授权**有权访问和修改数据或服务的行为者。Authorize actors who have the rights to access and modify either data or services.
7. **限制**对计算资源的**访问**。Limit access to computing resouces.
8. 通过最小化系统的攻击面来**限制暴露**。Limit exposure by minimizing the attack surface of a system.
9. **加密**数据。Encrypt data.
10. 正在进行攻击时，撤消对**敏感资源**的访问。Revoke access to sensitive resources when an attack is underway.
11. Authenticate：认证，Authorize：授权。

### 3.5.4. 安全性的检查列表 Checklist for Security Design and Analysis
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/34.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/35.png) |
| -------------------- | -------------------- |

## 3.6. 可测试性 Testability
1. 可测试性是指可以使软件通过(通常基于执行)测试来证明其故障的难易程度。Testability refers to ease with which software can be made to demonstrate its faults through (typically execution-based) testing.
2. 为了使系统能够正确测试，必须有可能控制每个分量S的输入，然后观察其输出。For a system to be properly testable, it must be possible to control each component s inputs and then to observe its outputs.

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/36.png)

### 3.6.1. 可测试性的通用方案 Testability General Scenario

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/37.png)

### 3.6.2. 可测试性的样本方案 Testability Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/38.png)

### 3.6.3. 可测试性的策略 Testability Tactcs
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/39.png)

1. **控制和观察系统状态**：维护某种状态信息，允许测试人员为该状态信息分配一个值，和/或使测试人员可以按需访问该信息。Control and observe system state: Maintain some sort of state information, allow testers to assign a value to that state information, and/or make that information accessible to testers on demand.
   1. **专用界面**使您可以控制或捕获组件的值 Specialized interfaces allow you to control or capture values for a component.
   2. **记录/回放**导致故障的状态，然后重新创建故障。 Record/playback the state that caused a fault and re-create the fault.
   3. **沙盒**将系统的实例与现实世界隔离开来，可以进行实验以消除其后果。Sandboxing isolates an instance of the system from the real world to enable experimentation to undo its consequences.
2. **限制复杂度**：复杂的软件更难测试，因为它的操作状态空间很大，并且在大状态空间中重新创建精确状态更加困难。Limit complexity: Complex software is harder to test, because its operating state space is very large and more difficult to re-create an exact state in a large state space.
   1. 限制结构的**复杂性**，避免、减少或解决组件之间的**依赖**关系；隔离和封装对外部环境的依赖关系。Limit structural complexity avoiding, reducing or resoling dependencies between components; isolating and encapsulating dependencies on external environment.
      1. 限制派生一个类的**类的数量**。Limit the number of classes from which a class is derived.
      2. 限制继承**树的深度**和类的子级数。Limit the depth of the inheritance tree and the number of children of a class.
      3. 限制**多态**和**动态调用**。Limit polymorphism and dynamic calls.
   2. 限制**不确定性**-限制**行为复杂性** Limit nondeterminism - limiting behavioral complexity.
      1. 非确定性系统更难测试。Nondeterminism systems are harder to test.

### 3.6.4. 可测试性的检查列表 Checklist for Testability Design and Analysis
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/40.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/41.png) |
| -------------------- | -------------------- |

## 3.7. 易用性 Usability
1. 可用性与用户完成所需任务的**难易程度**以及系统提供的用户**支持**的类型有关。Usability is concerned with h how easy it is for the user to accomplish a desired task and the kind of user support the system provides.
2. 可用性包括以下几个方面：Usability comprises the following aspects:
   1. **学习**系统功能 Learning system features
   2. **有效**使用系统 Using a system efficiently
   3. 最小化**错误的影响** Minimizing the impact of errors
   4. 使系统**适应**用户需求 Adapting the system to user's needs
   5. 增强信心和**满意度** Increasing confidence and satistaction

### 3.7.1. 易用性的通用方案 Usability General Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/42.png)

### 3.7.2. 易用性的样本方案 Usbility Sample Scenario
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/43.png)

### 3.7.3. 易用性的策略 Usability Tactics
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/44.png)

1. 支持用户主动权：支持用户纠正错误或提高效率。Support user initiative: support the user in either correcting errors or being more efficient.
   1. **取消** Cancel
   2. **撤消**：系统必须维持足够数量的系统状态，以便可以恢复更早的状态。Undo: System must maintain a sufficient amount of system state so that an earlier state may be restored.
   3. 用户启动长时间操作运行时**暂停/恢复** Pause/resume when a user has initiated a long-running operation
   4. 将较低级别的对象**聚合**到一个**组**中，以便可以将操作应用于该组。Aggregate the lower-level objects into a single group, so that the operation may be applied to the group.
2. **初步支持**系统：确定系统用来预测其自身行为或用户意图的模型。Support system initiaive: Identify the models the system uses to predict either its own behavior or the user's intention.
   1. 维护**任务模型**：确定**上下文**，以便系统可以了解用户的尝试并提供帮助，对任务进行建模。Maintain task model: Determine context so the system can have some idea of what the user is attemping and provide assistance.
   2. 维护**用户模型**：代表用户的关于**系统的知识**，根据用户行为训练出用户的模型 Maintain user model: Represent the user's knowledge of system.
   3. 维护**系统模型**：确定预期的**系统行为**，以便可以向用户提供适当的反馈。Maintain system model: Determine expected system behavior so that appropriate feedback can be given to the user.

### 3.7.4. Checklist for Usbility Design and Analysis

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/45.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/46.png) |
| -------------------- | -------------------- |

## 3.8. 更多的能力 X-ability
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/47.png)

# 4. 架构攸关的需求 Architecturally Significant Requirements
1. 架构攸关的需求(ASR)是对体系结构产生**深远影响**的要求-如果没有这样的要求，体系结构可能会发生**巨大的变化**。An Architecturally Significant Requirement (ASR) is a requirement that will have a profound effect on the architecture - the architecture might well be dramatically different in the absence of such a  requirement.
2. QA需求越**困难和重要**，就越有可能显着影响体系结构，从而成为ASR。The more difficult and important the QA requirement, the more likely it is to significantly affect the architecture, and hence to be an ASR.
3. 如何系统地识别将影响ASR和其他因素？How to systematically identify the ASRs and other factors that will shape the architecture?
   1. 从**需求文档**中收集ASR Gathering ASRs from requirements documents
   2. 通过采访**涉众**来收集ASR Gathering ASRs by interviewing stakeholders
   3. 通过了解**业务目标**来收集ASR Gathering ASRs by understanding the business  goals
   4. 在**项目树**中管理ASR Capturing ASRs in a utility tree

## 4.1. 从需求文档中收集ASR Gathering ASRs from Requirements Documents
1. 无论是使用"MoSCoW"样式指定需求还是作为"用户故事"的集合来指定需求，这些都不能帮助您确定质量属性。Whether requirements are specifed using the "MoSCoW" style or as a collection of "user stories", neither of these is much help in nailing down quality attributes.
2. MoSCoW样式：<a href = "https://blog.csdn.net/cheny_com/article/details/6358456">MoSCoW的样式说明</a>：使用四个级别来定义一个需求的优先级程度
3. 需求文档通常会以两种方式使架构师**失败**：Requirements documents often fail an architect in two ways:
   1. 需求规范中的大多数内容都不会影响体系结构。Most of what is in a requirements specification does not affect the achitecture.
      1. 系统应模块化 The system shall be modular
      2. 系统应显示出高可用性 The system shall exhibit high usability
      3. 系统应满足用户的性能期望 The system shall meet users' performance expectations
   2. 对架构师有用的大部分内容甚至都没有出现在最佳需求文档中 Much of what is useful to an architect is not in even the best requirements document.
      1. 在收购环境中，需求文档代表的是收购方的利益，而不是开发商的利益。In an acquisition context, the requirements document represents the interests of the acquirer, not that of the developer.
4. 如果某项要求影响了**关键体系结构设计决策**的制定，那么根据定义，它就是ASR。If a requirement affects the making of a critical architectural design decision, it is by definition an ASR.

## 4.2. 通过和涉众面谈来收集ASR Gathering ASRs by Interviewing Stakeholders
1. 质量属性工作坊(QAW) Quality Attribute Workshop (QAW)
   1. QAW演示和介绍 QAW presentation and introductions
   2. 业务任务介绍 Business mission presentation
   3. 架构计划介绍 Architectual plan presentation
   4. 架构驱动程序的识别：就精简的架构驱动程序列表达成共识，其中包括总体需求，业务驱动程序，约束和质量属性。Identification of architectural drivers: to reach a consensus on a ditilled list of architectural drivers that includes overall requirements, business drivers, constraints, and quality attributes.
   5. 场景集思广益：每个利益相关者都表达一个场景，表示他/她对系统的关注。Scenario brainstorming: each stakeholder expresses a scenario representing his/ her concerns with respect to the system.
   6. 方案合并(合并类似方案) Scenario consolidation (merging similar scenarios)
   7. 方案优先级(通过投票) Scenario prioritization(by voting)
   8. 方案细化：对最重要的方案进行细化和阐述。Scenario refinement: the top scenarios are refined and elaborated.
2. QAW的结果包括架构驱动程序列表和利益相关者(作为一个小组优先考虑)的一组(2A方案)。The results of QAW include a list of architectural drivers and a set of QA scenarios that the stakeholders (as a group prioritized).

## 4.3. 通过Utility树来获取ASR Capturing ASRs in a Utility Tree
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/48.png)

1. 将scenario使用量化的方式来描述，之后才可以使用测试等方式来确定是否实现了要求。
2. 逐渐对质量需求进行分解，分解到含有量化指标为止。
3. 然后将分解的结果进行细化

## 4.4. 基于决策来发现ASR的方法 Persona-Based Approach to exploring ASRs

### 4.4.1. 结合ASR工作 Working with ASRs
1. 在实践中，通常不会引发ASR(尤其是NFR)，也没有明确规定。 In practice ASRS (especially NFRs) are often not elicited and are not clearly specified.
   1. 许多软件需求规范根本不包含NFR。Many Software Requirements Specifications simply don't include NFRs.
   2. 同样，许多敏捷项目都没有包含与ASR相关的用户案例。Similarly, many agile projects fail to include ASR-related user stories.
2. 有没有更好的办法？Is there a better way?
3. 在我们的TraceLab项目中，我们采用了角色驱动的方法，使我们能够在项目早期发现具有架构重要性的需求，并利用我们的知识对架构设计和实施做出明智的决策。In our TraceLab project we adopted a persona-driven approach which enabled us to discover architecturally significant requirements early in the project and to use our knowledge to make informed decisions about architectural design and implementation.

### 4.4.2. TraceLab中的ASR ARSs in TraceLab
1. TraceLab是一项由国家科学基金会资助的200万美元的项目 TraceLab is a US $2 Million Project funded by the National Science Foundation
2. 由DePaul大学，威廉和玛丽学院，肯特州立大学和大学的合作者开发。肯塔基州。Developed by collaborators at DePaul University, College of William and Mary, Kent State Univ, and Univ. of Kentucky.
3. 旨在通过促进创新和创造力，增强可追溯性研究人员之间的协作，降低新可追溯性研究项目的启动成本和工作量以及促进技术转让来授权未来的可追溯性研究。Intended to empower future traceability research through facilitating innovation and creativity, increasing collaboration between traceability researchers, decreasing the startup costs and effort of new traceability research projects, and fostering technology transfer.
4. 提供了一个环境，研究人员可以在此环境中设计和执行实验，共享组件和数据集，并在受控的环境中比较评估结果。Provides an environment in which researchers can design and execute experiments, share components and datasets, and comparatively evaluate results in a controlled setting.

### 4.4.3. 考虑折中 Competing Tradeoffs
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/49.png)

### 4.4.4. 传统的HCI角色 Traditional HCI Personas
1. 我们决定通过开发一组精通架构的角色来表示冲突的需求。We decided to represent the conflicting needs through developing a set of architecturally-savvy personas.
2. 传统上，角色构建涉及对用户进行调查，对其进行分类，制定使用假设，进行验证，创建方案以及最终设计角色。Traditionally persona construction involves surveying users, classifying them, formulating hypotheses of use, validating, creating scenarios,  and finally designing personas.
3. 我们的项目太耗时，即过多的前期工作会阻碍我们实现目标。Too time consuming for our project i.e. too much upfront effort that would retard the achievement of our goals.
4. 解决方案：角色草图。Solution: Persona sketches.

### 4.4.5. 精通架构的角色(精简版) Architecturally-Savvy(Lite)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/50.png)

### 4.4.6. 几个例子
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/51.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/52.png) |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/53.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/54.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/55.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/56.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/57.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/58.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec13/59.png) |                      |

# 5. 第一次作业
1. 至少一个是上课列出的质量属性的单子中，另一个可以不再上课列出的质量属性的单子
2. 建议使用表格的形式(一个tactics会对多个质量属性产生影响)
3. 第一页上写好姓名和学号