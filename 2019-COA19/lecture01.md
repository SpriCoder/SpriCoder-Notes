**Computer is Everywhere.**
---

<!-- TOC -->

- [1. 什么是计算机？](#1-什么是计算机)
- [2. 结构和组织](#2-结构和组织)
- [3. 计算机发展历史](#3-计算机发展历史)
    - [3.1. 第一代计算机:真空管](#31-第一代计算机真空管)
        - [3.1.1. 冯·诺依曼模型(第一代计算机)](#311-冯·诺依曼模型第一代计算机)
        - [商用计算机](#商用计算机)
    - [3.2. 第二代计算机:晶体管](#32-第二代计算机晶体管)
    - [3.3. 第三代计算机:集成电路](#33-第三代计算机集成电路)
- [4. 摩尔定律](#4-摩尔定律)
- [5. Possible computer operations 可能的计算机操作](#5-possible-computer-operations-可能的计算机操作)
- [6. 计算机性能提升](#6-计算机性能提升)
- [7. 计算机表现](#7-计算机表现)
- [8. CPU速度](#8-cpu速度)
    - [8.1. 时钟速率](#81-时钟速率)
    - [8.2. 例子](#82-例子)
    - [8.3. CPI](#83-cpi)
    - [8.4. MIPS(Million Instruction Per Second)](#84-mipsmillion-instruction-per-second)
    - [8.5. MFLOPS(Million Floating Point Operations Per Second)](#85-mflopsmillion-floating-point-operations-per-second)
    - [8.6. Benchmarks(基准)](#86-benchmarks基准)

<!-- /TOC -->

# 1. 什么是计算机？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-2.png)
1. 数字化:现在很多数据未必用数字化的形式来存储下来，而在计算机中是的。

# 2. 结构和组织
1. 结构(对于程序员是可见的)
    + 一个提供乘法算法的计算机和另一个不提供乘法算法的计算机之间的区别
    + 包括:指令集、各类数据类型的大小
2. 组织(对于程序员是不可见的)
    + 一个用乘法器完成乘法的计算机和一个用加法器通过算法完成乘法的计算机之间的不同。
    + 包括:控制信号、存储技术

# 3. 计算机发展历史

## 3.1. 第一代计算机:真空管
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-3.png)

1. 第一台计算机是十进制的计算机。
2. 什么是程序?
    1. 将程序和数据以二进制的形式存储下来。

### 3.1.1. 冯·诺依曼模型(第一代计算机)
冯·诺依曼模型:最重要思想就是把数据和程序进行存储。
1. 存储器:地址和存储的内容。
    + 因为我们需要把数据和程序存储进去。
2. 处理单元:执行信息的实际处理。
    + 因为我们需要处理存入的数据和程序。
3. 控制单元:指挥信息的处理。
    + 因为我们需要控制一部分来控制整个处理过程。
4. 输入设备:将信息送入计算机中。
    + 我们需要输入数据和信息送入计算机。
5. 输出设备:将处理结果以某种形式显示在计算机外。
    + 因为我们需要将处理结果以某种形式显示在计算机外

### 商用计算机

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-4.png)

## 3.2. 第二代计算机:晶体管
第二代计算机特点:使用晶体管代替了真空管
1. 本身晶体管和真空管是兼容的。改变了计算机组织的改变，之后改变程序员的编程能力，然后推动了计算机结构的变化

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-5.png)

## 3.3. 第三代计算机:集成电路
特点:集成电路
1. 将在一个硅片上嵌入的晶体管更多。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-6.png)

# 4. 摩尔定律
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-7.png)

1. 每过18个月，在同样(单位面积)硅片上的晶体管的数量增加一倍。(69年以后，69年以前是12个月)
2. 摩尔定律意义:
    1. 计算机逻辑电路和存储器的成本显著下降。
    2. 在集成度更高的芯片中逻辑和存储器单元的位置更靠近，电子线路长度更短，提高了工作速度。
    3. 计算机的小型化带来了可能性和便捷性。
    4. 减少对于能源和降温的依赖和对冷却的要求。
    5. 避免芯片拼接，增强芯片稳定性。

# 5. Possible computer operations 可能的计算机操作
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-8.png)

1. 还有控制。

# 6. 计算机性能提升
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-9.png)

1. CPU速度:主要目标
2. Memory:容量速度
3. I/O:容量速度

# 7. 计算机表现
1. 第一、我们根据需求来选择计算机
    + 有很多事情都会影响计算机的选择。
2. 第二、计算机性能的要求。
    + 有的CPU需要快，有的GPU需要快。
    + 选计算机的时候并不是每一部分来算分，而是根据需要。
    + 从性能来看也有很多指标。
3. 第三、CPU和GPU等等
    + 在过去，更关心CPU的速度，而现在可能更关心GPU、内存等问题。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-10.png)

# 8. CPU速度
1. 如何比较CPU速度
2. 一般参考的属性:
    1. Hz数
    2. 核数

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-11.png)

## 8.1. 时钟速率
1. 在计算机处理中，是按照时钟来确定最小单位
    + 完成一个事情必须是时钟时间的整数倍。
2. 时钟时间越快，速度越高。
3. 3GHz:一秒钟3G次。
4. 时钟周期:是脉冲而不是时间。

## 8.2. 例子
1. 如果A比B的时钟速率高，那么A比B的速度快?
    + 没有规定完成一件事情是一个时钟周期来进行
    + 如果在时钟周期在切短后，一个周期内并不能完成等同数量的操作，那么可能会导致速度反而变慢

## 8.3. CPI

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-12.png)

1. 参数注解:f是周期个数，t是时钟周期时间。
2. CPI:平均每条指令所需要的时钟周期的数量。
3. CPI<sub>i</sub>就是每一个具体指令的。
4. 在一个计算机，如果知道CPI,还知道I<sub>c</sub>(指令个数),周期时间个数
5. 根据f可以得到t，而p是这个操作需要的数字。传输k次数据，每次需要m条指令。
6. 单条指令时间:CPI<sub>i</sub>*t。
7. 指令条数I<sub>c</sub>
8. 题目中是**指令周期时间**。

## 8.4. MIPS(Million Instruction Per Second)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-13.png)

1. 每秒能够处理的百万条指令数，越大越好。
2. 提升MIPS的指令:
    1. 有一些指令不常用，跑得又慢。一般处理器不进行处理。
    2. 而我在硬件上添加相应的处理的专用处理器，可以优化。
3. T是指一条指令实际执行所需要的时间，参考CPI

## 8.5. MFLOPS(Million Floating Point Operations Per Second)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-13.png)

1. 用来平衡不同指令差异时的MIPS值的不同。
    + 在电脑中浮点处理时常用的，所有类似标准程序。
2. 都需要按照浮点数进行优化。

## 8.6. Benchmarks(基准)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2019-COA19/img/cpt1/cpt1-15.png)

1. 这两个东西都是有道理的。
2. R<sub>i</sub>:是第i个测试程序的高级语言指令的执行速度。