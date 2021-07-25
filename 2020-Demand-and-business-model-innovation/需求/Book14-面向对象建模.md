book14-面向对象建模
---

# 1. 课程相关内容
1. 直播电商
   1. 罗永浩连遇造假，羽绒服中间商为阎利珉，漱口水为虚假国外品牌
      1. 阎利珉是帮助阿里巴巴做聚划算失败。
      2. 漱口水质量不达标。
   2. 辛巴赔付燕窝后，广州工商判定虚假宣传，快手封禁账号60天
2. 腾讯申请注册"打工鹅"商标
3. 供应链品牌化
   1. 企业在有制造能力的基础上把它品牌化，使其主营业务变成产品和品牌战略
   2. 新零售的本质，宏观经济发展的必然
      1. 高频
      2. 消耗性
      3. 相对分散
      4. 可运输可存储
      5. SKU多却没有锚定价格
   3. 三只松鼠，南极人，小熊电器， 小米，石头科技，完美日记，珀莱雅名创优品，安克创新
   4. 最需要商业模式、设计思维与软件产品的支持
   5. 电商的出现使得销售和反馈的速度大加快，(更好的报合用户的真一实需要)，需要品牌的背书
4. 需求分析的主要任务
   1. 需求建模
   2. 需求细化
   3. 确定需求优先级
   4. 需求协商

# 2. 面向对象分析

## 2.1. 现实世界的复杂模型
1. 复杂总是简单部分的组合
2. 简单部分又是更简单部分的组合，简单组成复杂的过程存在层次性
3. 每个最小简单部分独立负责完成一系列相关任务
4. 相比较而言，每个组合内部各部分的关系比其内部与外部的关系都更紧密
5. 各个部分通过一致的**接口**进行组合，即一个部分对其它部分的所知仅仅是接口

## 2.2. 映射现实模型的面向对象思想
1. 任何系统都是能够完成一系列相关目标和任务的对象
   1. 对象完成一个任务时会请求一系列其他对象帮助其完成一些子目标
   2. 其他对象为了完成其任务又会请求将子目标更细分为子子目标，并请求其他对象帮助完成
   3. 子目标的分解和责任分担一直进行直到最后产生的子部分可以映射到计算实体
2. 计算实体：对象
3. 层次关系：继承与关联、聚合、组合
4. 组合接口：一个对象暴露的接口

## 2.3. 面向对象建模
1. 面向对象建模：一种用于辨识系统环境中的对象及这些对之间关系的技术(UML)
   1. OMT (James Rumbaugh)
   2. Booch方法(Grady Booch)
   3. OOSE (Ivar Jacobson)
2. Coad-Yourdon
3. Shlaer-Mellor
4. Fusion

## 2.4. UML
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/1.png)

1. 对象模型Object Model (Domain Model)
2. 用例模型Use Case Model(第7章)
3. 行为模型Behavior Model
   1. 顺序图
   2. 状态图
   3. 活动图(第5章)
4. 对象约束语言OCL

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/2.png)

1. 领域模型是粗略的结构模型
2. 我们是否将系统作为一个总体，在外部设计时不必，但是在设计系统整体的时候需要考虑
3. 面向对象分析与设计的关键是实现从用例模型到完全对象模型的过渡，包括如下步骤：
   1. 从用例描述中识别出应用领域的对象和类，建立分析类图(领域模型)。
   2. 从用例描述中识别系统行为,建立分析的行为模型(粗略行为模型)。
   3. 考虑设计要素，将分析类图转化为初始设计类图(细化的对象模型)。
   4. 基于初始设计类图，将分析的行为模型转化为设计的行为模型(细化的行为模型)。
   5. 综合考虑初始设计类图与设计行为模型,将系统行为分配给类,细化类的职责,建立完全的对象模型。
4. 面向对象分析与设计的步骤
   1. 使用面向对象方法进行需求获取，描述业务模型(活动图)，组织需求信息的用户描述，建立用例模型。
   2. 从用例模型一方面寻找对象和类，建立领域模型。另一方面建立行为模型，体现用例描述中的系统行为。
   3. 获取对用户需求的完成、准确理解后，考虑软件实现。
   4. 得到完整的对象模型后，进行程序编码
5. 对象模型(类图)：建立领域模型
6. 交互图、状态图：建立行为模型

# 3. 对象模型

## 3.1. 对象模型组成元素

### 3.1.1. 对象
1. 对象：对象是指在一个应用当中具有明确角色的独立可确认的实体 
2. 每个对象都要包含
   1. 标识：唯一的标识自己，引用 
   2. 状态：对象的特征描述，包括对象的属性和属性的取值 
   3. 行为：对象在其状态发生改变或者接收到外界消息时所采取的行动
3. 常见的事物都可以是对象
   1. 和系统存在交互的**外部实体**，例如人、设备、其他的软件系统等；
   2. 问题域中存在的**事物**，例如报表、信息展示、信号等；
   3. 在系统的上下文环境中发生的**事件**，例如一次外部控制行为、一次资源变化等；
   4. 人们在与系统的交互之中所扮演的**角色**，例如系统管理人员、用户管理人员、普通用户等；
   5. 和应用相关的**组织单位**，例如分公司、部门、团队、小组等；
   6. 问题域中问题发生的**地点**，例如车间、办公室等；
   7. 事物组合的**结构**关系，例如部分与整体的关系等。
4. 但是也有事物不是对象
   1. 无法界定的事物
   2. 纯粹的值
   3. 纯粹的行为
5. 成为对象的条件
   1. 独立可确认：能够从周围的环境中界定自己，相对于问题域。
   2. 明确的角色：职责，**职责是指对象持有、维护特定知识并基于知识行使固定职能的能力**
      1. 状态：对象的特征描述
      2. 行为：对象在其状态发生改变或接收到外界消息所采取的行动。
6. 对象：一个对象**维护其自身的状态**需要对外公开一些方法，**行使其职能**也要对外公开一些方法，这些方法组合起来定义了该对象**允许外界访问的方法**，或者说限定了外界可以期望的表现，它们是对象需要对外界履行的**协议(Protocol)** 
   1. 一个对象的整体协议可能会分为多个**内聚的逻辑行为组**，划分后的每一个逻辑行为组就描述了对象的一个独立职责，体现了对象的一个独立**角色**
   2. 如果一个对象拥有**多个行为组**，就意味着该对象拥有多个**不同的职责**，需要扮演多个**不同的角色**。 
   3. 理想的单一职责对象应该仅仅扮演一个角色：通过**关联和集成**构建更加**复杂的角色与概念**。
   4. 比如：学生对象的部分行为在学习时发生，部分在购物时发生，则可以划分为2组。
7. 对象具有标识、状态和行为。
   1. b是全局对象，它对系统内的所有其他对象都是可见的。
   2. b是a的一部分。
   3. b是被a创建的。
   4. b的引用被作为消息的一部分传递给了a。

### 3.1.2. 对象之间的关系：链接
1. 链接：对象之间的物理或业务联系 
   1. 链接通常是单向的，当然也有双向的链接存在
   2. 如果一个对象a存在指向b的链接，那就意味着a拥有对b的假设，关于b的行为和行为效果的假设。也就是说，b需要满足a的某些行为期望。
2. 导航和可见性
   1. 由a指向b的链接除了包含假设和期望因素之外，还意味着a能够在链接的指引下，正确的找到并将消息发送给b，即a可以导航到b
   2. 由a指向b的链接使得b对a可见，或者说a拥有b的可见性(Visibility)  
3. 建立a指向b的链接的途径：

## 3.2. 类

### 3.2.1. 概述
1. 类是共享相同属性和行为的对象的集合，它为属于该类的所有对象提供统一的抽象描述和生成模板
   1. 抽象描述称为**接口**(Interface)，定义了类所含对象**对外**的(其他类和对象)的统一协议
   2. 生成模板称为**实现**(Implementation)，说明了类所含对象的**生成机制和行为模式**

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/47.png)

### 3.2.2. 类的产生——分类
1. **类产生的关键是进行正确的分类**
2. 人们认识和处理具体事物时总会有意识或无意识的对它们进行归类，分为数据驱动和职责驱动两种
3. 数据驱动(Data-Driven)
   1. 将具有相同属性的对象归为一类
   2. 产生自哲学上传统的经典分类理论(Classical Categorization Theory) 
      1. 所有具有一个给定特性或共同特性集的实体组成一个类
4. 职责驱动(Responsibility-Driven) 
   1. 会依据事物的相似性而不是完全的相同性来进行事物的分类 
   2. 产生自哲学上的**概念聚类**(Conceptual Clustering)
      1. 使用概念描述而不是指定的特征来描述类别和事物，在进行事物分类时它会考虑概念之间的相似性，并将事物归入和其概念最为相似的类别   

### 3.2.3. 类的产生——抽象
1. 抽象是人们理解事物时常用的手段
2. 忽略特征的方式
   1. 水平层次上忽略一些特征，多用于对复杂事务的简化。无关属性排除。
   2. 在特征的垂直表达层次上忽略底层的细节。张三李四抽象为姓名。

### 3.2.4. 类的封装
1. 信息隐藏，封装。
2. 只公开对象为履行职责所必需的协议。

## 3.3. 类之间的关系

### 3.3.1. 关联
1. 指出了类之间的某种语义联系
2. 关联是类对其对象实例之间的无数潜在关系的描述
   1. 为关联赋予名称，表示关系的语义内涵。
   2. 将参与关联的类的数量表示为度数，用来度量关联的复杂度
   3. 使用最大基数和最小基数
   4. 如果一个关联同时有状态和行为，那么也可以视为关联类。
   5. 关联端上还可以标记可见性信息。

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/3.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/4.png) |
| --------------------- | --------------------- |

### 3.3.2. 聚合与组合
1. 组合：如果缺少则不能完成组合
2. 聚合：主要看和组合的区别

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/48.png)

### 3.3.3. 继承(泛化关系)
1. 如果一个类A继承了对象B，那么A就自然具有B的全部属性和服务，同时A也会拥有一些自己特有的属性和服务，这些特有部分是B所不具备的
2. 此时A被称为子类，B被称为父类。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/49.png)

### 3.3.4. 多态
1. 广义多态：一个对象在相似情景下表现出多个不同形态，或者多个对象在同一情景中表现出相同形态的现象
   1. 重载与泛型：是同一对象在不同情境下表现出不同形态的现象的抽象。
      1. 根据参数或返回值不同为协议定义不同的版本
      2. 同一个通用的实现处理不同的数据类型
   2. 狭义多态：多个对象在同一情景中表现出相同形态的现象 

## 3.4. 领域模型
1. 类大多是**概念类**(Concept Class)，是一个能够代表现实世界事物的概念
   1. 概念类之间存在指明语义联系的关联，这些关联通常不标记方向，也不标记关联端的可见性
   2. 概念类会显式的描述自己的一些**重要**属性，但不是全部的详细属性，而且概念类的属性通常没有类型的约束
   3. 概念类**不显式**的标记类的行为，即概念类不包含明确的方法
2. 一般都是一个简化后的类图。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/5.png)

## 3.5. 领域模型建模
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/50.png)

### 3.5.1. 识别候选对象与类

#### 3.5.1.1. 概念类分类列表
1. 这种方法事先给出一个概念类的分类列表，从中发现对象 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/6.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/7.png)

#### 3.5.1.2. 名词分析
1. 从文本描述中识别出有关的名词和名词短语，然后从中发现对象 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/8.png)

#### 3.5.1.3. 行为分析
1. 从需求描述中搜寻动词，识别出系统行为
2. 找到系统行为的而主动对象和被动对象作为候选对象

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/51.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/52.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/53.png)

### 3.5.2. 确定概念类
1. 如果候选对象既维持一定的状态，又依据状态表现一定的行为，那么它就应该是一个独立存在的对象 
2. 如果候选对象只有状态没有行为，那么就要分析它的状态是否是系统需要的数据。
   1. 如果系统需要它的状态数据，那么该候选对象就应该作为其他对象的属性出现在最终的领域模型当中。
   2. 否则，该候选对象应该被摈弃 
3. 如果候选对象只有行为没有状态，那么往往意味着需求信息的遗漏
4. 如果候选对象没有装填也没有行为，则摒弃。
5. 注意点
   1. 属性的复杂度问题：二维限制不应该出现在面向对象建模中，比如图书中的作者是一个复杂属性，我们也不应该将其抽象为一个对象，因为他没有自己的行为。
   2. 人们易于武断的将单值状态类抽象为其他类的属性：比如价格之于商品，价格本身可能会有一定的行为。

### 3.5.3. 建立类之间的关联
1. 保证类之间协作所必需的可见性：需要知道
2. 适当使用问题域内的关联，增强领域模型的可理解性，要适可而止
3. 不要在关联的识别上花费太多的时间，识别概念类比识别关联更加重要 
4. 避免显示冗余和导出的关联

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/54.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/55.png)

### 3.5.4. 添加类的重要属性
1. 实现类协作时必要的信息，是协作的条件、输入、结果或者过程记录 
2. 使用用户的描述方式，不进行类型和约束的严格定义 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/9.png)

### 3.5.5. 领域模型的分析作用
1. 发现数据方面的需求缺陷与不足，表现为数据的定义、加工与使用
2. 用例之间是互补的，有些用例的数据缺陷可以在其他用例的领域模型中得到补充

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/10.png)

# 4. 行为模型

## 4.1. 交互图
1. 以**一组对象**为中心的交互描述技术，描述在**特定上下文环境**中一组对象的交互行为 
2. **通常描述的是单个用例的典型场景**
3. 交互图中的每一个交互都描述了环境中的对象为了实现某目标而执行的一系列消息交换 
4. **顺序图**和通信图是最常用的交互图
5. 交互图中出现的对象应该在领域模型中有相应的对象存在 

## 4.2. 顺序图
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/11.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/56.png) |
| ---------------------- | ---------------------- |

1. 工作状态，生命线是双道线，表示对象处于激活态。
2. 不要绘制太长的激活态。
3. 组合片段
   1. opt:可选
   2. alt:多选一
   3. loop：循环
   4. break：满足条件执行其中语句后退出顺序图
   5. par:交织并行
   6. critical:关键原子操作，不可以被破坏
   7. strict:必须顺序执行
   8. seq:不同时间线上可以按照任意序

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/13.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/14.png) |
| ---------------------- | ---------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/15.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/16.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/17.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/18.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/19.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/20.png) |

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/57.png)

4. 引用顺序图

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/21.png)

## 4.3. 通信图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/58.png)

## 4.4. 系统顺序图
1. 系统顺序图：将整个系统看作一个黑箱的对象，强调外部参与者和系统的交互行为，重点展示系统级事件

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/12.png)

## 4.5. 建立交互图

### 4.5.1. 建立典型场景的系统顺序图
1. 确定系统顺序图的上下文环境
2. 找出参与交互的对象。
3. 根据发现的对象建立交互图框架。将对象平行排列，并添加对象的生命线。
4. 添加消息，描述交互行为：以消息的方式，将对象之间的交互行为描述出来，并建立行为之间的顺序。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/22.png)

### 4.5.2. 建立用例(多场景)的系统顺序图
1. 先为主流程场景建立基础的系统顺序图，然后根据分支场景与异常场景的分支点、异常点，建立组合片段描述

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/23.png)

### 4.5.3. 建立详细顺序图
1. 简单项目:系统顺序图
2. 复杂项目，系统顺序图粒度太大，可以考虑适度使用详细顺序图
3. 建立详细顺序图的关键是正确识别参与交互的对象，这个可以借鉴领域模型的工作
4. 详细顺序图仍然只是分析模型，不要添加设计因素

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/24.png)

### 4.5.4. 建立交互图，发现需求缺陷
1. 建立交互图时最常发现的问题是系统的**交互行为缺失**。
2. 组合片段和消息描述可能会发现**行为数据**的问题。如果一个交互消息的数据内容在领域模型中没有描述，就意味着其数据内容是缺失的。如果组合片段监护条件使用的数据内容在领域模型中没有描述，也意味着其数据内容的缺失。

## 4.6. 状态图
1. 以**状态机理论**为基础建立的对系统行为的描述手段
   1. 状态机是以"**状态**"概念为基础解释系统行为的一种技术
   2. 有限状态机FSM(Finite State Machine)是用于建模的最简单的状态机
   3. 在FSM技术基础之上，发展出了多种分支技术(FSM,STD,Yourdon,SDL,STM,SC)，UML的状态图SD(State Diagram) 也是其中之一。
2. 主要用于描述重要而且复杂的对象的所有行为：这个对象的行为通常要涉及很多(甚至大部分)的用例
3. 状态机理论
   1. 状态机理论认为，系统总是处于一定的状态之中。而且，在**某一时刻，系统只能处于一种状态之中**。
   2. 系统在任何一个状态中都是**稳定**的，如果没有外部事件触发，系统会一直持续维持该状态。
   3. 如果发生有效的**触发事件**，系统将会响应事件，从一种状态转移到唯一的另一种状态。
4. 如果能够罗列出系统所有**可能的状态**，并发现所有有效的**外部事件**，那么就能够从状态转移的角度完整的表达系统的所有行为 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/25.png)

### 4.6.1. 图示

### 4.6.2. 简单示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/26.png)

### 4.6.3. 状态图示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/27.png)

### 4.6.4. 组合状态
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/28.png)

### 4.6.5. 并发状态
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/29.png)

### 4.6.6. 入口与出口
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/30.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/31.png) |
| ---------------------- | ---------------------- |

### 4.6.7. 决策选择
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/32.png)

### 4.6.8. 汇集点
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/33.png)

> 注意监护状态

### 4.6.9. 中止与历史状态
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/34.png)

### 4.6.10. UML状态图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/59.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/60.png)

### 4.6.11. UML状态图示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/61.png)

## 4.7. 建立状态图
1. 确定上下文环境：搞清楚状态的主体常见的状态主体有：类、用例、多个用例和整个系统 
2. 识别状态，标记初始状态和结束状态：可能会不存在确定的初始状态和结束状态 
3. 建立状态转换

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/62.png)

4. 补充详细信息，完善状态图 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/35.png)

## 4.8. 建立状态图，发现需求缺陷
1. 如果状态图中发现有无法进入的状态或者无法跳出的状态，就意味着相应**行为**的缺失(需要重新需求获取)
2. 如果一个状态在发生触发时转移路线不确定，就意味着**监护条件数据缺失或者行为**需要细化
3. 如果应该建立的状态转移在需求内容中没有体现，就需要修正需求内容
4. 如果应该存在的状态在需求内容中没有体现，也需要修正需求内容

# 5. 对象约束语言OCL
1. OCL并不是UML中单独的一个模型，而是被应用在其他的模型当中，丰富其他模型的语义
2. OCL是一种**无副作用**的规约语言
   1. 以表达式的方式定义对其他模型元素的约束 
   2. 约束和限制其他模型元素的行为和状态变化
   3. 不会修改任何其他模型元素的表述 
3. OCL不是一种编程语言。
   1. OCL的首要定位是建模语言，因此它在保证一定表达能力的前提下，注重于语言的简洁性和抽象性 
   2. 它无法被用来描述程序的控制逻辑和工作流程，它的表达式定义也无法在程序中得到直接的执行 

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/36.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/37.png) |
| ---------------------- | ---------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/38.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/39.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/40.png) |                        |

## 5.1. 构成 

### 5.1.1. 类型
1. 包含原始数据类型、集合数据类型和针对UML模型的类型。

### 5.1.2. 表达式
1. 表达式 = 操作符 + 操作数

### 5.1.3. 保留关键字
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/63.png)

## 5.2. 主要应用

### 5.2.1. 不变量 
1. 不变量是可以对UML类元施加的约束
   1. 类元需要保持它的表达式取值在指定的时间范围内或者指定的条件下始终为"**真**"
   2. 最常见的是用来约束类的属性或者类的方法 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/41.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/64.png)

### 5.2.2. 前置条件和后置条件 
1. 前置条件要求类元在执行操作之前必须保证前置条件的表达式为真
2. 后置条件要求类元在操作执行完成之后必须保证后置条件的表达式为真 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/42.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/65.png)

### 5.2.3. 监护条件
1. 监护条件是对状态机模型中状态转移施加的约束
2. 在状态机到达转移点时，监护条件的表达式需要根据实际状态进行评估，并只有在表达式实际取值为"真"的情况下才进行转移 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/43.png)

# 6. 使用对象约束语言建立契约说明
1. 不需要为所有的系统行为都定义操作契约，可以有选择的为其中的一部分系统行为定义操作契约 
   1. 涉及到很多状态变化的复杂行为
   2. 因果关系比较微妙的模糊行为
2. 选择系统行为的选择时通常需要考虑以下两个因素
   1. 行为的复杂度
   2. 行为的清晰度

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/66.png)

## 6.1. 可以从下面几个角度进行约束的发现工作：
1. 不变量：系统行为中所涉及的敏感状态，这些状态的改变往往会产生广泛的连锁反应
   1. 不可改变的属性、不可改变的关联关系
2. 前置条件：行为发生和顺利完成所需要的系统的状态条件
   1. 合法的参数
   2. 有效的状态：对象的存在状态、对象的属性取值、有效的关联关系
3. 后置条件：行为顺利完成之后引起的系统状态改变
   1. 有效状态的改变，对象的存在状态、对象的属性取值
   2. 关联关系的改变

## 6.2. 示例
1. 操作: 输入物品项enterItem(ItemID, quantity)
2. 引用: 销售处理
3. 前置条件:
   1. 有一个销售si正在进行
   2. 有一个物品项列表sli存在
   3. si和sli建立了关联
   4. quantity介于[Minimum…Maximum]
   5. ItemID可以和某个物品描述实例spi建立联系
4. 后置条件:
   1. 创建了一个商品实例spi
   2. spi和sli建立了关联
   3. spi.quantity被置为参数quantity
   4. spi.itemID被置为参数itemID

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/44.png)

# 7. CRC
1. CRC是Candidates、 Responsibilities和 Collaborators三者的缩写
2. 基于CRC可以建立一种索引卡片，被称为CRC卡，每个卡片代表了一个被发现的候选对象 
3. 形式可能是多种多样的，卡片、纸张、黑板等等都可以作为CRC卡的介质载体 
4. CRC卡简洁方便，可以随时**被移动、修改或者丢弃**，所以它特别适合于在复杂的系统当中进行对象的发现和设计思想的挖掘，即进行复杂情况下的面向对象分析与设计

## 7.1. CRC卡示例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/45.png)

## 7.2. 基于CRC卡的职责驱动方法
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book14/46.png)

### 7.2.1. 确定主题
1. 找到系统中重要的主题
2. 业务需求和为满足业务需求而规划的系统特性来确定主题

### 7.2.2. 识别候选对象
1. 着手方面：
   1. 问题域中重要的对象和结构。
   2. 系统的控制和协调行为。
   3. 需要传递的重要信息流。
   4. 关联硬件和其他的关联系统。
2. 识别出候选对象后，为他们建立CRC卡，并给以合适的名称。

### 7.2.3. 描述对象特性
1. 在系统中的地位
2. 功能行为
3. 和其他对象的关系
4. 公共责任
5. 抽象级别
6. 复杂度

### 7.2.4. 发现系统职责
1. 系统所需要和维护的信息
2. 系统的功能和行为

### 7.2.5. 分配系统职责
1. 集中信息与行为
2. 维持对象的角色
3. 保持对象职责的相关性
4. 保持职责的合适粒度
5. 保持对象的粒度：不要承担过多的责任
6. 不要重复责任：不要重复分配责任
7. 必要时调整候选对象

### 7.2.6. 建立对象之间的协作
1. 角色：角色表明对象在系统和具体工作中的位置。
2. 任务：识别任务中的参与对象，分析任务中的责任分解、衔接和分解。
3. 职责：分析一个对象的职责，发现对象之间的写作。

# 8. 本章小结
1. 面向对象分析是90年代之后的主流分析方法，它以UML为基础，综合使用了多种不同的分析技术，主要有：
   1. 对象模型Object Model (Domain Model)
   2. 用例模型Use Case Model
   3. 行为模型Behavior Model
      1. 状态机模型
   4. 对象约束语言OCL
2. 面向对象分析任务的成功执行，除了要掌握多种面向对象分析技术之外，还需要掌握利用这些技术的建模方法
3. CRC方法是面向对象分析在处理复杂问题时的手段，但是它需要了解很多的建模知识才足以进行

# 9. 思考题
1. 在需求获取阶段，需求工程师收集了大量的样本，包括文档、表格和报告，解释这些样本对面向对象建模有哪些用处
2. 分析你所在学校使用的选课系统，给出它的详细和完备的面向对象分析模型描述。
