Book3-需求工程过程
---

# 1. 需求工程过程
1. 过程是一组相关活动的集成，通过这些活动的执行，可以完成一项任务或者达到一个目标。
2. 需求工程过程是系统开发当中需求开发活动的集成，他以用户所面临的业务问题为出发点进行分析和各种转换，最终生成一个能够在用户环境下解决用户业务问题的系统方案，并将其文档化为明确的需求

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/1.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/2.png) |
| -------------------- | -------------------- |

3. 如上右图，需求工程活动是相互交织的，整个开发活动也是不断迭代和递增的。
4. 不同的项目的需求工程过程不同
   1. 大规模的军用系统会有严格的需求工程过程
   2. 小型创新型软件公司需求工程可能仅仅是一些头脑风暴会议。
5. 从需求的层次性看需求开发

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/3.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/4.png) |
| -------------------- | -------------------- |

6. 常见的文档：
   1. 项目前景和范围文档：定义系统的业务需求，明确系统努力方向和工作范围。
   2. 用户需求文档：定义用户需求，以用户的立场表达了对系统行为的期望，比如用例文档。
   3. 需求规格说明文档：定义了系统的系统级需求，指出了开发者应该完成的任务。
      1. 系统规格说明：包含整个系统的需求
      2. 软件规格说明：软件需求

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/25.png)

# 2. 需求工程过程的活动

## 2.1. 需求获取
1. 需求获取是从**人、资料或者环境**当中获取需求的过程
2. 需求工程师必须要利用**各种方法和技术**来"发现"需求 
3. 需求获取和需求分析是**交织在一起**的：需求获取前半段确立项目前景与范围时使用的目标模型也可视作一类典型的基于建模的需求分析

### 2.1.1. 收集背景资料
深入了解需要构建知识框架，是与用户进行交流的知识基础。

### 2.1.2. 获取问题与目标，定义项目前景和范围
1. 生成业务需求，明确系统需要达到的目标。
2. 当用户之间发生需求冲突的时候，可以利用项目前景指导需求冲突的协商解决。
3. 需求获取面对的信息非常广泛：
   1. 不能在无关的内容上花费太大的代价。
   2. 不遗漏应该获取的重要内容。
4. 项目的业务需求、前景和范围都会被记录到项目的前景和范围文档中。
5. 文档内容有助于坚定投资人信心(项目明确化)

### 2.1.3. 识别涉众，选择信息的来源
1. 涉众分析：选择少数用户来代表全体用户，于是我们需要将用户进行分类，找到用户代表
2. 硬数据采样：表单、报表、备忘录等硬数据是需求获取信息的另一个重要来源：他们用更清晰、条例和准确的方式描述了实际业务，但是我们需要使用恰当的方法进行采样。
3. 相关的产品、文档和领域专家等也可能是需求的来源。

### 2.1.4. 选择获取方法，执行获取
面谈(调查表)、观察、原型(需要深入)

### 2.1.5. 记录获取结果(未精加工的原始信息) 
1. 需求获取阶段产生的主要成果有业务需求、项目前景和范围、用户需求以及问题域特性。
   1. 前景和范围文档记录**业务需求**
   2. 获取笔录记录**用户需求和问题域特性**
2. 获取的笔录可能存在凌乱、模糊等问题。

## 2.2. 需求分析
1. 需求分析的主要工作是建模来整合各种信息，以使人们更好地理解问题：信息的细化、为创造性活动提供支撑，完成内容的转化
   1. 为问题定义出一个**需求集合**，这个集合能够为问题界定一个有效的解决方案
   2. 检查需求当中存在的**错误、遗漏、不一致**等各种缺陷，并加以修正：利用模型本身的语法和赋予的语义
2. 需求分析的最后会产生一个需求的**基线集**。它指定了系统开发需要完成的任务。
   1. 基线集在有限资源条件下往往是用户所要求功能的一个子集。
   2. 基线集中的需求要求具有优秀需求的特性，尤其要解决不一致和冲突现象。

### 2.2.1. 背景分析
1. 由于系统必须和部署的环境互动才能解决用户的问题，所以在系统开发时，尤其是需求开发，研究系统所要部署的环境很重要。
2. 对环境的分析和理解，帮助需求工程师形成一个关于用户业务的知识框架，有利于在细节的需求获取活动中和用户有效交流。
3. 背景分析师研究系统环境的一部分。复杂环境需要使用专门的分析方法，如领域分析和企业建模。

### 2.2.2. 业务分析(问题分析、目标分析、涉众分析)，确定系统边界 (业务需求)
1. 系统边界的定义要能够保证系统和周围环境形成有效的互动，并在互动中解决用户的问题，满足业务需求。
2. 系统用例图和上下文图通常被用来定义系统的边界。

### 2.2.3. 软件需求建模
1. 建模是为展现和解释信息而进行的抽象描述活动。
2. 建模帮助需求工程师有更加深刻的理解，更方便进行信息的传递。
3. 需求建模技术有数据流图、实体关系图、状态转换图、类图等半形式化建模技术，以及Z模型等更加严格的形式化技术。

### 2.2.4. 细化需求
1. 用户需求往往具有模糊、歧义等诸多不理特征。
2. 依据模型得到系统级需求

### 2.2.5. 确定优先级
1. 定期评估和调整
2. 在开发资源有限和不足的情况要动态调整优先级。

### 2.2.6. 需求协商
1. 在分析中有时会发生不通过用户间的需求冲突，这种情况下用户各自的需求都是合理的，但是不可能在系统内同时被事项。
   1. 不同用户需求敌对
   2. 系统资源不足
2. 需求工程师要通过分析及时发现冲突，并为处理冲突提供技术上的参考信息，组织和指导用户之间的协商

## 2.3. 需求规格说明
1. 获取的需求需要被编写成文档，主要目的是为了**在系统涉众之间交流需求信息**
   1. 业务需求被写入项目前景和范围文档
   2. 用户需求被写入用户需求文档(或者用例文档)
   3. 系统需求被写入需求规格说明
2. 最重要的质量要求是**简洁、精确、一致和易于理解**。

### 2.3.1. 定制文档模版
1. 开发谈对在内部为各种需要编写的文档维护一些文档模板。
2. 参考IEEE1998推荐的规格说明文档。
3. 需求工程师需要再根据项目的特点对组织的参考模板进行进一步定制。

### 2.3.2. 编写文档
1. 选择最精确的表达方式
2. 保证文档的良好结构和易读性。
3. 方式
   1. 模型语言(图形、表达式等)：保证信息传递的准确性。
   2. 自然语言(文本)：保证该文档可读性。

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/5.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/6.png) |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/7.png) |                      |

## 2.4. 需求验证
1. 确保需求规格说明文档能**正确、准确**的反映用户的意图
2. 确保文档的高质量的标准
   1. 文档内**每条需求**都正确、准确的反映了用户的意图
   2. 文档记录的需求集在**整体**上具有**完整性和一致性**
   3. 文档的组织方式和需求的书写方式具有**可读性和可修改性** 

### 2.4.1. 执行验证
1. 同级评审：最常用
2. 原型：代价较高
3. 模拟：代价较高

### 2.4.2. 问题修正
修正后需跟踪以确保落实

## 2.5. 需求管理
1. 保证需求作用在整个软件的**产品生命周期**中的**持续、稳定和有效发挥**
2. 需求管理会进行变更控制，纳入和实现合理的变更请求，拒绝不合理的变更请求，控制变更的成本和影响范围。
3. 在企业界时间中，需求变更被认为是导致项目失败的两个主要原因之一。
4. CMMI(Capability Maturity Model Integration，软件能力成熟度模型集成)将其作为所有二级成熟度企业都应该具备的关键过程域。

### 2.5.1. 建立和维护需求基线集
1. 建立良好的配置管理，对基线进行版本控制，是进行有效需求管理的前提和基础。
2. 实现基线的版本控制，首先要标识每项需求，记录其相关属性，如ID、来源、产生日期、产生理由、优先级和预先实现成本等，然后为每一个需求文档建立唯一的版本号标识。
3. 建立版本控制后，所有的变更情况、变更日期和变更原因都要被记录，并且传达给被影响的每一个人。

### 2.5.2. 建立需求跟踪信息
1. 以系统级需求作为出发点。
2. 后向跟踪：跟踪各种系统级需求被设计、实现为哪些制品，并回溯每个设计、实现制品是为哪些需求存在的。
3. 前向跟踪：回溯每个系统级需求是为支撑哪些用户需求及业务需求存在的，并跟踪每个业务需求、用户需求是如何被转化为系统级需求。

### 2.5.3. 进行变更控制
1. 现实世界的多变性，项目建立基线后仍然应该及时响应外界的需求变化请求，但是必须是在控制下的，
2. 实现变更控制首先需要建立一个控制变更的流程以及相关策略，还需要挑选有经验的用户和开发人员组成变更控制团队，分析利益得失、是否接受。
3. 努力实现半自动化

# 3. 需求工程过程的并发和迭代性
需求开发是迭代的，其重要活动需求获取和需求分析是交织的。

## 3.1. 需求开发中的分析模型复杂度
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/11.png)

1. 理论上随着时间的延伸，获取的内容增加，整体复杂度应该一直线性上升。
2. 下降是因为可能发生了知识积累到一定程度的知识重构过程。
3. 获取、分析 $\rightarrow$ 重构 $\rightarrow$ 再获取、分析 $\rightarrow$ 再重构

## 3.2. 迭代的需求开发过程模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/12.png)

需求开发的迭代性

## 3.3. 需求开发活动的并发性
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/13.png)

1. 需求开发不仅仅是迭代的，各个活动之间还是并发的。
2. 其中，分类属于本书的需求分析活动。

# 4. 实践方法的应用
1. 个人才智$\rightarrow$实践方法$\rightarrow$知识体系
2. 工程领域经过相当时间的探索，从生产者大量个人行为中总结出了有效的工作方式和方法，和知识体系的要求还有较大的距离，但是它们可以很好的帮助人们完成工程实践，所以被称为实践方法(原则)
3. 需求工程师需要为组织或项目选择、定制和应用一些有效的实践方法 

## 4.1. 实践方法
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/26.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/27.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/28.png)

## 4.2. 管理实践
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/29.png)

# 5. 需求工程过程示例

## 5.1. 适用于软件开发螺旋模型的需求开发过程模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/14.png)

1. 螺旋模型用于风险驱动项目的需求开发
2. 协商与建模属于需求分析活动。

## 5.2. 依赖原型方法的需求开发过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/15.png)

1. 领域分析和原型开发属于需求获取活动。
2. 基础及高阶模型开发属于需求分析活动。
3. 同级评审、场景走查和涉众反馈属于需求验证活动。
4. 特点：借助原型和分析模型的验证作用，加上涉众评价、反馈，可以不依赖软件规格说明文档完成需求验证，然后将验证后的高质量需求写成文档。

## 5.3. HP公司的需求过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/16.png)

1. 将需求开发划分为两部分
   1. 系统工程的系统需求开发
   2. 软件工程的需求分析
2. 适用于创新性产品或大型项目开发。
3. 需要系统需求开发结束后通过可行性分析后，才能进行软件产品开发阶段。

## 5.4. Practices-Based
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/17.png)

1. 基于需求实践方法建立的需求开发过程，将需求实践方法划分为多种类型以进行过程的评价与改进
   1. 基础实践：完成最基本的需求开发任务，必备。
   2. 进阶实践：让需求工程某些部分更好。
   3. 优化实践：非必须，可以进一步提高需求工程效果。
   4. 依赖上下文的实践仅适用于特殊环境的时间。

## 5.5. Agile RE的七个实践
1. 面对面的交流胜过写规格说明文档(User Story)
2. 迭代式需求工程；
3. 将需求划分优先级做到极限；
4. 通过持续规划管理需求变更；
5. 原型法；
6. 测试驱动开发；
7. 用户评审会议与验收测试。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/18.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/30.png)

## 5.6. RUP
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/19.png)

1. 强调最优实践的同时给出一个可定制的过程框架。
2. 不同工作流共同完成需求开发工作。

# 6. 需求工程过程与软件工程

## 6.1. Waterfall
1. 软件的问题域比较成熟和易于明确化，并且需求也比较稳定
2. 不利于用户的有效参与
3. Waterfall

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/20.png)

## 6.2. Incremental
1. 软件的问题域比较复杂，但是业务非常成熟而且需求比较稳定
2. 不利于用户的有效参与
3. Incremental

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/21.png)

## 6.3. Spiral/Evolutional
1. 问题域极其复杂或者需求不稳定
2. 更好的应对需求的改变
3. 提高用户的有效参与度
4. 使得开发工作的协同和管理工作变得困难
5. Spiral/Evolutional

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/22.png)

## 6.4. Agile
1. 问题域不成熟，业务活动仍然在不断发展和改变
2. 能够很好的解决各种不确定性
3. 提高了需求工程阶段的成本，而且易于发生各种原型风险
4. Agile

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/23.png)

## 6.5. 概述
1. 需求工程过程更应该是软件工程过程的一部分，而不是独立出来作为单独部分
2. < Requirements Engineering and Software Project Success- An Industrial Survey in Australia and the US >
   1. 发现相比于需求方法本身的好坏，需求方法与软件开发方法的适配性更会影响项目的成败。这也就是说，需求开发方法与软件开发方法是否适配，比结果需求的好坏更能影响项目的成败
   2. 相比于应用领域的熟练性，一个项目管理者有效管理需求的能力更加重要;
   3. 没有必要在项目一开始就建立完备的需求，更好的方式在项目后续的阶段中逐步完善需求;

## 6.6. Software Process Model in Practices
1. < Requirements Engineering-The State of the Practice >, 2003 – 传统软工过程更重视需求工程过程

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/24.png)

# 7. 需求开发过程与软件工程过程的相互影响。
1. "需求工程"是正性活动:
   1. 前景与范围定义
   2. 涉众描述
   3. 分析模型
   4. 需求特征描述

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/8.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/9.png) |
| -------------------- | -------------------- |

1. 需求开发方法与软件开发方法是否适配，比结果需求的好坏更能影响项目的成败。
2. 需求对后续的影响：Requirements Engineering and Downstream Software Development: Findings from a Case Study, 2005
   1. 改进对细节的理解，改进对特征间依赖及复杂性的理解
   2. 节省精力浪费
   3. 看不见的好处：提升沟通
   4. 看不见的好处：帮助决策
   5. 估算
   6. 变更管理
3. How to Manually Trace during Process [Watkins & Neal, IEEE Software1994]

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book3/10.png)

# 8. Summary
1. 需求工程有着属于它自己的生命周期模型，存在着针对需求开发的需求工程过程 
2. 需求工程过程拥有一些常见的需求工程活动：需求获取、需求分析、需求规格说明、需求验证和需求管理 
3. 需求开发活动是互相交织、并发、迭代和递增 的
4. 需求工程过程的成功执行需要应用很多的有效实践方法
5. 在实践中，需求工程过程的差异性是非常大的
6. 因为处于前端，需求工程对后续软件开发活动的影响是非常深入的
