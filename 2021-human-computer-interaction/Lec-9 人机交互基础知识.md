Lec-9 人机交互基本知识

# 1. 信息处理模型
1. 作用
   1. 研究人对外界信息的接收、存储、集成、检索和使用，可预测人执行特定任务的效率，如可推算人需要多长时间来感知和响应某个刺激（又称“反应时间”），信息过载会出现怎样的瓶颈现象等
   2. 信息处理机，Lindsay和Norman
      1. 没有考虑到注意和记忆的重要性

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/1.png)

## 1.1. 扩展的信息处理机模型
1. Barber对其进行了扩展
   1. 注意和记忆功能与信息处理过程的各个阶段存在交互

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/2.png)

## 1.2. 人类处理机模型
1. 最著名的信息处理模型
2. Card等，1983
3. 包含三个交互式组件
   1. 感知处理器：信息将被输出到声音存储和视觉存储区域
   1. 认知处理器：输入将被输出到工作记忆
   2. 动作处理器：执行动作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/3.png)

## 1.3. 存在的问题
1. 把认知过程描述为一系列处理步骤
2. 仅关注单个人和单个任务的执行过程:忽视了复杂操作执行中人与人之间及任务与任务之间的互动
3. 忽视了环境和其他人可能带来的影响
  
导致出现了：外部认知模型、分布式认知模型

# 2. 认知心理学
1. 兴起于20世纪50年代中期
2. 关注人的高级心理过程，如记忆、思维、语言、感知和问题解决能力等：神经元网络已经成为新一代人工智能领域最热门的研究课题之一
3. 对HCI的贡献
   1. 有助于理解人与计算机的交互过程，同时也可对用户行为进行预测
   2. 人对于外界的感知有80%来自于视觉获取的信息

## 2.1. 格式塔（Gestalt）心理学
1. 研究人是如何感知一个良好组织的模式的，而不是将其视为一系列相互独立的部分
   1. 事物的整体区别于部分的组合
2. “Gestalt”
   1. 德语，“完形（configuration）”或“型式（pattern）”
   2. 格式塔心理学又称完形心理学
3. 表明
   1. 用户在感知事物的时候总是尽可能将其视为一个“好”的型式
   2. 相近性原则、相似性原则、连续性原则、完整性和闭合性原则

### 2.1.1. 相近性原则
1. 空间上比较靠近的物体容易被视为整体
   1. 设计界面时，应按照相关性对组件进行分组
2. 如下图，你看到了什么？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/4.png)

### 2.1.2. 相似性原则
1. 人们习惯将看上去相似的物体看成一个整体
2. 功能相近的组件应该使用相同或相近的表现形式
3. 这一次呢？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/5.png)

### 2.1.3. 格式塔心理学与界面感知
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/6.png)

### 2.1.4. 连续性原则
1. 共线或具有相同方向的物体会被组合在一起：将组件对齐，更有助于增强用户的主观感知效果

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/7.png)

### 2.1.5. 对称性原则
1. 相互对称且能够组合为有意义单元的物体会被组合在一起
2. 相近性？对称性？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/8.png)

### 2.1.6. 完整和闭合性原则
1. 人们倾向于忽视轮廓的间隙而将其视作一个完整的整体：页面上的空白可帮助实现分组

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/9.png)

### 2.1.7. 前景&背景
1. 前景和背景在某些情况下可以互换：“整体区别于局部”

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/10.png)

### 2.1.8. 屏幕格式塔
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/11.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/12.png)

### 2.1.9. 文字格式塔
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/13.png)

### 2.1.10. 标题格式塔
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/14.png)

### 2.1.11. 段落格式塔
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/15.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/16.png)

### 2.1.12. 线的长度/文本宽度
1. 回溯Retracing：段落太宽，不容易找到下一行的开始
2. 扫视Saccades
   1. 只有注视能看到内容
   2. 每隔15~30个字符（依赖于文字难度、阅读技能等）就要停下来注视
3. 不成文规定
   1. line length at most 12.5 cm (5 inches)
   2. lines at most 65 characters (average, excluding spaces)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/17.png)

### 2.1.13. 约定
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/18.png)

### 2.1.14. 格式塔心理学反例
1. 对比Constract
2. 让重点更突出！

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/19.png)

### 2.1.15. 几种不同形式的对比
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/20.png)

# 3. 人脑中的记忆结构
1. 三个阶段，Atkinson和Shiffrin
   1. 感觉记忆
   2. 短时记忆
   3. 长时记忆
   4. 三个阶段之间可以进行信息交换

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/21.png)

## 3.1. 关于记忆
1. 感觉记忆
   1. 又称瞬时记忆
   2. 在人脑中持续约为1秒钟
   3. 帮助我们把相继出现的一组图片组合成一个连续的图像序列，产生动态的影像信息
2. 短时记忆
   1. 感觉记忆经编码后形成
   2. 又称工作记忆，约保持30秒
   3. 储存的是当前正在使用的信息，是信息加工系统的核心，可理解为计算机的内存
   4. 短时记忆的存储能力约为7±2个信息单元

## 3.2. 7±2理论vs. 交互式系统设计
1. 影响
   1. 菜单中最多只能有7个选项
   2. 工具栏上只能显示7个图标
   3. ……
2. 事实
   1. 浏览菜单和工具栏基于人的识别功能：人们识别事物的能力要远胜于回忆事物的能力
   2. 界面设计时要尽可能减小对用户的记忆需求，同时可考虑通过将信息放置于一定的上下文中，来减少信息单元的数目

## 3.3. 长时记忆
1. 短时记忆->长时记忆
   1. 短时记忆中的信息经进一步加工后会变为长时记忆
   2. 只有与长时记忆区的信息具有某种联系的新信息才能够进入长时记忆
2. 长时记忆的信息容量几乎是无限的
3. 启发
   1. 注意使用线索来引导用户完成特定任务
   2. 在追求独特的创新设计时也应注重结合优秀的交互范型
4. 遗忘
   1. 长时记忆中的信息有时是无法提取
   2. 不代表长时记忆区的信息丢失了
5. 易出错
   1. “人为错误”被定义为“人未发挥自身所具备的功能而产生的失误，它可能降低交互系统的功能”
   2. 从表面上看是由于用户的误解、误操作或一时大意
   3. 大部分交互问题都源于系统设计本身

## 3.4. 视错觉
1. 知觉感受的扭曲
   1. 前后景互换实际上就是视错觉的一种
   2. 白色三角的例子
2. 视错觉是不可避免的
3. 启示：对于物体的视觉感知与物体所处的上下文密切相关

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/22.png)

## 3.5. 视觉感知&上下文

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/23.png)

1. 提示：它的头在左侧，能产奶，上下文信息有助于增强人们的视觉感知
2. 期望对感知的影响：红桃和黑桃
3. 字母顺序重要吗？

# 4. 交互范型（Form）

## 4.1. 命令行交互
1. 用户通过在屏幕某个位置上键入特定命令的方式来执行任务：“基于字符的界面（Characterbased Interface）
2. 优点
   1. 专家用户能够快速完成任务；
   2. 较GUI节约系统资源；
   3. 可动态配置可操作选项；
   4. 键盘操作较鼠标操作更加精确；
   5. 支持用户自定义命令
3. 缺点
   1. 命令语言的掌握对用户的记忆能力提出较高要求；
   2. 基于回忆的方式（recall memory）：没有GUI基于识别的方式（recognition memory）容易使用
   3. 键盘操作，出错频率较高；
   4. 要求用户记忆指令的表示方式：与可用性理论所强调的“不应要求用户了解计算机底层的实现细节”相违背。

## 4.2. 菜单驱动界面
1. 以一组层次化菜单的方式提供用户可用的功能选项，一个或多个选项的选择可以改变界面的状态
2. 通过鼠标、数字键、字母键或者方向键进行选择

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/24.png)

1. 优点
   1. 基于识别机制，对记忆的需求较低；
   2. 具有自解释性；
   3. 容易纠错；
   4. 适合新手用户。若提供了较好的快捷键功能，则对于专家用户同样适用。
2. 缺点
   1. 导航方式不够灵活；
   2. 当菜单规模较大时，导航效率不高；
   3. 占用屏幕空间，不适合小型显示设备：为节省空间，通常组织为下拉菜单或弹出式菜单；
   4. 对专家用户而言使用效率不高
3. （1）现代的菜单形式（2）网页上的菜单（3）手机上的菜单

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/25.png)

## 4.3. 基于表格的界面
1. 显示给用户的是一个表格，里面有一些需要用户填写的空格
2. 优点
   1. 简化数据输入；
   2. 只需识别无需学习；
   3. 特别适合于日常文书处理等需要键入大量数据的工作
3. 缺点
   1. 占用大量屏幕空间；
   2. 导致业务流程较形式

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/26.png)

## 4.4. 直接操纵
1. Ben Shneiderman，1982
   1. 用户通过在可视化对象上面进行某些操作来达到执行任务的目的
   2. 展现了真实世界的一种扩展
   3. 对象和操作一直可见
   4. 迅速且伴有直观的显示结果的增量操作
   5. 增量操作可以方便地逆转

### 4.4.1. 直接操纵的三个阶段
1. 自由阶段——指用户执行操作前的屏幕视图；
2. 捕获阶段——在用户动作（点击、点击拖拽等）执行过程中屏幕的显示情况；
3. 终止阶段——用户动作执行后屏幕的显示情况。

### 4.4.2. 优点
1. 将任务概念可视化，用户可以非常方便地辨别他们；
2. 容易学习，适合新手用户；
3. 基于识别，对记忆的要求不高，可减少错误发生；
4. 支持空间线索，鼓励用户对界面进行探索；
5. 可实现对用户操作的快速反馈，具有较高的用户主观满意度。

### 4.4.3. 缺点
1. 实现起来比较困难；
2. 对专家用户而言效率不高；
3. 不适合小屏幕显示设备；
4. 对图形显示性能的需求较高

### 4.4.4. 直接性演化
1. 更少的记忆、更多的识别、更少的键盘和点击、更不易出错、以及更可视的上下文

## 4.5. 问答界面Wizard
1. 通过询问用户一系列问题实现人与计算机的交互
   1. Web问卷是典型的采用问答方式进行组织的应用
   2. 应允许用户方便地取消其中一个界面的选项
2. 优点
   1. 对记忆的要求较低；
   2. 每个界面具有自解释性；
   3. 将任务流程以简单的线性表示；
   4. 适合新手用户。
3. 缺点
   1. 要求从用户端获得有效输入；
   2. 要求用户熟悉界面控制；
   3. 纠错过程可能比较乏味。

## 4.6. 隐喻（Metaphor）界面
1. 本质：在用户已有知识的基础上建立一组新的知识，实现界面视觉提示和系统功能之间的知觉联系，进而帮助用户从新手用户转变为专家用户
2. 优点：直观生动、无需学习
3. 局限性
   1. 不具有可扩展性
   2. 不同用户对同一事物可能产生不同的联想
   3. 紧紧地将我们的理念和物理世界束缚在一起
   4. 寻找恰当的隐喻可能存在困难

### 4.6.1. 桌面隐喻（桌面演变史）
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/27.png)

## 4.7. 自然语言交互
1. 自然语言的模糊性
   1. The boy hit the dog with the stick.
   2. 她说她不知道
2. 受限于理解技术，当前只能够使用受限的语言与计算机进行交流，Q：还是自然语言吗？

## 4.8. 其他交互形式
1. 虚拟现实交互
2. 增强现实/混合现实
3. 触觉交互
4. 手势/体感交互
5. 笔式交互
6. 脑机交互

# 5. 交互框架

## 5.1. 作用
1. 提供理解或定义某种事物的一种结构
2. 能够帮助人们结构化设计过程
3. 认识设计过程中的主要问题
4. 还有助于定义问题所涉及的领域

## 5.2. 执行/评估活动周期EEC
1. 最有影响力的框架
2. 定义了活动的四个组成部分
   1. 目标(Goal) ≠意图(Intention)
   2. 执行(Execution)
   3. 客观因素(World)
   4. 评估(Evaluation)

## 5.3. EEC模型
1. 从用户视角探讨人机界面问题
2. 共有七个阶段
   1. 1-4：执行阶段
   2. 5-7：评估阶段
3. 每个循环代表一个动作
4. 夜晚看书的例子

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/28.png)

## 5.4. 执行隔阂& 评估隔阂
1. EEC模型可解释为什么有些界面的使用存在问题
   1. 执行隔阂
      1. 用户为达目标而制定的动作与系统允许的动作之间的差别
      2. “保存文件” 举例
   2. 评估隔阂
      1. 系统状态的实际表现与用户预期之间的差别
2. 意义
   1. 如何才能够使用户简单地确定哪些活动是被允许的
   2. 如何确定系统是否处于期望的运行状态等问题

## 5.5. 扩展EEC模型
1. EEC模型不能描述人与系统通过界面进行的通信
2. 四个构成部分+四个步骤(翻译过程
   1. 系统：内核语言
   2. 用户：任务语言
   3. 输入：输入语言
   4. 输出：输出语言
   5. 执行阶段
   6. 定义，执行，表现
   7. 设计人员应保证从输入到系统的翻译是容易的
3. 评估阶段：观察

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2021-human-computer-interaction/img/lec9/29.png)
