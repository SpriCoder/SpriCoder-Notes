lec03-Enbedded Software System
---

<!-- TOC -->

- [1. 嵌入式系统硬件](#1-嵌入式系统硬件)
  - [1.1. 硬件平台架构](#11-硬件平台架构)
  - [1.2. 流行的微处理器(单片机)](#12-流行的微处理器单片机)
  - [1.3. 冯诺依曼结构计算机](#13-冯诺依曼结构计算机)
  - [1.4. Harvard](#14-harvard)
  - [1.5. RISC vs. CISC](#15-risc-vs-cisc)
  - [1.6. RISC-V](#16-risc-v)
  - [1.7. 设计系统芯片之前需要考虑的五件事](#17-设计系统芯片之前需要考虑的五件事)
  - [1.8. 编程模型](#18-编程模型)
  - [1.9. 嵌入式微处理器的分类](#19-嵌入式微处理器的分类)
  - [1.10. 嵌入式微处理单元(MPU)](#110-嵌入式微处理单元mpu)
  - [1.11. 嵌入式微控制器(MCU，Microcontroller Unit)](#111-嵌入式微控制器mcumicrocontroller-unit)
  - [1.12. 时间和温度系统的硬件架构图](#112-时间和温度系统的硬件架构图)
  - [1.13. `NXP i.MX RT`系列跨界处理器](#113-nxp-imx-rt系列跨界处理器)
  - [1.14. 嵌入式DSP](#114-嵌入式dsp)
  - [1.15. 嵌入式SoC](#115-嵌入式soc)
  - [1.16. FPGA](#116-fpga)
  - [1.17. DSP与FPGA](#117-dsp与fpga)
  - [1.18. TI嵌入式处理产品组合](#118-ti嵌入式处理产品组合)
- [2. 嵌入式系统产品](#2-嵌入式系统产品)
- [3. 嵌入式微处理器的特点](#3-嵌入式微处理器的特点)
- [4. 选择微控制器的标准](#4-选择微控制器的标准)
- [5. ARM Ltd](#5-arm-ltd)
  - [5.1. 与ARM合作伙伴联系](#51-与arm合作伙伴联系)
  - [5.2. ARM处理器的分类](#52-arm处理器的分类)
  - [5.3. ARM架构](#53-arm架构)
  - [5.4. 管道组织](#54-管道组织)
  - [5.5. Meltdown & Spectre](#55-meltdown--spectre)
  - [5.6. 字节序](#56-字节序)
- [6. 选择微控制器的10个步骤](#6-选择微控制器的10个步骤)

<!-- /TOC -->

# 1. 嵌入式系统硬件
1. 嵌入式系统硬件经常在循环中使用("循环中的硬件")：网络物理系统

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/1.png)

## 1.1. 硬件平台架构
1. 包含很多部分：CPU、bus、memory、I/O devices: 网络，传感器，执行器等。
2. 每个部分有多大/多快？

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/2.png)

## 1.2. 流行的微处理器(单片机)
1. ARM:做嵌入式设备很久，市场占有率比较高。
2. MIPS(学院派):美国计算机协会(ACM)宣布 John L. Hennessy 和 David A. Patterson 荣获 2017 年年图灵奖。
3. PowerPC
4. X86

## 1.3. 冯诺依曼结构计算机
1. 存储器保存数据，指令。
2. 中央处理器(CPU)从内存中获取指令。
3. 分开的CPU和内存区分可编程计算机。
4. CPU寄存器可提供帮助：程序计数器(PC)，指令寄存器(IR)，通用寄存器等。
5. 嵌入式中两个版本的CPU都有

## 1.4. Harvard
1. Harvard 不能使用自我修改的代码。
2. Harvard 允许同时进行两次内存提取。
3. 大多数DSP(数据信号处理，Digital Signal Process)使用 Harvard 架构来传输数据：
   1. 更大的内存带宽
   2. 更可预测的带宽

## 1.5. RISC vs. CISC
1. Complex instruction set computer (CISC): 复杂指令集计算机：许多寻址模式、多种操作
2. Reduced instruction set computer (RISC): 精简指令集计算机：加载/存储、可传递指令

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/3.png)

## 1.6. RISC-V
1. 简单、完全开源并且免费
2. 将基准指令和扩展指令分开，可以通过扩展指令做定制化的模块和扩展:RISC-V的基准指令确定后将不不会再有变化，这是RISC-V稳定性的重要保障。
3. 32、64、128位指令集

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/4.png)

## 1.7. 设计系统芯片之前需要考虑的五件事
成本、生态系统、碎片化风险、安全性、设计保证

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/6.png)

## 1.8. 编程模型
1. 编程模型：对程序员可见的寄存器。
2. 一些寄存器不可见(IR)

## 1.9. 嵌入式微处理器的分类
1. 嵌入式微处理器种类繁多，按位数可分为4位、8位、16位、32位和64位。
2. 根据功能不同，嵌入式微处理器分为四种：
   1. 嵌入式微处理单元(MPU)
   2. 嵌入式微控制器(MCU)
   3. 嵌入式DSP处理器
   4. 嵌入式SoC

## 1.10. 嵌入式微处理单元(MPU)
1. 嵌入式微处理器就是和通用计算机的处理器对应的CPU。
   1. 功能和微处理器基本一样,是具有32位以上的处理器,具有较高的性能.
   2. 具有体积小,功耗少,成本低,可靠性高的特点.
   3. 有的可提供工业级应用
2. 流行的嵌入式微处理器:
   1. ARM(ARM公司): Cortex-A8/A9/A15/A75/A76
   2. Power
   3. MIPS(MIPS公司)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/7.png)

## 1.11. 嵌入式微控制器(MCU，Microcontroller Unit)
1. 嵌入式微控制器就是将整个计算机系统的主要硬件集成到一块芯片中,芯片内部集成ROM/EPROM, RAM, 总线, 总线逻辑, 定时/计数器, Watchdog, I/O, 串行口等各种必要功能和外设.
2. 特点：
   1. 一个系列的微控制器具有多种衍生产品;
   2. 单片化,体积大大减小,功耗和成本降低,可靠性提高;
   3. 是目前嵌入式工业的主流,约占嵌入式系统50%的份额;
   4. 多是8位和16位处理器，32位的也不多
3. 流行的嵌入式微控制器
   1. 通用系列:8051,Coldfire的MC683xx(32位)，Cortex-M0/3/4/7/M33/M35P
   2. 半通用系列:支持I2C,CAN BUS及众多专用MCU和兼容系列

## 1.12. 时间和温度系统的硬件架构图

| 基于MPU             | 基于MCU             |
| ------------------- | ------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/8.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/9.png) |

> 左侧部分是芯片，**存储也会被集成到芯片中**

## 1.13. `NXP i.MX RT`系列跨界处理器
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/10.png)

## 1.14. 嵌入式DSP
1. 嵌入式DSP是专门用于信号处理方面的处理器，其在系统结构和指令算法方面进行了特殊设计，具有很高的编译效率和指令执行速度。
2. 应用领域：
   1. 数字滤波
   2. 频谱分析
   3. FFT
3. 流行的嵌入式DSP
   1. 德州仪器器(TI)，c6000 与 c5000
   2. 模拟器件公司(ADI)
   3. 摩托罗拉(Motorola) 公司

## 1.15. 嵌入式SoC
1. 嵌入式SoC是追求产品系统最大包容的集成器器件。绝大多数系统构件都在一个系统芯片内部。
2. 特点：结构简洁、体积小、功耗小、可靠性高、设计生产效率高
3. 流行的SoC：高通骁龙(Snapdragon)、海思

## 1.16. FPGA
1. 现场可编程门阵列列
2. 赛灵思、阿尔特拉(被英特尔收购)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/11.png)

## 1.17. DSP与FPGA
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/12.png)


## 1.18. TI嵌入式处理产品组合
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/13.png)

> 公司的产品线

# 2. 嵌入式系统产品
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/14.png)

> M是最底层的

# 3. 嵌入式微处理器的特点
1. 基础是通用微处理器
2. 与通用微处理器相比的区别：
   1. 体积小、重量轻、可靠性高
   2. 功耗低
   3. 成本低：片上存储、引脚与封装、代码密度
   4. 工作温度、抗电磁干扰、可靠性等方面增强

# 4. 选择微控制器的标准
> 如何选择一个适合的微服务控制器?
> 嵌入式系统都是实时系统，需要考虑效率

1. 有效且经济地满足任务的计算需求
   1. 速度，ROM和RAM的数量，I / O端口和计时器的数量，大小，包装，功耗
   2. 容易升级
   3. 单位成本
2. 软件开发工具的可用性：汇编器，调试器，C编译器，仿真器，模拟器，技术支持(开源框架可能没有多少人维护)
3. 微控制器的广泛可用性和可靠来源。

# 5. ARM Ltd
1. 成立于1990年11月：从Acorn Computers剥离出来
2. 设计ARM系列的RISC处理器内核
3. 将ARM核心设计许可给制造并销售给客户的半导体合作伙伴：ARM本身并不制造硅
4. 还开发有助于ARM体系结构设计的技术
5. 软件工具、板、调试硬件、应用软件、总线架构、外围设备等

> 源自英国，售卖知识产权盈利

## 5.1. 与ARM合作伙伴联系
1. ARM有非常大规模的生态链

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/15.png)

## 5.2. ARM处理器的分类
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/16.png)

## 5.3. ARM架构
1. 典型的RISC架构：
   1. 大型统一寄存器文件
   2. 加载/存储架构
   3. 简单的寻址模式
   4. 统一和固定长度的指令字段
2. 增强功能：
   1. 每条指令控制ALU和移位器
   2. 自动递增和自动递减寻址模式
   3. 多次加载/存储
   4. 有条件的执行
3. 结果：高性能、低码量、低功耗、低硅面积

## 5.4. 管道组织
1. 提高速度：大多数指令在单个周期内执行
2. 版本：
   1. 3级(ARM7TDMI及更早版本)
   2. 5级(ARMS，ARM9TDMI)
   3. 6级(ARM10TDMI)
3. 管道刷新并在分支上重新填充，导致执行速度变慢
   1. 分支指令if，会导致预取指令失败，然后清空流水线，再取，分支指令可能会带来性能下降
   2. 有一个部分的分支嵌套过多，对嵌入式设备非常严重
4. 指令集中的特殊功能消除了代码中的小跳动，从而获得了流水线中的最佳流程

## 5.5. Meltdown & Spectre
1. 近20年年的Intel、AMD、Qualcomm厂家和其它ARM的处理器受到影响；
2. 因为此次CPU漏洞的特殊性，包括Linux、Windows、OSX等在内的操作系统平台参与了修复；
3. Firefox、Chrome、Edge等浏览器也发布了相关的安全公告和缓解方案；

## 5.6. 字节序
1. 位与字节/字顺序之间的关系定义了字节序：

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/17.png)

# 6. 选择微控制器的10个步骤
1. Step 1: 列出所需的硬件接口(保证物理上，设备可以连接到未处理器上)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec3/18.png)

2. Step 2: 检查软件架构
3. Step 3: 选择架构
4. Step 4: 确定内存需求
5. Step 5: 开始寻找微控制器
6. Step 6: 检查成本和功率约束
7. Step 7: 检查零件可用性
8. Step 8: 选择开发套件
9. Step 9: 研究编译器和工具
10. Step 10: 开始实验

> 1. 做原型可以先忽略一些东西，SBC板机，需要考虑够不够用的问题。
> 2. 计算下移到AIoT的位置