Book7-基于用例/场景模型展开用户需求获取
---

# 1. 相关新闻
1. 上市
   1. 千亿市值的泡泡玛特(12.11)
      1. 投资人对王宁的评价：学历平平，没正经上过班，说起话来表情平静，没感染力，团队也没有精英。
      2. 上市后：王宁性格沉稳，话不多，喜怒不形于色，拥有"消费创业者"的许多优秀品格。
   2. Airbnb上市(12.10)
      1. 12年，30-68-144(164)美元/股
      2. 国内：途家、小猪短租、美团民宿
2. 社区团购
   1. 京东入股兴盛，美团优选查贪腐
   2. 永辉超市彩食鲜获10亿腾讯投资：类似河马
3. B站跨年晚会
   1. 元气森林, TVB，武汉文旅，湖北广电
   2. 央视频(未来电视) 学而思 题拍拍
4. 宣传海报如下，包含了商业模式多种元素

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/24.png)


# 2. 用户需求获取活动的展开
1. 需求获取前半段：确定**项目前景与范围**
2. 需求获取后半段：以**场景/用例模型**展开获取
3. 三大要素：确定范围，模型与流程，获取方法

## 2.1. 注意事项
1. 要时刻检查**项目边界**，不能有需求遗漏：参照系统特性，围绕系统边界设计获取活动计划，范围内不遗漏，范围外排除
   1. 结构化：以系统与外界的输入/输出流为线索注意展开获取过程。
   2. 面向对象：以业务需求、系统特性、目标模型、活动图等前景与范围阶段的工作成果。
2. 多轮次"获取$\rightarrow$分析"最终完成用户需求获取。
3. 根据内容合理安排获取方法。
4. 及时组织已获取需求，为后续获取提供指导
   1. 充足的背景阅读
   2. 1+轮前景与范围，2+轮获取：开放 -> 封闭

### 2.1.1. 多轮次获取要点
1. 前景与范围阶段
   1. 准备：背景资料获取与分析
   2. 第一轮：问题分析(深入)
   3. 第二轮：高层解决方案制定(确认)
2. 用户需求获取阶段
   1. 准备：明确主题与内容，准备材料
   2. 第一轮：明确任务与任务中主要问题(深入)
   3. 第二轮：明确任务细节，澄清困难内容(技巧、困难)
   4. 第三轮：明确解决方案(确认)

### 2.1.2. 获取方法安排
1. 面谈：常规方法
   1. 集体面谈：快速方法
   2. 调查表：用户分散
   3. 头脑风暴："发明"需求
2. 不确定性：原型
3. 情景性：观察

### 2.1.3. 用户需求的组织
1. 场景/用例模型驱动
   1. 整理和归类需求获取行为得到的信息(框架) 
   2. 指导和组织需求获取行为的开展
   3. 为详细信息的分析提供背景基础和上下文知识 
2. 承上启下
   1. 展开上一层(业务需求)
   2. 准备下一层的展开(系统级需求)

## 2.2. 用户需求获取活动的主线索——用例/场景模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/1.png)

1. 目标模型用于组织系统的**目标、特性、任务**等与业务需求相关的内容,目标分析过程是建立目标模型并验证其**正确性、完备性、一致性**的过程。
2. 用例/场景模型用于组织用户需求的相关内容，用例/场景分析是建立用例/场景模型的过程，但用例/场景分析无法完成对用户需求相关内容**正确性、完备性、一致性**的验证。
3. 面向对象分析模型或结构化分析模型用于**描述软件解决方案的细节知识**，组织和指导系统级需求的建立。面向对象分析或结构化分析是建立面向对象分析模型或结构化分析模型的过程，同时还能够验证用户需求相关内容的正确性、完备性和一致性。
4. 用例/场景模型不是保证用户需求相关内容正确性、完备性、一致性的的主要手段。
5. 用例/场景模型能够及时地将每次需求获取活动的进展组织起来，展现、提供给分析活动，并在得到分析结果后进一步指导后续获取活动，所以其是用户 需求获取活动中的主线索。

# 3. 场景/用例

## 3.1. 为什么需要"用例与场景"
1. 场景是更为基本的元素，用例是一种特殊场景，是需求工程师在组织需求是更喜欢使用的场景类型。
2. 获取笔录：权宜之计
   1. 用户需求+问题域特性
   2. 混杂、不清晰等特性
3. 用例与场景
   1. 场景为单位
   2. 问题域特性或者用户需求+问题域特性
   3. 组织清晰

### 3.1.1. 场景
1. [Zorman1995]将场景定义为对系统和环境行为的**局部描述**
2. [Plihon1998]将场景定义为对**行为或者事件序列**的描述，序列中的行为和事件是系统需要完成的一个任务的特殊示例。
3. [Jarke1996]认为场景包含有行为序列和行为发生的环境，环境描述了行为的主体、客体和上下文设置
4. 以上的描述都不足以作为场景的准确定义，人们也很难给场景下一个非常准确的定义[Rolland1998a]
5. **场景强调系统同外部环境互动以完成预期任务**，具有**重点描述真实世界**(商业模式设计：讲故事->场景)的特征，它利用**情景、行为者之间的交互、事件随时间的演化**等方式来叙述性的描述系统的使用 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/3.png)

### 3.1.2. 用例定义
1. 用例
   1. 相关**场景集合**的叙述性的**文本描述**
   2. 用例的概念是[Jacobson1992]最先在Objectory方法中提出的
2. UML将用例定义为"在**系统(或者子系统或者类)和外部对象的交互**当中所执行的**行为序列**的描述，包括各种**不同的序列和错误的序列**，它们能够联合提供一种**有价值的服务**"[Rumbaugh2004]。
3. 每一个行为序列成为一个场景。一个用例是多个场景的集合，用例承载了目标相关的成功和失败的场景。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/30.png)


### 3.1.3. 用例与场景
1. 以用例/场景为单位组织用户需求(和问题域特性)
2. 很受实践者欢迎
   1. 易于接受
   2. 易于使用
   3. 用例驱动！
3. 方法多样，差异性很大
   1. 也可以用来处理业务需求和系统级需求
   2. 还可以用来处理设计问题、测试问题……

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/5.png)

## 3.2. 场景/用例的组织特点
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/6.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/7.png) |
| -------------------- | -------------------- |

1. 左图左侧是用例/场景的组织方式，将原本独立的多个需求组织成一个个故事，让用户、客户等领域中的涉众看起来更容易接受，受涉众欢迎。
2. 左图右侧是各自独立方式组织成的所有需求，每一个需求都独立于其他需求，更符合开发者视角，受开发者欢迎。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/11.png)

3. 弱点
   1. 只考虑**其他内容与功能需求**之间的联系，却无法描述其他内容相互之间的联系，例如质量需求的相互依赖(目标模型)、界面需求的跳转(对外接口中的人机交互文档)、对外接口需求与质量需求的联系(IF作为主体承载目标实现)…
   2. 只考虑存在**联系**的事实，却无法分析联系的**合理性**，例如有无遗漏功能需求、数据需求及业务规则是否充分、质量需求是否可行(需求分析)
4. 所以，虽然用例/场景的**优点**非常明显，但它毕竟只是一种组织形式，不能寄希望于单凭用例/场景模型解决所有问题[Gottesdiener2002]，目标模型、面向对象分析模型或结构化模型等其他的模型形式仍然是必要的。

## 3.3. 用户/场景的层次性
1. 用户/场景是有层次性的，用来组织业务需求内容，如下图。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/31.png)

2. 可以用于组织用户用例的内容。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/32.png)

3. 可以用于组织系统级需求

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/33.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/34.png) |
| --------------------- | --------------------- |

## 3.4. 基于用例/场景进行软件开发
1. 以用例驱动的软件开发某种程度上就是需求驱动的软件开发。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/4.png)

# 4. 用例/场景模型
1. 用例/场景模型更多是需求内容的组织内容，一直没有形成严谨、准确的语法。
2. 场景的差异性模型如下：

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/8.png)

## 4.1. 场景定位

### 4.1.1. 场景的形式：场景的表达模式  
1. 描述(Description) 
   1. 表示法的正规性
      1. 非形式化语言：完全自由、没有任何规则
      2. 半形式化语言：有一定规则但不严格
      3. 形式化语言：有形式化体系，完备的语法、语义和语义
   2. 媒介形式(Medium)：叙述性的自由文本、结构化文本、强限制文本(半形式化)、建议使用表格、图表、图像等非形式化语言。
2. 外观：场景被表达出来时的效果
   1. 静态外观(主)：展现为一个或者数个描述性的文本或者图片。
   2. 动态外观：以动态的方式展现出来，用户可以按照时序查看。
   3. 交互外观：用户可以一定程度上控制和改变场景的变化时序和效果。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/9.png)

### 4.1.2. 场景的内容
1. 主要关注点：关于现在的，关于未来的，**关于解决方案的**
2. 环境范围：
   1. 系统内部的行为细节
   2. 系统和应用环境交互
   3. 系统和外部环境交互
   4. 提倡把组织背景、文化背景和目标等环境上下文信息描述包括在场景的内容中国。
3. 抽象层次
   1. 具体的(实例场景)：对个别行为者、事件、情节的细节描述，很少或完全没有抽象内容，张三去某个ATM取1000元钱
   2. 抽象的(类型场景)：以经验中的类别和抽象概念来描述事实，储户在ATM上取钱。
   3. 混合的：部分具体部分抽象，储户要从ATM中取1000元钱。
4. 覆盖范围：**功能需求**，非功能需求 
5. 粒度
   1. 整个业务过程(前期)
   2. **某个任务的完成过程**(中期)
   3. 某个交互行为的详细处理步骤(后期)
6. 示例类型
   1. **正常流程**
   2. 异常流程

### 4.1.3. 场景的目的
1. 描述(descriptive)：记录已经得到的需求，即整理每次需求获取行为中得到的信息。
   1. 需求的文档化
   2. 需求协商的基础
2. 探索(exploratory)：**主要使用**
   1. 需求获取：以需求为关注点进行探索
   2. 需求建模与分析：以解决方案为关注点
3. 解释(explanatory)：使用示例来说明原因或可行性
   1. 降低模型复杂度
   2. 需求的验证 

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/10.png)

### 4.1.4. 生命周期
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/35.png)

1. 实践中发现的场景应用和处理可以概括为5种情况
   1. (比较复杂的系统)从当前系统中捕获和建立关于**现在**的场景，它们描述问题域的状态和问题。对现在的场景做**进一步的分析**，转化产生关于**未来的场景**，描述期待中系统的**解决方案**。将关于未来的场景进行**文档化**，产生系统的需求规格说明，如图7-13(a)所示。
   2. (比较简单的系统)在当前系统中分析问题和期望，捕获、分析和建立关于未来的场景。然后再将关于**未来的场景进行文档化**，产生系统的需求规格说明，如图7-13(b)所示。
   3. (主要)在当前系统中分析问题和期望，捕获、分析和建立关于未来的场景，并依据场景描述建立需求模型。在这种情况下，需求工程除了场景之外不会再产生专门的需求规格说明，而是**以场景作为需求规格说明的替代**，如图7-13(c)所示。
   4. (有已有部分和逆向部分)依据已经建立的需求规格说明，解释和建立关于未来的场景，然后为场景中描述的解决方案建立需求模型，如图7-13(d)所示。
   5. (需求验证)依据需求规格说明所描述的解决方案建立需求模型。同时建立能够验证解决方案的场景，最后使用场景来验证需求模型的正确性，如图7-13(e)所示。
2. 场景信息是通过面谈、原型、观察等基础需求获取方法得到的。

## 4.2. 用例定位
1. 用例是场景方法中的一种

### 4.2.1. 用例的定位
1. 用例是**静态的结构化文本**描述。
2. 用例的内容可以是对当前世界的描述，也可以是对将来确定的解系统的内部行为描述，还可以是对一种**期待的解决方案的描述**。
3. 用例可能会被用于描述系统内部的交互(系统级需求)，也可能被用于**描述系统和环境的交互(用户需求)**，还可能会被用于描述行为的环境和背景(业务需求)，倾向于第二种。
4. 用例是类型层次的事件描述，**主要用来描述功能需求**，**可以包含其他类型的需求**
5. 用例可以比较抽象，也可以比较具体，也可以非常具体。
6. 用例的内容既包含有正常流程，又包含有异常流程。
7. 用例可以用于各种目的的应用(**同场景**)，包括描述、探索和解释。需求获取和需求验证是它在需求工程中的主要应用阶段，它也可以用于需求的建模、交流和协商。
8. 场景的各种生命周期特征根、应用和处理过程都适用于用例。
9. 高层功能需求获取完前不允许使用功能分解方式的。

### 4.2.2. 用例的含义和用法
1. 主参与者：提出请求的用户
2. 辅助参与者：实现主参与者的目标过程中被系统请求的外部对象。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/36.png)

## 4.3. 用例模型

### 4.3.1. 用例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/37.png)

### 4.3.2. 参与者
1. 参与者是与系统进行交互的角色。
2. 参与者可以是一个组织、另一个系统、外部设备或事件概念。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/38.png)

### 4.3.3. 关系

#### 4.3.3.1. 关联
1. 关联：用例和参与者之间的关系，描述了用例与参与者的交互。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/39.png)

#### 4.3.3.2. 包含
1. 多个用例发生相同得到行为，我们可以抽象出来成为抽象用例。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/40.png)

#### 4.3.3.3. 扩展
1. 不修改原用例，建立新需求的附加用例，使用附加用例扩展原有用例。
2. 执行附加用例前优先执行原有用例的流程。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/41.png)

3. 降低复杂度，表示用例的复杂处理行为扩展

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/42.png)

#### 4.3.3.4. 用例泛化
子用例继承了父用例的特征并增加了新的特征。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/43.png)

#### 4.3.3.5. 参与者泛化
子参与者继承了父参与者的特征并增加了新的特征。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/43.png)

### 4.3.4. 系统边界
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/44.png)

# 5. 基于场景/用例模型展开需求获取
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/16.png)

1. 基于前景与范围建立初始用例模型：依据系统用例图、目标模型建立初始用例/场景模型
2. (迭代)展开用例
   1. 据用例/场景模型指导获取，完善层次结构：选择合适的需求获取方法获得用例的详细描述，比如面谈、原型、头脑风暴、观察…
   2. 使用用例/场景组织获取内容
   3. 分析用例/场景发现仍需获取的需求内容
      1. 选择合适的模型分析用例描述
      2. 类图、顺序图、实体关系图、业务规则模型……
3. 验证场景/用例模型：评审用例描述
4. 维护用例/场景模型
   1. 用新组织或修正的用例/场景完善用例/场景模型
   2. 依据用例/场景模型组织需求分析模型

## 5.1. 依据系统用例图和目标模型建立初始场景/用例模型
场景的逐层展开不等于用例！

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/17.png)

## 5.2. 根据用例/场景模型指导需求获取，完善层次结构
1. 初始系统用例涉及的**主题**需要获取。
2. 概要用例描述中发现的**新主题**需要获取。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/45.png)

3. 具体用例中发现的**模糊、不正确、不完备**等细节内容需要再获取

## 5.3. 用新组织或修正的用例/场景完善用例/场景模型
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/46.png)

## 5.4. 根据用例/场景模型组织需求分析模型
1. 系统复杂度比较高，我们从局部需求分析入手，避免需求遗漏，保证各部分一致性。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/47.png)

## 5.5. 分析用例/场景发现仍需要获取的需求内容
1. 用例/场景没有验证内容正确性、完备性和一致性，我们需要使用分析技术来验证。

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/48.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/49.png) |
| --------------------- | --------------------- |

2. 最左图的交互不足，修正为改进一：无法绘制系统顺序图。
3. 改进一对于数据的描述不足，修正为改进二：无法建立概念类图。

## 5.6. 例子
1. 正常流程(触发条件，每天晚上)
   1. **车队**报勤，包括**人员**报勤和**车辆**报勤
   2. 如果有新任务，新建用车计划。
   3. 根据用车计划，开具路单
   4. 为路单开具出门证。
2. 扩展流程
   1. `3a`没有用车计划，也有可能开路单。
   2. `3b`开路单的车辆选择也可能不算报勤车辆
   3. `4`没有路单，也有可能单开出门证。

| 展开用例              | 组织获取内容          |
| --------------------- | --------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/18.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/19.png) |
| 用例展开              | 组织获取内容          |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/20.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/21.png) |

3. 面谈报告：面谈对象：调度人员-车辆报勤

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/22.png)

## 5.7. 使用分析模型(行为+结构)分析用例描述
1. 收银员输入会员编号；
2. 收银员输入商品；
3. 系统显示购买信息；
收银员重复2-3步，直至完成所有输入
4. 系统显示总价和赠品信息；
5. 顾客付款；
6. 系统找零；
7. 系统更新数据；
8. 系统打印收据；
9. 顾客离开

### 5.7.1. 流程细化改进
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/23.png)

### 5.7.2. 交互明晰(信息传递)改进
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/25.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/26.png) |
| --------------------- | --------------------- |

## 5.8. 用例文档
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/27.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Demand-and-business-model-innovation/需求/img/book7/28.png) |
| --------------------- | --------------------- |

# 6. 本章小结
1. 需求获取的展开过程是递进、迭代的，场景/用例模型在其中起着重要的作用
2. 场景/用例是需求的组织手段，是一种更为用户接受的需求线索表达方式
3. 在实践中，场景/用例模型有很大的差异性，要正确掌握和使用需求的场景/用例特点
4. 围绕场景/用例模型为核心，可以展开用户需求的获取活动
