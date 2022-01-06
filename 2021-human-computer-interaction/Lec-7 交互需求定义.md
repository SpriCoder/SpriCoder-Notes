0.1. Lec-7 交互需求定义
---

# 1. 背景
1. 无论取代或更新已有系统，还是开发新产品，需求的建立都是非常重要的
2. 需求获取是项目设计的第一个阶段
   1. 确定和记录现有的工作流程：收集
   2. 将信息组织起来，整体上涵盖工作的各个方面：描述
3. 产品是不同的：对需求提出了特殊的要求
4. 用户是不同的
   1. 人有不同的能力和弱点
   2. 有不同的背景和文化
   3. 不同的兴趣、观点和经历
   4. 人的年龄和身材高矮不同

# 2. 需求是什么
1. 需求
   1. 关于目标产品的一种陈述，它指定了产品应做什么，或者应如何工作
   2. 应该是具体、明确和无歧义的
      1. “完整下载任何网页的时间应少于5秒”
      2. “女孩们应觉得这个网站吸引人”
2. 需求活动
   1. 搜集数据
   2. 解释数据
   3. 提取需求

## 2.1. 产品特性
1. 功能不同
   1. 智能冰箱：应能够提示牛奶已用完
   2. 字处理器：系统应支持多种格式
2. 物理条件不同
   1. 移动设备运行的系统应尽可能小，屏幕显示限制
3. 使用环境不同
   1. 物理环境：如操作环境中的采光、噪音和尘土状况
   2. 社会环境：是否要共享数据，同步还是异步？
   3. 组织环境：用户支持的质量、响应速度如何？是否提供培训资源或设施？
   4. 技术环境：产品应能运行于何种平台上？应与何种技术兼容？
4. 一些例子
   1. KordGrip键盘：一只手操作的计算机
   2. 智能交通灯：SCOOT(Split Cycle Offset Optimisation Technique)系统，行人分段偏移优化技术

## 2.2. 用户特性
1. 心理学原理部分，假设每个人都有相似的能力和局限性
   1. 合理的，心理学原理可以适用于大多数人
2. 交互产品设计人员应该意识到个性的差异
   1. 用户并不是完全相同的
   2. 在设计中尽可能地体现这些差异
3. 用户差异
   1. 体验水平
   2. 年龄
   3. 文化
   4. 健康

## 2.3. 体验水平差异
1. 背景
   1. 程序员只创造适合专家的界面
   2. 市场人员要求只适合新手的交互
   3. 数目最多、最稳定和最重要的用户群是中间用户
   4. 中间用户往往被忽略
2. 设计目标
   1. 让新手快速和无痛苦地成为中间用户
   2. 避免为想成为专家的用户设置障碍
   3. 让中间用户感到愉快
3. 因为他们的技能将稳定地处于中间层

## 2.4. 不同类型的用户

### 2.4.1. 新手用户
1. 特点
   1. 敏感，且很容易在开始有挫折感
2. 设计要求
   1. 不能将新手状态视为目标
   2. 让学习过程快速且富有针对性
   3. 确保程序充分反映了用户关于任务的心智模型
   4. 无论什么样的帮助，都不应该在界面中固定
   5. 具有向导功能的对话框帮助较好：不要使用在线帮助作为学习指导
   6. 菜单项应该是解释性的

### 2.4.2. 专家用户
1. 特点
   1. 对缺少经验的用户有着异乎寻常的影响：“专家说不好就不好”
   2. 欣赏更新的且更强大功能
   3. 不会受到复杂性增加的干扰
2. 设计要求：对经常使用的工具集，要能快速访问

### 2.4.3. 中间用户
1. 特点
   1. 需要工具
   2. 知道如何使用参考资料
   3. 能够区分经常使用和很少使用的功能
   4. 高级功能的存在让永久的中间用户放心
2. 设计要求
   1. 工具提示（Tooltip）是适合中间用户最好的习惯用法
   2. 在线帮助是永久中间用户的极佳工具
   3. 常用功能中的工具放在用户界面的前端和中心位置
   4. 提供一些额外的高级特性

## 2.5. 年龄差异
1. 老年人
   1. 65岁以上的老年人中多数有某种残疾
   2. 技术应能提供对残缺部位的支持，如听觉、言语和灵活性
   3. 设计必须清楚、简单并且容许出错
   4. 利用冗余来支持信息访问
2. 儿童
   1. 在为儿童设计交互式系统时让他们参加很重要
   2. 允许多种输入模式（包括触觉或手写）
   3. 通过文本、图形和声音呈现信息的冗余显示也将增强他们的体验

## 2.6. 文化差异
1. 在不同的文化中符号有不同的意思
   1. 勾（√）和叉（X）分别表示肯定和否定
   2. 不能假设每个人都以同样的方式解释符号
2. 姿势的理解存在差别
   1. 点头vs.摇头
3. 颜色的使用
   1. 红色和绿色在不同的国家意味着不同的事物
   2. 通过冗余阐明特定颜色的指定意义

## 2.7. 健康差异
1. 每个国家至少有10%的人口有残疾
2. 视觉损伤
   1. GUI应用的增加降低了视觉损伤用户应用的可能性
   2. 辅以声音的应用和触觉的应用（Hearme，seeing AI）
3. 听觉损伤
   1. 较视觉残疾对与图形界面交互的影响要小：界面中多媒体的增加和声音的应用带来了交互困难
   2. 给听觉内容加文字描述
   3. 姿势识别可作为信息输出方式
4. 身体损伤
   1. 如在控制和应用手的移动方面存在差别
   2. 语音输入和输出对那些没有言语障碍的人是一种选择
   3. 用姿势和眼球移动的跟踪进行控制
5. 语音损伤
   1. 提供合成语音和基于文本的通信：语音合成必须快速地反映自然会话的步调
6. 诵读困难
   1. 提供拼写更正功能
   2. 一致性的导航结构和清晰的标识提示

# 3. 找到你的用户
1. 明确定位

## 3.1. 用户建模
1. 每个用户都是不同的，如何使用用户的研究数据设计出满意的产品呢？
2. 人物角色（Personas）
   1. 不是真实的人
   2. 是基于观察到的那些真实人的行为和动机，并且在整个设计过程中代表真实的人
   3. 是在人口统计学调查收集到的实际用户的行为数据的基础上形成的综合原型
   4. 概念简单，但使用起来相当复杂：拼凑出几个用户档案是不行的

## 3.2. 人物角色的作用
1. 解决产品开发过程中出现的3个设计问题
   1. 弹性用户
      1. 为弹性用户设计赋予了开发者根据自己的意愿编码，而仍然能够为“用户”服务的许可
      2. 如设计医院产品时，考虑设计能够满足所有护士的产品
   2. 自参考设计
      1. 设计者或者程序员将其自己的目标、动机、技巧及心智模型投射到产品的设计中
   3. 边缘情况设计
      1. 必须考虑边缘情况，但它们又不应该成为设计的关注点
      2. 问：A会经常进行这种操作吗？

## 3.3. 人物角色的构造
1. 错误观点
   1. A：专业开发人员知道什么可行，什么对用户最合适
   2. B：用户最了解他们需要什么，应当让他们指导设计工作
2. 人物角色
   1. 与某个系统有关的用户假定的一组公共需要、兴趣、期望、行为模式和责任
   2. 这些属性可能是若干用户共有
   3. 同一个用户也可以扮演系统的任意个不同角色
   4. 举例：频繁使用文字处理软件的用户
      1. 写作者的角色
      2. 编辑者的角色
      3. 排版者的角色

## 3.4. 人物角色的构造
1. 基于如下问题
   1. 谁将使用系统？
   2. 这些用户属于哪些类型的人群？
   3. 是什么因素决定他们将怎样使用系统？
   4. 他们与软件的关系有什么特征？
   5. 他们通常需要软件提供什么支持？
   6. 他们对软件会有怎样的行为？他们对软件的行为有什么期望？

## 3.5. 举例
1. 设计运行在笔记本电脑上的一个演示程序包
   1. 销售部的一位同事
   2. 公司的销售代表
      1. 能快捷方便地创建标准格式的简单幻灯片
      2. 能使用带有项目的文字内容或简单图表
      3. 图形依靠软件提供的标准图形库
2. 人物角色：日常最低要求演示者
   1. 经常使用；快速、方便操作；简单使用；
   2. 简洁、标准格式：带有项目符号的列表、条形图、饼图、图形等；标准图形库

## 3.6. 注意
1. 要注意那些与软件用户界面设计有关的角色特征
2. 要关注使角色之间彼此相区别的特征
3. 要留心焦点角色：最常见、最典型的角色

## 3.7. 建模过程
1. 拼凑：采用头脑风暴方法，产生一些零碎概念或模型的片段，先不去考虑他们的细节
2. 组织：将这些片段按照所构造模型的需要进行分组和分类，归并或删除那些冗余重叠的东西
3. 细节：建立和完善相应描述，补充遗漏的数据
4. 求精：对模型进行推敲，以便改进和完善
5. 以上过程循环反复

## 3.8. 人物角色的信息组织

# 4. 需求获取

## 4.1. 需求获取——观察
1. 设计的最初，可能不知道问什么问题或由谁来回答这些问题
2. 没有与参与者实际的讨论和观察是不可能得到完整的工作流程画面的
3. 有用的信息可以通过观察人们在工作环境中完成他们的活动来获得
4. 直接观察
   1. 陪同他们工作而直接获得信息
   2. 可能影响被观察者的日常活动：可提问：这是你通常完成任务的方式吗
5. 间接观察
   1. 用视频/录音获得信息
   2. 观察者更舒适

## 4.2. 场景
1. 场景是表示任务和工作结构的“非正式的叙述性描述”
   1. 以叙述的方式描述人的行为或任务，从中可以发掘出任务的上下文环境、用户的需要、需求
   2. 形式可以类似于一篇故事、一个小品或者在给定环境下按照时间顺序的一段情节
2. “讲故事”是人们解释自己做什么或者希望执行某个任务的最自然方式
   1. 故事的焦点就是用户希望达到的目标
   2. 若场景说明不断提到某个特定形式、行为或者地点，就表明它是这个活动的核心内容
3. 来源：场景说明通常来自专题讨论或者访谈，目的是解释或讨论有关用户目标的一些问题

## 4.3. 场景举例
1. 图书馆目录服务系统的潜在用户场景

```
“我要查找George Jeffries 写的书，但不记得书名，只知道它是在1995 年前出版的。我在目录系统中输入口令。我不明白为什么要输入口令，但不这么做我就无法进入图书馆系统，使用目录服务。系统确认了口令之后，显示了一些检索选项，如根据作者或日期检索，但不能结合两者进行检索。我选择了基于作者的检索，因为根据日期的检索通常会返回过多的书目。约30 秒后，系统返回了结果，说没有找到George Jeffries 写的书，也列出了一些最接近的匹配书目。在浏览了这个清单后，我发现把作者的名字弄错了，应该是Gregory 而不是George。于是。我选择了想要的书目，系统即显示了它的位置。”
```

2. 以上场景说明的问题
   1. 正确输入作者姓名的重要性
   2. 用户对输入口令感到反感
   3. 应提供更灵活的检索方法
   4. 在匹配不成功时，应给出相近的检索结果

## 4.4. 人物角色+场景剧本→需求
1. 需求定义的5个步骤
   1. 创建问题和前景综述
   2. 头脑风暴
   3. 确定人物角色的期望
   4. 构建情境场景剧本
   5. 确立需求
2. 迭代的过程
   1. 直到需求变得稳定

### 4.4.1. 第一步：创建问题和前景综述
1. 设计问题综述应该简明地反映需要改变的情况，来服务人物角色和提供产品给人物角色的商业组织
2. 前景综述高层次的设计视图和需求是问题综述的倒置
3. 设计新的产品P会帮助用户实现目标G，这让用户能更好地（精确度和效率等）完成X、Y和Z任务，并且不会产生其现在遇到的A、B和C等问题。从而会有力地改善H公司的顾客满意度，并且会增加市场占有率。

### 4.4.2. 第二步：头脑风暴
1. 目的
   1. “说反话”
   2. 尽可能地去除成见，允许设计师以开放和灵活的方式想象来构建场景剧本，使用他们的思维从场景剧本中得到需求
   3. 将头脑置于“解决问题模式”中
2. 特点
   1. 不受约束且不加以评判
   2. 不要花费太多时间，当想法重复或变慢时停止

### 4.4.3. 第三步：确定人物角色的期望
1. 一个人的心理模型通常是根深蒂固的
2. 界面表现模型与用户心理模型尽量匹配是非常重要的
3. 对于每一个基本和次要人物角色，需确定
   1. 影响人物角色愿望的态度、经历、渴望，以及其他社会、文化、环境和认知因素
   2. 人物角色在使用产品体验方面可能有的一般期待和愿望
   3. 人物角色认为什么是数据的基本单元或者元素
4. 理清如下问题
   1. 主体首先提到的是什么？
   2. 他们使用哪些动作单词？
   3. 他们没有提及对象中的哪些中间步骤、任务或者对象？

### 4.4.4. 第四步：构造情境场景剧本
1. 情境场景剧本
   1. 关注人物角色的活动，及其心理模型和动机
   2. 将注意力集中在设计的产品中怎样能够最好地帮助你的人物角色达到目标
   3. 应该专注于高层次的从用户角度描述的行动，广而浅：不应描述产品或交互的细节
2. 解决的问题
   1. 产品是否会被使用很长一段时间？
   2. 人物角色是否经常被打断？
   3. 和其一起使用的其他产品是什么？
   4. 人物角色需要做哪些基本的行动来实现目标？
   5. 使用产品预期的结果是什么？
3. 情境场景剧本举例
   1. 第1次迭代
      1. 人物角色Vivien Strong
         1. 女，32岁，已婚，女儿Alice
         2. 印第安纳波利斯市的一个房地产代理商
         3. 目标是平衡工作和家庭生活
         4. 紧紧抓住每一个交易机会并且让每一个客户都感觉自己是Vivien的唯一客户
      2. 情景场景剧本
         1. 在早晨做好准备，Vivien使用电话来收发电子邮件。它的屏幕足够大，并且网络连接很快。因为早上她同时要匆忙地为女儿Alice准备带到学校的三明治，这样手机比计算机更方便
         2. Vivien收到一封Email，来自最新客户Frank，他想在下午去看房子。Vivien在几天前已经输入了他的联系信息，所以她现在只需要在屏幕上执行一个简单的操作，就可以拨打他的电话
         3. 在与Frank打电话的过程中，Vivien切换到免提状态，这样她能够在谈话的同时看到屏幕。她查看自己的约会记录，看看哪个时段自己还没有安排。当她创建一个新的约会时，电话自动记录下这是与Frank的约会，因为它知道她是在与谁交流。谈话结束后，她快速地输入准备看的那处房地产的地址
         4. 将Alice送到学校之后，Vivien前往房地产办公室收集另一个会面所需的信息。她的电话已经更新了其Outlook约会时间，所以办公室里的其他人知道她下午在哪里
         5. Vivien拿起了电话——Alice错过了公交，需要接她。Vivien给她的丈夫打电话看他能否代劳，可是访问的却是其语音信箱，他肯定是不在服务区内。她给自己的丈夫留言，告诉他自己和客户在一起，看他能否去接Alice。5分钟后，电话发出了一个简短的铃音。从音调中，Vivien可以判断出这个短信是丈夫发给她的。她看到了丈夫发出的短消息：“我会去接Alice，好运！”
      3. 注意
         1. 没有涉及太具体的界面和技术信息
         2. 活动是和Vivien的目标相关的：尽可能去掉多余的任务
   2. 由场景生成故事板：突出关键交互动作、关键任务

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec7/1.png)

### 4.4.5. 第五步：确定需求
1. 同上例：直接从约会记录（情境）中拨打电话（动作）给某个人（对象）
2. 数据需求
   1. 必须在系统中被描绘的对象和信息
   2. 可以被看作是与对象相关的宾语或形容词
   3. 如账号、人、文档、邮件、歌曲、图片以及它们的属性比如状态、日期等
3. 功能需求
   1. 系统对象必须进行的操作
   2. 最终会转化为界面控件
4. 其他需求：开发进度、大小等

## 4.5. 任务分析
1. 记录人们如何完成任务的一种方式
2. 作用
   1. 可以用来了解通过观察和访谈目前参与工作流程的人收集到的数据
   2. 主要用于调查现有情形，而不是展望新系统或设备
   3. 分析基本原理，了解人们想要达到什么目标，如何达到这些目标，并由此建立需求
3. 层次化任务分析（HTA）是应用最广的任务分析技术
   1. 把任务分解为若干子任务，再把子任务进一步分解为更细致的子任务。之后，把他们组织成一个“执行次序”，说明在实际情形下如何执行各项任务

### 4.5.1. 举例：图书馆目录服务
1. “借书”的子任务
   1. 访问图书馆目录
   2. 根据姓名、书名、主题等检索
   3. 记录图书位置
   4. 找到书架并取书（假定书在书架上）
   5. 到柜台办理借阅手续
2. 以上过程可以有所变化

### 4.5.2. 执行次序
1. 0.借书
   1. 1.前往图书馆
   2. 2.检索需要的图书
      1. 2.1 访问图书馆目录
      2. 2.2 使用检索屏
      3. 2.3 输入检索准则
      4. 2.4 找出需要的图书
      5. 2.5 记录图书位置
   3. 3.找到书架并取书
   4. 4.到柜台办理借阅手续
2. 执行次序0：执行1-3-4；若图书不在期望的书架上，则执行2-3-4。
3. 执行次序2：执行2.1-2.4-2.5；若未查到此书，则执行2.2-2.3-2.4-2.5编号说明了对应步骤编号。

### 4.5.3. 终止规则
1. 任务分析是一个迭代过程
2. 终止点
   1. 任务包含了复杂机械响应的地方
      1. 如鼠标移动
      2. 此时分解没有价值
   2. 涉及内部决断的地方
      1. 若决断和查找文档等外部动作相关，则分解
      2. 若为纯粹认知性，则终止

### 4.5.4. 方框-线条图示
1. HTA的图形描述（考试）
   1. 是自顶向下逐步求精的。
   2. 不可细分的叶子节点下画一条横线

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec7/2.png)

2. 评估是必考的

### 4.5.5. 用途
1. 手册和教学
   1. 如怎样拆卸、擦净来复枪，怎样安装软件等
   2. “如何做”手册适于培训
2. 需求获取和系统设计
   1. 任务分析本身不是需求获取
   2. 但有助于需求的完整表达
3. 详细的接口设计：应用于菜单设计

# 5. 需求验证
1. 原型的重要性
   1. 用户往往不能准确描述自己的需要
   2. 用户在看到或尝试某些事物后，就能立即知道自己不需要什么
2. 原型
   1. 在某一方面和真正产品比较接近、以便人们能对这一方面的各种技术方案进行不断评估和改进的一种接近于实际产品的模型：如房屋、桥梁的缩微模型
   2. 借助于原型，当事人就能与未来的产品交互，从中获得一些实际的使用体验，并发掘新思路

## 5.1. 原型分类
1. 低保真原型
   1. 与最终产品不太相似的原型
   2. 使用与最终产品不同的材料，如纸张、纸板：如PalmPilot掌上电脑的木雕原型
   3. 优点是简单、便宜、易于制作和修改
2. 高保真原型
   1. 与最终产品更为接近，使用相同的材料：如使用Visual Basic开发的软件系统原型
   2. 风险：
      1. 用户会认为原型就是系统
      2. 开发人员可能认为已找到了一个用户满意的设计
3. 建议使用低保真原型

## 5.2. 原型体现交互逻辑
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec7/3.png)

## 5.3. Tool support - Mockups

# 6. 小结
1. 用户是不同的
2. 产品是不同的
3. 人物角色的构建
4. 需求获取和分析：层次化任务分析
5. 原型

# 7. Design, prototyping and construction

## 7.1. Design and prototyping
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec7/4.png)

## 7.2. What is a prototype?
1. In other design fields a prototype is a small-scale model
   1. a miniature building town
   2. a miniature car

## 7.3. What is a prototype in Interaction Design?
1. from low-fidelity to high fidelity
2. a series of screen sketches
3. a storyboard, i.e. a cartoon-like series of scenes
4. a lump of wood (e.g. PalmPilot)
5. a cardboard mock-up
6. a Powerpoint slide show
7. a video simulating the use of a system
8. a piece of software with limited functionality written in the target language or in another language

## 7.4. Why prototype?
1. Evaluation and feedback are central to interaction design
2. Stakeholders can see, hold, interact with a prototype more easily than with a document
3. Team members can communicate effectively
4. You can test out ideas for yourself
5. It encourages reflection
6. Prototypes answer questions, and support designers in choosing between alternatives

## 7.5. What to prototype?
1. Technical issues
2. Work flow, task design
3. Screen layouts and information display
4. Difficult, controversial, critical areas

## 7.6. But before we start prototyping…
1. The most important thing to design is the user’s conceptual model. Everything else should be subordinated to making that model clear, obvious, and substantial. That is almost exactly the opposite of how most software is designed.(Liddle, 1996, p. 17)
2. A conceptual model is a high-level description of how a system is organized and operates. (Johnson and Henderson, 2002, p. 26)

## 7.7. Conceptual models and mental models
Ideally, users’ mental models should be compatible with the designer’s conceptual models

## 7.8. Conceptual models
1. Types of activities
   1. Giving instructions
   2. Manipulating and navigating
   3. Conversing
   4. Exploring and browsing
2. Metaphors and analogies

## 7.9. Instructing vs. manipulating
1. Still very common
2. Have to learn syntax
3. Frequent error messages
4. Lack of feedback
5. Efficient use of space
6. Efficient interaction for repetitive actions
7. Most common
8. No syntax to learn
9. Error messages rarely needed
10. Immediate feedback
11. Space gobblers
12. Some actions are awkward to perform

## 7.10. Conversing
1. Underlying model of having a conversation with another human
2. Range from simple voice recognition menu-driven systems to more complex ‘natural language’ dialogues
3. Examples include timetables, search engines, advice-giving systems, help systems

## 7.11. Exploring and browsing
1. Similar to how people browse information with existing media (e.g. newspapers, magazines, libraries, pamphlets)
2. Information is structured to allow flexibility in way user is able to search for information

## 7.12. What would be the most suitable conceptual model for
1. A car racing 3D video game?
2. An application for downloading music off the web?
3. An online system to support troubleshooting of computer hardware problems?
4. Programming?

## 7.13. Conceptual models based on objects
1. Usually based on an analogy with something in the physical world
2. Examples include books, tools, vehicles
3. Classic: Star Interface based on office objects

## 7.14. Benefits of metaphors
1. Makes learning new systems easier
2. Helps users understand the underlying conceptual model
3. Can be very innovative and enable the realm of computers and their applications to be made more accessible to a greater diversity of users

## 7.15. Types of prototypes
1. Different kinds of prototyping
   1. Low fidelity
   2. High fidelity
      1. Evolutionary
      2. ‘Throw-away
2. Compromises in prototyping
   1. Vertical
   2. Horizontal

### 7.15.1. Low-fidelity Prototyping
1. Uses a medium which is unlike the final medium, e.g. paper, cardboard
   1. Sketches of screens with post-it notes (task sequences)
      1. Card-based
   2. Storyboards
   3. ‘Wizard-of-Oz’
2. Quick, cheap, easily changed

## 7.16. Sketching
1. Sketching is important to low-fidelity prototyping
2. Don’t be inhibited about drawing ability (even I sketch regularly)

## 7.17. Card-based prototypes
1. Index cards (3 X 5 inches)
2. Each card represents one screen or part of screen
3. Often used in website development

## 7.18. Storyboards
1. Often used with scenarios, bringing more detail, and chance to role play
   1. It is a series of sketches showing how a user might progress through a task using the device
   2. Used early in design

## 7.19. ‘Wizard-of-Oz’ prototyping
1. Users thinks they are interacting with a computer, but a developer is responding to output rather than the system.
2. What could the shortcomings of this approach be?

## 7.20. High-fidelity prototyping
1. Uses materials that you would expect to be in the final product.
2. Prototype looks more like the final system than a lowfidelity version.
3. Common prototyping environments include Macromedia Director or Flash.
4. Danger that users think they have a full system

## 7.21. Summary
1. Prototyping enables designers to build designs iteratively and involve users
2. The most important thing to design is the users’ conceptual model1
3. Different kinds of prototyping are used for different purposes and at different stages
   1. Low fidelity at early stages for initial design solution attempts
   2. High fidelity later to refine design solution