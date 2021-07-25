Lec08-嵌入式系统建模
---

<!-- TOC -->

- [1. 建模、设计、分析](#1-建模设计分析)
  - [1.1. 什么是建模？](#11-什么是建模)
  - [1.2. 一个好的模型](#12-一个好的模型)
  - [1.3. 通用系统模型](#13-通用系统模型)
  - [1.4. 什么是基于模型的设计？](#14-什么是基于模型的设计)
  - [1.5. 建模技术](#15-建模技术)
  - [1.6. 计算分类法](#16-计算分类法)
  - [1.7. 建模，语言和工具](#17-建模语言和工具)
  - [1.8. 建模和语言](#18-建模和语言)
  - [1.9. 什么时候以及为什么要对嵌入式系统建模？](#19-什么时候以及为什么要对嵌入式系统建模)
  - [1.10. 软件建模](#110-软件建模)
    - [1.10.1. 建模语言的核心方面](#1101-建模语言的核心方面)
    - [1.10.2. 一种标准的嵌入式控制系统模式](#1102-一种标准的嵌入式控制系统模式)
    - [1.10.3. 建模语言的例子](#1103-建模语言的例子)
    - [1.10.4. C代码：文本，执行，实现语言](#1104-c代码文本执行实现语言)
    - [1.10.5. 各种图片](#1105-各种图片)
  - [1.11. 为什么要对嵌入式系统建模？](#111-为什么要对嵌入式系统建模)
  - [1.12. 什么时候应该对嵌入式系统建模？](#112-什么时候应该对嵌入式系统建模)
  - [1.13. 有限状态机](#113-有限状态机)
  - [1.14. 什么是模型？](#114-什么是模型)
  - [1.15. Application](#115-application)
- [2. FSM示例模型](#2-fsm示例模型)
  - [2.1. FSM在游戏中](#21-fsm在游戏中)
  - [2.2. 吃豆人](#22-吃豆人)
  - [2.3. 标准FSM命名法](#23-标准fsm命名法)
  - [2.4. 等价](#24-等价)
  - [2.5. 等效允许优化](#25-等效允许优化)
  - [2.6. 非确定性FSM](#26-非确定性fsm)
  - [2.7. NFA和FSM](#27-nfa和fsm)
- [3. Mealy-Moore FSM](#3-mealy-moore-fsm)
  - [3.1. 常规FSM作为模型](#31-常规fsm作为模型)
  - [3.2. 并发](#32-并发)
  - [3.3. 正交组件](#33-正交组件)
- [4. Harel的StateCharts：FSM的层次结构](#4-harel的statechartsfsm的层次结构)
  - [4.1. 分层FSM模型](#41-分层fsm模型)
  - [4.2. 层次状态划分](#42-层次状态划分)
  - [4.3. 定义](#43-定义)
  - [4.4. 默认状态机制](#44-默认状态机制)
  - [4.5. 历史机制](#45-历史机制)
  - [4.6. 结合历史和默认状态机制](#46-结合历史和默认状态机制)
- [5. 并发](#5-并发)
  - [5.1. 进入或离开AND-超级状态](#51-进入或离开and-超级状态)
  - [5.2. 计时器](#52-计时器)
  - [5.3. 应答机器计时器](#53-应答机器计时器)
  - [5.4. StateCharts中的常规边标签](#54-statecharts中的常规边标签)
  - [5.5. 条件转换](#55-条件转换)
  - [5.6. 评估状态图](#56-评估状态图)
    - [5.6.1. 优点：](#561-优点)
    - [5.6.2. 缺点](#562-缺点)
- [6. 示例：可乐机](#6-示例可乐机)
  - [6.1. v 1.0](#61-v-10)
  - [6.2. v1.1](#62-v11)
- [7. 分层FSM](#7-分层fsm)
  - [7.1. 定时炸弹的例子](#71-定时炸弹的例子)
  - [7.2. UML State Diagram Representing the Time-Bomb State Machine](#72-uml-state-diagram-representing-the-time-bomb-state-machine)
  - [7.3. 嵌套交换机FSM](#73-嵌套交换机fsm)
  - [7.4. 炸弹示例：声明](#74-炸弹示例声明)
  - [7.5. 后果](#75-后果)
- [8. 状态表FSM](#8-状态表fsm)
  - [8.1. 基于通用状态表的事件处理器的结构](#81-基于通用状态表的事件处理器的结构)
  - [8.2. 表事件处理器：数据结构](#82-表事件处理器数据结构)
  - [8.3. 表事件处理器：代码](#83-表事件处理器代码)
  - [8.4. 表事件处理器：用户代码I](#84-表事件处理器用户代码i)
  - [8.5. 表事件处理器：用户代码II](#85-表事件处理器用户代码ii)
  - [8.6. 表事件处理器：用户行为](#86-表事件处理器用户行为)
  - [8.7. 表事件处理器：问题](#87-表事件处理器问题)
- [9. 面向对象设计模式](#9-面向对象设计模式)
  - [9.1. 后果](#91-后果)
  - [9.2. 更好的表事件处理器：QEP(萨米克)](#92-更好的表事件处理器qep萨米克)

<!-- /TOC -->

# 1. 建模、设计、分析
1. 建模是通过模仿来加深对系统的理解的过程。 模型指定系统的功能。
2. 设计是构件的结构化创建。它指定系统如何执行操作。
3. 分析是通过解剖来加深对系统的了解的过程。它指定了系统为什么要执行其工作(或未能执行模型说明的应做的工作)。

## 1.1. 什么是建模？
1. 通过模仿获得对系统，流程或工件的见解。
2. 模型是模仿目标系统，流程或目标的工件。
3. 从最抽象的意义上讲，建模是一种方法，其中创建一些表示来描述和/或传达通过系统实现不容易，自然或充分捕获的系统方面
4. 数学模型是一组定义和数学公式形式的模型。

## 1.2. 一个好的模型
1. 简单
2. 适合理论发展
   1. 定理允许概括和捷径
   2. 不应太笼统(定理变得太弱)
3. 高表现力:紧凑的外观实现更高的生产率
4. 提供批判性推理能:
5. 可执行:模拟/验证
6. 可综合:通常需要设计正交性(例如编译器)
7. 不受任何具体实施的偏见:极难实现，但值得。
8. 适合手头的任务:如果模型不合适，则需要太多工作来使用它

## 1.3. 通用系统模型
1. 状态导向模式：有限状态机
2. 面向活动的模型：把系统描绘成一组与数据或者执行的相关性有关的活动的集合；
3. 面向结构的模型：框图、着重强调系统的物理构成
4. 面向数据的模型：实体-关系图
5. 异构模型
   1. 综合前四种模型特征
   2. 表达复杂系统的不同视图What is Model-Based Design?

## 1.4. 什么是基于模型的设计？
1. 创建嵌入式系统所有部分的数学模型
   1. 物理世界
   2. 控制系统
   3. 软件环境
   4. 硬件平台
   5. 网络
   6. 传感器和执行器
2. 根据模型构建实施
   1. 目标：像编译器一样自动执行此构造
   2. 实际上，只有部分是自动构建的

## 1.5. 建模技术
1. 模型是系统动力学的抽象(事物随时间变化的方式)
2. 例子：
   1. 建模物理现象：ODE
   2. 反馈控制系统：时域建模
   3. 模态行为建模：FSM，混合自动机
   4. 传感器和执行器建模：校准，噪声
   5. 建模软件：并发实时模型
   6. 网络建模：延迟，错误率，丢包

## 1.6. 计算分类法
1. "常规"与"事件驱动"
   1. 常规示例：流应用程序，处理器，…
   2. 事件驱动："反应性"(因环境变化而触发)
2. 即时的
   1. 硬期限与软期限
   2. 定期与非定期
3. 控制，数据，通讯：每个多少？
4. 平行度，地理距离：高度并发与顺序； 分布式系统
5. 确定性与非确定性：可预测程度

## 1.7. 建模，语言和工具
1. 计算模型是用于捕获系统行为的概念性概念，例如：
   1. 一组对象
   2. 组成规则
   3. 执行语义
2. 语言定义语法以捕获计算模型
3. 工具是"编译器"，可以将一种语言捕获的模型转换为另一种语言捕获的模型

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/1.png)

## 1.8. 建模和语言
1. 运算模型描述系统行为，概念，例如配方，顺序程序
2. 语言捕获模型，具体形式，例如英语，C
3. 多种语言可以捕获一种模型，例如，顺序程序模型C，C ++，Java
4. 一种语言可以捕获多种模型，例如，C ++→顺序程序模型，面向对象的模型，状态机模型
5. 某些语言更擅长捕获某些计算模型

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/2.png)

## 1.9. 什么时候以及为什么要对嵌入式系统建模？
1. 通过使用现代建模软件工具，您可以在离线仿真中设计并执行初始验证。
2. 然后，您可以使用模型来构成所有后续开发阶段的基础。
3. 通过在整个开发过程中执行验证和确认测试，将建模与硬件原型相结合将减少出错的风险并缩短开发周期。
4. 以系统模型为基础，可以更快，更可靠地进行设计评估和预测。
5. 这种迭代方法可以在性能和可靠性方面改进设计。
6. 由于设计团队，设计阶段和各种项目之间模型的可重用性以及对物理原型的依赖性降低，资源成本得以降低。
7. 通过使用自动代码生成技术，可以减少开发错误和开销。

## 1.10. 软件建模
> 对于工程和设计任务，尤其是与嵌入式系统有关的任务，通常使用某种形式的软件建模作为粗化或构建整个应用程序设计的初始方法。

1. 一些软件模型是行为模型；
2. 有些仅仅是用于理解和设计的视觉辅助工具，
3. 其他被更多地用作框架，以确保相似应用程序之间的一致性或促进工程师团队之间的通信。
4. 嵌入式系统设计人员面临的挑战是知道哪种类型和级别的建模最适合他们独特的情况和眼前的问题。

### 1.10.1. 建模语言的核心方面

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/3.png)

### 1.10.2. 一种标准的嵌入式控制系统模式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/4.png)

### 1.10.3. 建模语言的例子
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/5.png)

### 1.10.4. C代码：文本，执行，实现语言
```c
previous_error = setpoint - process_feedback integral = 0
start:
  wait(dt)
  error = setpoint - process_feedback integral = integral + (error*dt) derivative = (error - previous_error)/dt
  output = (Kp*error) + (Ki*integral) + (Kd*derivative) previous_error = error
goto start
```

### 1.10.5. 各种图片

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/6.png)  | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/7.png) |
| -------------------- | ------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/8.png)  | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/9.png) |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/10.png) |                     |

## 1.11. 为什么要对嵌入式系统建模？
1. 集成良好的建模方法可以大大减少系统文档，设计，测试，和实际实施。
2. 除了上面列出的主要优点外，对于某些嵌入式系统问题，建模方法还直接带来了额外的效率和准确性。

## 1.12. 什么时候应该对嵌入式系统建模？
1. 关键任务和安全关键型应用
2. 高度复杂的应用程序和系统
3. 大型开发团队
4. 如果无法选择原型，则别无选择。

## 1.13. 有限状态机
1. 根据维基百科，有限状态机是：
   - 用于设计计算机程序的行为模型。 它由与转换相关联的有限数量的状态组成。转换是一组从一个状态开始并在另一(或相同)状态结束的动作。转换是由触发器启动的，并且触发器可以是 事件或条件。
   - FSM ={ {输入符号}，{输出符号}，{状态}，{初始状态}，过渡关系(输入符号，当前状态到下一个状态的映射)、输出功能(输入符号，当前状态到当前输出符号的映射)}
2. 通常适用于控制器，协议
3. 强大的验证算法
4. 易于综合，但效率低下

## 1.14. 什么是模型？
1. 系统输入/输出序列建模
   1. 在给定时间出现的"状态"属性集，"输入"和"输出"是系统的可观察特征
   2. 允许或观察到的"过渡"状态成对排序，从输入/输出序列中推断出状态和转换
   3. 如果输出仅取决于状态Moore，则为Mealy FSM
2. 关键假设：可用于状态以及输入和输出符号字母的总内存是有限的。

## 1.15. Application
1. 自动售货机
2. 交通信号灯
3. 电子游戏
4. 文本解析
5. 正则表达式匹配
6. CPU控制器
7. 协议分析
8. 自然语言处理
9. 语音识别，执行，实现语言

# 2. FSM示例模型
1. 非正式规格：如果驾驶员打开钥匙并在5秒钟内没有系紧安全带，则发出警报5秒钟或直到驾驶员系紧安全带或关闭钥匙
2. 正式例子
   1. 输入= {KEY_ON，KEY_OFF，BELT_ON，BELT_OFF，5_SECONDS_UP，10_SECONDS_UP}
   2. 输出= {START_TIMER，ALARM_ON，ALARM_OFF}
   3. 状态= {关闭，等待，报警}
   4. 初始状态=关
   5. NextState：CurrentState，输入-> NextState
   6. 例如 NextState(WAIT，{KEY_OFF})= OFF
3. 输出：CurrentState，输入->输出，例如 Outs(OFF，{KEY_ON})= START_TIMER

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/11.png)

作业:类似安全带的例子，包含状态机和数学模型

## 2.1. FSM在游戏中
1. 可以将角色建模为一系列心理状态。
2. 世界事件可能会迫使状态发生变化。
3. 即使对于非程序员，这种心理模型也易于掌握。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/12.png)

## 2.2. 吃豆人
1. 吃豆人(Pac-Man)要求玩家在迷宫中导航，吃药并避免幽灵追赶他穿过迷宫
2. 有时，吃豆人可以通过吃强力药丸来在追赶者的桌子上转一转，这临时赋予了他吃鬼的能力
3. 发生这种情况时，鬼魂的行为发生了变化，他们没有追赶吃豆人，而是试图避开他
4. 吃豆人中的鬼有四种行为：
   1. 随意迷宫
   2. 追赶吃豆人，只要他在视线内
   3. 吃豆人消耗掉能量颗粒后，逃离吃豆人
   4. 回到中央基地进行再生

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/13.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/14.png) |
| -------------------- | -------------------- |

## 2.3. 标准FSM命名法
1. 按状态集的属性分类的有限自动机行为，以及转换关系(next_states，输出)=Φ(状态，事件)，它描述了事件后可能的下一个状态和输出
2. 有限自动机分类
   1. "确定性"表示Φ(S，E)为单值
   2. "完全指定"是指Φ(S，E)对于每个可能的输入都有一个值
   3. "摩尔"表示输出完全由当前状态决定-因此独立于当前事件
   4. " Mealy"表示输出取决于当前状态和当前事件
   5. "同步"表示状态仅按时钟间隔更改(对事件进行轮询)
   6. "异步"表示事件可以随时发生，而FSM事件更新

## 2.4. 等价
1. 两个在所有输入字符串上具有相同输出的FSM被认为是等效的
2. 等效不需要同构(相同形状)：即两个等效的机器不必具有相同的图形甚至是相同数量的状态！

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/15.png)

## 2.5. 等效允许优化
1. 在软件中，FSM的简单程序实现的复杂度与FSM中的转换数量成正比
2. 通常有助于最小化状态数，因此有助于最小化FSM的转换数
3. 如果机器是确定性的并且完全指定，则可以在时间O(s2t)中完成此过程，其中s是状态数，t是FSM的状态转换数
4. 如果不确定性或指定不完全，问题将是NP-hard题。

## 2.6. 非确定性FSM
1. 当下一状态或输出函数具有多个值时，FSM称为不确定性
   1. 下一个状态是一种关系，但是输出满足：紧凑型(逻辑电路)
   2. 输出不满足：形式上的不确定性(人类语义模型通常需要)
2. 非确定性允许建模：
   1. 未指明的行为：规格不完整
   2. 未知行为：例如环境模型
   3. 紧凑型：可以完全"确定性"，只是较小的模型

## 2.7. NFA和FSM
1. 通常的FSM和NDA是等效的(Rabin-Scott构造，Rabin '59)
2. 在实践中，NFA通常更为紧凑(用于确定的指数爆炸)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/16.png)

- 就是将非确定性的转换为确定性的，两者是等价的

# 3. Mealy-Moore FSM
1. 状态模型是单线程的：任何时候都只有一个状态有效
2. 摩尔状态模型：所有动作均在进入状态时进行
   1. 无反应(响应延迟一个周期)
   2. 易于撰写(始终清晰定义)
   3. 适用于实施(即良好的电路模拟)
3. 状态模型：所有动作都处于过渡状态
   1. 在软件中，导致更紧凑的代码
   2. 硬件时序和可组合性困难

## 3.1. 常规FSM作为模型
1. 经常过度指定实施：完全指定了排序(即使不在乎)
2. 由于缺乏组成比喻的可扩展性差：状态数量可能难以控制
3. 不支持并发：通常希望推理一个本地子属性复合机，但是如何关联子状态的行为？
4. 简单的解决方案：介绍要建模的层次结构：听起来并不简单

## 3.2. 并发
1. 示例：
   1. 设备可以处于{关闭，启动，运行，错误}状态
   2. 从{待机，电池}运行时
2. 如何安排这些状态？桩体爆炸

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/21.png)

## 3.3. 正交组件
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/20.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/22.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/23.png)

# 4. Harel的StateCharts：FSM的层次结构
1. StateCharts支持：
   1. 将状态重复分解为AND / OR子状态
   2. 嵌套状态，并发，正交组件
   3. 动作(可能有参数)
   4. 活动(状态为活动时执行的功能)
   5. 卫兵
   6. 历史
   7. 同步(瞬时广播)通信机制

## 4.1. 分层FSM模型
1. 问题：如何缩小表示的大小？
2. Harel关于StateCharts(语言)和有限并发性(模型)的经典论文：3个正交指数约简
3. 层次结构：
   1. 声明"包围" FSM
   2. 处于活动状态意味着活动中的FSM
   3. a的状态称为OR状态
   4. 用于建模抢占和异常
4. 并发：
   1. 两个或多个FSM同时处于活动状态
   2. 状态称为AND状态
5. 非确定性：用于抽象行为

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/24.png)

## 4.2. 层次状态划分
1. FSM将完全处于S的子状态之一
2. 从子状态到子状态的转换
3. 初始(默认)
4. 历史

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/25.png)

## 4.3. 定义
1. FSM的当前状态也称为**活动状态**。
2. 不由其他状态组成的状态称为**基本状态**。
3. 包含其他状态的状态称为**超级状态**。
4. 对于每个基本状态s，包含s的超状态称为**祖先状态**。
5. 如果每当S处于活动状态时，恰好S的子状态之一处于活动状态，则超级状态S称为OR超级状态。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/26.png)

## 4.4. 默认状态机制
1. 默认状态是为S定义默认开始状态的伪状态
2. 不是状态本身

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/27.png)

## 4.5. 历史机制
1. 给定输入m，S返回到离开S之前的状态(可以是A，B，C，D或E)。
2. 首次输入S时，将应用默认机制。
3. 历史记录和默认机制可以分层使用。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/28.png)

## 4.6. 结合历史和默认状态机制
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/29.png)

# 5. 并发
1. AND超级状态
   1. FSM处于超级状态的所有(立即)子状态
   2. 与Or-Supers不同，它正式需要多个控制点

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/30.png)

## 5.1. 进入或离开AND-超级状态
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/31.png)

## 5.2. 计时器
1. 由于需要在嵌入式系统中对时间进行建模，因此需要对计时器进行建模。
2. 在StateCharts中，特殊边缘可用于超时。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/32.png)

## 5.3. 应答机器计时器
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/33.png)

## 5.4. StateCharts中的常规边标签
1. 在StateChart中标记过渡的表达式的一般语法为n [c] / a，其中
   1. n是触发过渡的事件
   2. c是过渡发生的条件
   3. a是在以及何时过渡被采用时执行的操作
2. 对于每个过渡标签，事件，条件和操作是可选的
   1. 事件可以是值的改变
   2. 允许将标准比较作为条件，将赋值语句作为动作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/34.png)

## 5.5. 条件转换
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/35.png)

## 5.6. 评估状态图

### 5.6.1. 优点：
1. 层次结构允许任意嵌套AND-和ORsuper状态。
2. (StateMate)另一个优点是，StateMate的语义在足够详细的级别上定义
3. 可用的大量商业仿真工具(StateMate，StateFlow，BetterState等)
4. 可用的"后端"将StateCharts转换为C或VHDL，从而实现软件或硬件实现。

### 5.6.2. 缺点
1. 生成的C程序效率低下
2. 生成的硬件可能更糟
3. 难以应用于分布式应用程序
4. 没有结构层次的描述

# 6. 示例：可乐机

## 6.1. v 1.0
1. 假设您有一台可乐机：
   1. 开机后，机器等待付款
   2. 存入四分之一时，机器等待1/4
   3. 存入第二个季度时，机器等待选择
   4. 用户按下"可乐"时，将分配可乐
   5. 使用者拿瓶时，机器会再次等待
   6. 当用户按下" SPRITE"或" DIET"时可乐，"是雪碧或减肥可乐
   7. 使用者拿瓶时，机器会再次等待

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/36.png)

## 6.2. v1.1
1. 瓶子可能卡在机器中
   1. 当瓶子卡住时，自动指示器会通知系统
   2. 发生这种情况时，在清除瓶子之前，机器将不接受任何金钱或发出任何瓶子
   3. 清除瓶子后，机器将再次等待付款
2. 状态机更改
   1. 需要多少个新状态？
   2. 多少个新过渡？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/37.png)

# 7. 分层FSM
1. 层次结构允许
   1. 明智的默认活动
   2. 多个地方增强行为：考虑卡住的恢复行为–吞噬您的钱…
   3. 大大减少所需的状态数
   4. 易于添加扩展状态语义
   5. 增强状态和保护措施
2. 我们如何在软件中进行有效的演绎？HFSM比FSM更复杂且成本更高，但是要权衡表达与复杂性和维护性之间的关系

## 7.1. 定时炸弹的例子
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/38.png)

## 7.2. UML State Diagram Representing the Time-Bomb State Machine
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/39.png)

## 7.3. 嵌套交换机FSM
1. "状态"是静态类型的枚举
2. "事件"是一种类型化的信号(也是一个枚举)
3. " init"设置计时器并初始化变量
4. 在每个事件上调用"调度"以将控制权传递给FSM

## 7.4. 炸弹示例：声明
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/40.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/41.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/42.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/43.png)

## 7.5. 后果
1. 很简单。
2. 它需要枚举信号和状态。
3. 它具有较小的内存占用量，因为只需要一个小的标量状态变量即可表示状态机的当前状态。
4. 它不会促进代码重用，因为状态机的所有元素都必须专门针对眼前的问题进行编码。
5. 整个状态机被编码为一个整体功能，很容易变得太大。
6. 事件调度时间不是恒定的，而是取决于两个级别的switch语句的性能，它们随着案例数的增加而降低(通常为O(log n)，其中n为情况数)。
7. 实现不是分层的。您可以在每个转换中直接直接手动编写进入/退出操作的代码，但是鉴于状态机拓扑的变化，这很容易出错并且难以维护。这主要是因为与一种状态(例如，进入动作)有关的代码将在许多地方(在导致该状态的每个转变上)分布和重复。对于代码合成工具来说，后者属性不是问题，这些代码合成工具通常使用嵌套的switch语句类型的实现。

# 8. 状态表FSM
1. 通用表驱动事件处理器
2. 应用程序提供：动作功能，表，事件
3. 状态表是二维的：对于每个事件，说明表具有的状态(动作，下一状态)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/44.png)

## 8.1. 基于通用状态表的事件处理器的结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/45.png)

## 8.2. 表事件处理器：数据结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/46.png)

## 8.3. 表事件处理器：代码
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/47.png)

## 8.4. 表事件处理器：用户代码I
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/48.png)

## 8.5. 表事件处理器：用户代码II
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/49.png)

## 8.6. 表事件处理器：用户行为
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/50.png)

## 8.7. 表事件处理器：问题
1. FSM的常规结构
   1. 枚举用作索引
   2. 需要"填充物"状态和功能：一些状态，事件对为空
2. 分派是固定时间
3. 状态表是ROM候选者，但稀疏
4. 更改可能需要重建整个表
5. 每个动作都需要自己的功能
6. 不支持状态层次结构

# 9. 面向对象设计模式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec8/51.png)

## 9.1. 后果
1. 它在很大程度上依赖于多态性，并且需要像C ++这样的面向对象的语言。
2. 使状态转换高效(重新分配一个指针)。
3. 通过后期绑定为事件调度提供了非常好的性能机制(O(const)，不考虑动作执行)。
4. 它允许您自定义每个事件处理程序的签名。事件参数是显式的，语言的类型系统会在编译时验证所有参数的适当类型(例如，onTICK()接受uint8_t类型的参数)。
5. 实现是内存高效的。
6. 它不需要枚举状态，枚举事件。
7. 通过具体状态子类的方法(通过上下文指针)强制间接访问上下文的参数。
8. 添加状态需要对抽象状态类进行子类化。
9. 处理新事件需要将事件处理程序添加到抽象状态类接口。
10. 与状态表方法一样，事件处理程序通常具有良好的粒度。
11. 模式不是分层的。

## 9.2. 更好的表事件处理器：QEP(萨米克)
1. 想法：保留表的可扩展概念，但消除2-d查找
   1. 使用Switch语句区分每个状态的事件
   2. 使用指向状态处理程序功能的指针表来区分状态
2. 好处：
   1. 表分派比嵌套开关快，但是开关只需要分派已处理的事件
   2. 可以轻松添加新状态，也可以轻松添加新事件
   3. 只需要更改直接影响到实施的部分…