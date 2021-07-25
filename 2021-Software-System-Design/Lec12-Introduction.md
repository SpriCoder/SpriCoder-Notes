lec12-Introduction
---

# 1. 课程背景

## 1.1. 为什么要研究软件设计体系结构？Why Study Software Design & Architecture?
1. 软件(IT)系统无处不在 Software(IT) systems are everywhere
2. 每个软件密集型(组成的)系统都有一个软件设计和体系结构 Every software intensive system has a sofftware design and architecture
3. 软件设计和体系结构是实践，教育和研究中越来越重要的领域 Software design and architecture are an increasingly important area of practice, education, and research
4. 专业：软件架构师 As a profession: Software Architect
5. 作为研究领域 As a research area
   1. 最初于1960年左右开始 Originally started around 1960
   2. 自1990年以来备受关注 Attracting major attention since 1990
6. 本课程是关于 This course is about
   1. 软件设计和体系结构的概念，原理，方法和模式 Concepts, principles, methods, and patterns of software design and architecture
   2. 软件设计和体系结构的最新实践 State-of-the-art practices of software design and architecture

## 1.2. Learning Objectives 将要学习到的东西
1. 理解软件设计和体系结构的概念和原理 Understand concepts and principles of software design and architecture
2. 通过考虑需求或通过反向体系结构来创建软件体系结构 Create software architecture by taking requirements or through reverse architecting
3. 在创建软件体系结构和设计的时候应用设计模式、风格、中间件技术和框架 Apply tactics, patterns, styles, middleware technologies and frameworks in creating software architecture and design
4. 分析软件设计和评估软件体系结构的系统性 Analyze software design and evaluate software architecture systematically
5. 理解艺术式的设计是如何应用到软件设计与体系结构中的 Understand state-of the-art methods applied in software design and architecture
6. 理解软件设计与软件体系结构之间的关系，以及其他软件工程的领域话题 Understand relationships between software design and software architecture, and other software engineering topic areas

# 2. 介绍

## 2.1. Understanding Software Engineering 理解软件工程
1. Software 和 Engineering
2. Software 和 Hardware
   1. 软件是不可见的：软件是虚拟的，而硬件是实体的。
   2. 软件制作出来就是为了被修改和改变的(软件的演化是他的本质属性)
3. Science vs. Engineering：科学的研究是研究这个世界既有的部分，而工程是研究的是人类创造新的世界(是不是因为人才产生的)，下面的图是很重要的。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/1.png)

## 2.2. What is Software Architecture 什么是软件体系结构
1. 定义1：程序或计算系统的软件体系结构是系统的一个或多个结构，其中包括软件组件，这些组件的外部可见属性以及它们之间的关系。[软件工程学院(SEI)] Definition 1:"The software architecture of a program or computing system is the structure or structures of the system, which comprise software elements, the externally visible properties of those elements, and the relationships among them." [Software Engineering Institute (SEl)] 
2. 定义2：系统的基本组织，体现在其组件，它们之间的相互关系以及环境以及支配其**设计和演进的原则**。[IEEE 1471-2000有关软件密集型系统的体系结构描述的推荐做法] Definition 2: "The fundamental organization of a  system, embodied in its components, their relationships，to each other and the environment, and the principles governing its design and evolution." [IEEE 1471 -2000 Recommended Practice for Architectural Description of Software-Intensive Systems"]
3. Module和Component的区别
   1. Component(组件)：是已经实现了的软件部分
   2. Module(模块)：是还没有实现出来的软件部分
   3. Element包含了Component和Module。

## 2.3. 体系结构 vs 设计 Architecture vs. Design
1. 体系结构是关于软件设计 It's about software design 
   1. 所有的体系结构都是软件设计，但不是所有的软件设计都是体系结构 All architecture is software design, but not all design is software architecture
   2. 体系结构是设计过程的一个过程 "Architecting" is part of the design process 
2. 其他观点 Other views
   1. 体系结构是更高层的设计 High-level designs 
   2. 体系结构是设计决策的组合 A set of design decisions 
   3. 体系结构是根据不同项目而不同的 Locality
3. 系统的结构或组织 Structure/Organization of the system
   1. 元素(Elements)：部件(Components)和连接件(Connectors) Elements: components & connectors 
   2. 关系：静态(static)和动态(dynamic)的关系 Relationships: static & dynamic relationships
4. 属性：元素，元素组和整个系统 Properties: elements, groups of elements & overall system

## 2.4. 体系结构 vs 结构 Architecture vs. Structure
1. 体系结构将系统分解成部件/模块/子系统，降低每一部分的复杂度 Decomposition of system into components/modules/subsystems 
2. 体系结构定义 Architecture defines
   1. 部件接口：部件可以做什么？Component interfaces: What a component can do?
   2. 部件交流和依赖：部件可以怎么沟通交流？Component communications and dependencies:How components communicate? 
   3. 部件职责：当我们询问它时，部件需要精确的知道自己将要做什么？Component responsibilities:Precisely what a component will do when you ask it?

### 2.4.1. 结构和体系结构 Structure and Architecture
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/2.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/3.png) |
| ------------------- | ------------------- |

1. 左图是对于结构的描述
2. 右图是对于体系结构的描述
   1. 图中左侧的设计：第三方的模块与其他的四个模块直接耦合
   2. 图中右侧的设计：我们加入了AL模块来屏蔽了变化

### 2.4.2. 体系结构确定通信 Architecture Specifies Communication
1. 通信需要 Communication involves:
   1. **数据**通过机器传递，比如 Data passing mechanisms, for example:
      1. 函数调用 Function call
      2. 远程方法调用 Remote method invocation
      3. 异步信息 Asynchronous message
   2. **控制**流 Control flow
      1. 组件间的信息流来满足需要的功能 Flow of messages between components to achieve required functionality
      2. 序列化的 Sequential
      3. 并发/并行 Concurrent/parallel
      4. 同步 Synchronization

### 2.4.3. 体系结构强调非功能性需求(NFA) Architecture Address NFRS
1. **非功能性需求(Non-functional requirements)**定义了**系统运行的有多好** Non-functional requirements (NFRs) define "how well a system works? 
2. 当然也需要考虑功能性需求。
3. 非功能性需求很少在功能性需求中很少被发现 NFRs rarely captured in functional requirements
   1. 又名体系结构需求 Aka. architecture requirements
   2. 必须通过体系结构引出 Must be elicited by architect
4. 非功能性需求 NFRs include
   1. 技术约束 Technical constraints
   2. 商业约束 Business constraints
   3. 质量属性 Quality attrilbutes
5. 讨论：质量属性列表 Discussion: A list of quality attributes?

## 2.5. 设计是一种抽象 Design is an Abstraction
1. 体系结构提供了设计的更高层抽象视角 Architecture provides an higher level abstract view of a design
   1. 隐藏设计的复杂性和实现 Hides complexity and implementation of design
   2. 可能是或者可能不是体系结构元素和软件元素之间的直接映射 May or may not be a direct mapping between architecture elements and sottware elements 
2. 黑盒设计 和 白盒设计 Blackbox design and Whitebox design
   1. 是对系统结构和交互的非正式描述Informal depiction of system's structure and interactions.
   2. 描述在体系结构中内嵌的设计哲学Portray the design philosophies embodied in the
architecture
3. 讨论：为什么在设计中使用抽象？Discussion: Why abstraction in design?

## 2.6. 体系结构视图 Architecture Views
1. 体系结构视图主要是为了应对软件不可见的问题，屏蔽其他没有影响的部分，将关注点进行分离
2. 软件体系结构代表了一个复杂的设计制品 A software architecture represents a complex design artifact
3. 很多体系结构的可能视图：类比建筑-平面图，外部设计，电力设计，水暖，空气调节 Many possible 'views' of the architecture:Analogy with buildings-floor plan, external, electrical, plumbing, air-conditioning

# 3. 如何创建一个设计 How to Develop a Design?
1. 广义的设计策略 Generic Design Strategies:
   1. 分解 Decomposition
   2. 抽象 Abstraction
   3. 逐步的：分而治之 Stepwise:Divid and Conquer
   4. 生成和测试 Generate and Test
   5. 迭代：渐进式细化 Iteration: Incremental Refinement
   6. 重用元素 Reuseable elements

## 3.1. K.Kruchen的4+1视图模型 P.Krutchen's 4+1 View Model
1. 逻辑视图：描述了体系结构中在体系结构上明显重要的元素以及他们之间的关系Logical view: describes architecturally significant elements of the architecture and the relationships between them
2. 过程视图：描述了体系结构中的并发和交流元素 Process view: describes the concurrency and communications elements of an architecture.
3. 物理视图：描述了主要过程和部件是如何映射到应用硬件上的 Physical view: depicts how the major processes and components are mapped on to the applications hardware.
4. 发展视图：描述了软件部件是如何在软件内部组织的，比如配置管理工具Development view: captures the internal organization of the software components as held in e.g./ a configuration management tool.
5. 使用体系结构的情况：描述了体系结构的需求，关系到了超过一个常规的视图Architecture use cases: capture the requirements for the architecture; related to more than one particular view
6. 四个视图在某一个场景下进行描述

## 3.2. 体系结构和软件体系结构 Architect & Software Architect
> 体系结构设计了满足人类需求的结构 Architects design structures to meet human needs. - James Fitch, 1972

1. 体系结构的作用仍然保持着一致 The role of the architect remains the same
   1. 倾听用户，理解整体的需求 Listening to clients, understanding the totality of needs
   2. 仔细检查灵活性 Scrutinizing feasibilities
   3. 形成一个实际的结构版本，创建一个蓝图 Forming a practical vision of a structure and creating a blueprint
   4. 监督构建过程，保证是符合规范的 Overseeing construction and ensuring compliance to the plan 
   5. 引导在暴风雨式的设计变更、危机和歧义性中的版本 Guiding the vision through the tempest of design changes, crises and ambiguities
2. 软件体系结构则是监督软件的构建过程：开发人员、工程师和设计者 Software architects oversee software construction professionals Programmers, Engineers, Designers
3. 有名的软件体系结构
   1. Bill Gates: Chief Software Architect of Microsoft
   2. Tim Bernrs-Lee: Inventor and Chief Architect of World Wide Web
   3. Roy Fielding: Representational State Transfer (REST)

## 3.3. 软件体系结构在做什么 What Does a Software Architect Do?
1. 联络人 Liaison
   1. 在客户、技术团队和商业/需求分析师之间 Among clients, technical team and business/requirements analysts
   2. 包含管理和市场分析 With management or marketing 
2. 软件工程：软件工程的最佳实践 Software Engineering:Software engineering best practices
3. 技术知识：深入理解技术领域 Technology Knowledge:Deep understanding of technology domain
4. 风险管理：Risk Management
   1. 与设计、技术决策相关的风险 Risks associated with the design, technology choices
   2. 更多？More?

## 3.4. 总体设计模型 A General Design Model
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/4.png)

开发和设计是在做减法

## 3.5. 软件设计过程 Software Design Process
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/5.png)

## 3.6. 体系结构活动 Architecture Activities
1. 创建系统的商业案例 Creating the business casenfor the System
2. 理解需求 Understanding the requirements
3. 创建和选择体系结构 Creating and selecting architecture
4. 沟通体系结构(涉众，包括开发商) Communicating the architecture (stakeholders including developers)
5. 分析或评估体系结构 Analysing or evaluating the architecture
   1. 整体的方法论 Overall methodologies
   2. 具体技术的质量 Quality specific techniques
6. 实现体系结构Implementing the architecture
7. 保证和体系结构的一致性Ensuring contormance to an architecture

## 3.7. 软件体系结构过程 Software Architecture Process
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/6.png)

## 3.8. 体系结构生命周期 Architecture Lifecycle
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-Software-System-Design/img/lec12/7.png)

## 3.9. 软件体系结构和体系结构知识领域 Software Design & Architecture Knowledge Areas
1. 软件设计基本原理 Software Design Basic Concepts
   1. 整体设计原理 General design concepts
   2. 上下文：软件发展生命周期-需求、设计、编码和测试 Context: software development life cycle - requirements, design, construction and testing
   3. 设计过程：决策、活动、可运行产品 Design process(role, activity, work product)
   4. 软件设计的使能技术 Enabling techniques for software design
2. 核心问题(技术)：一致性、事件控制和处理、分发、异常处理、交互系统、持久化 Key Issues (technical): concurrency, control and handling of events, distribution, exception handling, interactive systems, persistence
3. 软件结构和体系结构 Software Structure and Architecture
   1. 体系结构结构和视点 Architecture Structures and viewpoints
   2. 体系结构风格和模式(宏观体系结构) Architectural styles and patterns (macro-architecture)
   3. 设计模式(微观体系结构) Design patterns (micro-architecture)
4. 软件设计方法Software Design Methods
   1. 体系结构方法，比如属性驱动的设计 Architecture Methods (e .g., Attribute- Driven Design)
   2. 设计方法，比如动态系统发展方法 Design Methods (e.g., Dynamic System Development Method)
5. 软件设计的质量分析和评估 Software Design Quality Analysis and Evaluation 
   1. 质量属性 Quality attributes
   2. 质量分析和评估方法、技术和工具 Quality analysis and evaluation methods, techniques and tools
      1. 设计回顾：比如SEI的体系结构权衡分析方法 Design reviews (e.g. SEI's Architecture Trade-off Analysis Method)
      2. 静态分析和动态分析 Static analysis and dynamic analysis
      3. 模拟和原型 Simulation and prototyping
   3. 度量 Measures:
      1. 矩阵：体系结构级别 Metrics: Architecture level
      2. 技术特有度量指标 Technique specific measures
6. 设计建模和展示 Design Modeling and Representation
   1. 体系结构和设计符号(体系结构描述语言，Architecture Description Languages，ADL)Architecture and Design Notations (Architecture Description Languages(ADL))
   2. UML Unified Modelling Language (UML)
   3. 设计文档(意见或其他) Design Documentation (Views & Beyond)
   4. 其他：在活动、关注点和领域上的不同，比如ACME，Rapide。 Others: differ in ability, focus and domain (e.g. ACME, Rapide)

# 4. 讨论
1. 科学和工程有什么不同？What is Difference between Science and Engineering? 
   1. 科学的研究是研究这个世界既有的部分
   2. 工程是研究的是人类创造新的世界(是不是因为人才产生的)
2. 软件和硬件有什么不同？What is Difference between 'Software' and 'Hardware'?
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