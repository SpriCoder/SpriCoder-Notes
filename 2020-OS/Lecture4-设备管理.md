Lecture4-设备管理
---
1. 外部设备分类
   1. 存储型设备：如磁带机、磁盘机等，以存储大量信息和快速检索为目标，在系统中存储持久性信息，作为内存的扩充，又叫外存。
   2. I/O型设备：如打印机等，把外界信息输入计算机，把计算结果从计算机中输出，完成计算机之间的通信或人机交互。
2. 设备管理
   1. 使用I/O中断、缓冲区管理、通道、设备驱动调度等多种技术，极大程度上克服了设备和CPU速度不匹配所引起的问题，使得主机和设备能够并行工作，提高设备的利用率。
   2. 将所有设备抽象为文件，统一在文件系统下，赋予文件属性，优点是尽可能统一文件和设备的I/O 处理; 尽可能把设备文件和普通文件纳人同一保护机制下。为了方便用户或高层软件使用，设备管理还对各种设备进行抽象，配置**设备驱动程序**，屏蔽物理细节和操作过程，提供统一使用界面
3. 设备管理的功能：设备中断处理、缓冲区管理、设备分配和去配、设备驱动调度、实现虚拟设备。

<!-- TOC -->

- [1. 设备管理概述](#1-设备管理概述)
  - [1.1. I/O系统、设备与操作](#11-io系统设备与操作)
  - [1.2. I/O设备的分类](#12-io设备的分类)
    - [1.2.1. 按信息传输方向(I/O操作特性)划分](#121-按信息传输方向io操作特性划分)
    - [1.2.2. 按交互功能划分](#122-按交互功能划分)
    - [1.2.3. 按设备管理(I/O信息交换单位)划分](#123-按设备管理io信息交换单位划分)
  - [1.3. 设备管理的目标](#13-设备管理的目标)
  - [1.4. 设备管理的功能](#14-设备管理的功能)
  - [1.5. 设备管理的层次](#15-设备管理的层次)
- [2. I/O控制方式](#2-io控制方式)
  - [2.1. 轮询方式(程序直接控制方式)](#21-轮询方式程序直接控制方式)
    - [2.1.1. 流程](#211-流程)
    - [2.1.2. 涉及指令](#212-涉及指令)
    - [2.1.3. 特点和评价](#213-特点和评价)
  - [2.2. 中断方式](#22-中断方式)
    - [2.2.1. 流程](#221-流程)
    - [2.2.2. 特点和评价](#222-特点和评价)
  - [2.3. 直接存储器访问(DMA)方式](#23-直接存储器访问dma方式)
    - [2.3.1. DMA模块](#231-dma模块)
    - [2.3.2. 流程](#232-流程)
    - [2.3.3. DMA方式中的周期窃取](#233-dma方式中的周期窃取)
    - [2.3.4. 特点和评价](#234-特点和评价)
  - [2.4. 小结：I/O控制方式的演化](#24-小结io控制方式的演化)
  - [2.5. I/O通道(第四种，更高级)](#25-io通道第四种更高级)
    - [2.5.1. I/O通道描述](#251-io通道描述)
    - [2.5.2. I/O通道的工作流程](#252-io通道的工作流程)
  - [2.6. 设备控制器(偏向硬件部分)](#26-设备控制器偏向硬件部分)
    - [2.6.1. 设备控制器的主要功能](#261-设备控制器的主要功能)
    - [2.6.2. 设备控制器的组成部分(例)](#262-设备控制器的组成部分例)
  - [2.7. I/O发展对总线的影响](#27-io发展对总线的影响)
    - [2.7.1. 单总线](#271-单总线)
    - [2.7.2. 传统的三级总线(例)](#272-传统的三级总线例)
    - [2.7.3. 采用南北桥的多级总线(例)](#273-采用南北桥的多级总线例)
    - [2.7.4. 采用I/O通道的多级总线(例)](#274-采用io通道的多级总线例)
- [3. I/O软件的实现](#3-io软件的实现)
  - [3.1. I/O软件](#31-io软件)
    - [3.1.1. I/O软件的总体设计目标](#311-io软件的总体设计目标)
    - [3.1.2. I/O软件设计思路](#312-io软件设计思路)
    - [3.1.3. I/O软件主要考虑的问题](#313-io软件主要考虑的问题)
  - [3.2. I/O软件的层次结构](#32-io软件的层次结构)
  - [3.3. I/O中断处理程序](#33-io中断处理程序)
  - [3.4. I/O设备驱动程序](#34-io设备驱动程序)
    - [3.4.1. I/O设备驱动程序的任务](#341-io设备驱动程序的任务)
    - [3.4.2. 设备驱动程序的功能](#342-设备驱动程序的功能)
    - [3.4.3. 设备驱动程序的处理方式](#343-设备驱动程序的处理方式)
    - [3.4.4. 设备驱动程序的层次](#344-设备驱动程序的层次)
  - [3.5. 独立于设备的I/O软件](#35-独立于设备的io软件)
    - [3.5.1. 设备命名](#351-设备命名)
    - [3.5.2. 设备保护](#352-设备保护)
    - [3.5.3. 提供与设备无关的数据单位](#353-提供与设备无关的数据单位)
    - [3.5.4. 缓冲技术](#354-缓冲技术)
    - [3.5.5. 设备分配和状态跟踪](#355-设备分配和状态跟踪)
    - [3.5.6. 错误处理和报告](#356-错误处理和报告)
  - [3.6. 用户空间的I/O软件](#36-用户空间的io软件)
    - [3.6.1. 库函数](#361-库函数)
    - [3.6.2. SPOOLing软件](#362-spooling软件)
  - [3.7. I/O操作应执行的步骤，以读操作为例](#37-io操作应执行的步骤以读操作为例)
- [4. 缓冲技术](#4-缓冲技术)
  - [4.1. 设置I/O缓冲的目的](#41-设置io缓冲的目的)
  - [4.2. 实现缓冲技术的基本思想](#42-实现缓冲技术的基本思想)
  - [4.3. 单缓冲](#43-单缓冲)
    - [4.3.1. 工作机制](#431-工作机制)
    - [4.3.2. 性能计算](#432-性能计算)
  - [4.4. 双缓冲](#44-双缓冲)
    - [4.4.1. 工作机制](#441-工作机制)
    - [4.4.2. 性能分析](#442-性能分析)
  - [4.5. 多缓冲](#45-多缓冲)
- [5. 驱动调度技术](#5-驱动调度技术)
  - [5.1. 磁盘的物理结构](#51-磁盘的物理结构)
    - [5.1.1. 磁盘的组成](#511-磁盘的组成)
    - [5.1.2. 物理块(扇面)在磁盘上的三维地址(磁头号，柱面号，扇区号)](#512-物理块扇面在磁盘上的三维地址磁头号柱面号扇区号)
  - [5.2. 磁盘读写数据](#52-磁盘读写数据)
  - [5.3. 磁盘存取时间](#53-磁盘存取时间)
- [6. 磁盘的驱动调度](#6-磁盘的驱动调度)
  - [6.1. 磁盘调度策略](#61-磁盘调度策略)
  - [6.2. 旋转调度](#62-旋转调度)
    - [6.2.1. 旋转排序](#621-旋转排序)
    - [6.2.2. 优化分布](#622-优化分布)
  - [6.3. 移臂调度](#63-移臂调度)
    - [6.3.1. 先来先服务算法 FCFS](#631-先来先服务算法-fcfs)
    - [6.3.2. 最短查找时间优先(最小短距离法) SSTF，Shortest Service Time First](#632-最短查找时间优先最小短距离法-sstfshortest-service-time-first)
    - [6.3.3. 扫描算法 SCAN算法](#633-扫描算法-scan算法)
    - [6.3.4. 分布扫描算法 N-step-SCAN](#634-分布扫描算法-n-step-scan)
    - [6.3.5. 电梯调度(LOOK 算法)](#635-电梯调度look-算法)
    - [6.3.6. 循环扫描(C-SCAN)](#636-循环扫描c-scan)
    - [6.3.7. 补充：后进先出(LIFO，Last-in,first-out)](#637-补充后进先出lifolast-infirst-out)
    - [6.3.8. 补充：单向扫描](#638-补充单向扫描)
  - [6.4. 提高磁盘I/O速度的办法](#64-提高磁盘io速度的办法)
  - [6.5. 磁盘循环冗余阵列](#65-磁盘循环冗余阵列)
    - [6.5.1. RAID 0(无冗余)](#651-raid-0无冗余)
    - [6.5.2. RAID 1(镜像)](#652-raid-1镜像)
    - [6.5.3. RAID 2(通过海明码冗余)](#653-raid-2通过海明码冗余)
    - [6.5.4. RAID 3(交错位奇偶校验)](#654-raid-3交错位奇偶校验)
    - [6.5.5. RAID 4(块奇偶校验)](#655-raid-4块奇偶校验)
    - [6.5.6. RAID 5(块分布奇偶校验)](#656-raid-5块分布奇偶校验)
    - [6.5.7. RAID 6(双重冗余)](#657-raid-6双重冗余)
  - [6.6. 磁盘Cache](#66-磁盘cache)
    - [6.6.1. 替换策略:LRU](#661-替换策略lru)
    - [6.6.2. 替换策略:LFU(Least Frequently Used)](#662-替换策略lfuleast-frequently-used)
- [7. 设备分配](#7-设备分配)
  - [7.1. 设备独立性](#71-设备独立性)
  - [7.2. 设备分配方式](#72-设备分配方式)
    - [7.2.1. 设备的物理特性](#721-设备的物理特性)
    - [7.2.2. 分配方式](#722-分配方式)
    - [7.2.3. 联系PV操作](#723-联系pv操作)
  - [7.3. 设备分配的数据结构](#73-设备分配的数据结构)
    - [7.3.1. 设备类表](#731-设备类表)
    - [7.3.2. 设备表](#732-设备表)
    - [7.3.3. 通道结构系统](#733-通道结构系统)
  - [7.4. 虚拟设备](#74-虚拟设备)
    - [7.4.1. SPOOLing设备](#741-spooling设备)
    - [7.4.2. SPOOLing设备组成](#742-spooling设备组成)
    - [7.4.3. 输入井的作业状态](#743-输入井的作业状态)
    - [7.4.4. SPOOLing步骤](#744-spooling步骤)
    - [7.4.5. 打印机SPOOLing](#745-打印机spooling)
    - [7.4.6. 网络通信SPOOLing守护进程](#746-网络通信spooling守护进程)

<!-- /TOC -->

# 1. 设备管理概述

## 1.1. I/O系统、设备与操作
1. I/O系统是I/O设备及其接口线路、控制部件、通道和管理软件的统称。
2. I/O设备又称为外围设备或外部设备，简称外设
   1. 用于计算机系统与外部世界(如用户、其他计算机或设备)的信息交换或存储
   2. 把外界信息输入计算机，把计算结果从计算机中输出，完成计算机之间的通信或人机交互。
3. I/O操作：内存和设备介质之间的信息传送操作
   1. 影响计算机的通用性和可扩充性
   2. 计算机系统综合处理能力及性价比的重要因素

## 1.2. I/O设备的分类
  
### 1.2.1. 按信息传输方向(I/O操作特性)划分
1. **输入设备**：将外界信息输入计算机，例如：键盘，鼠标，扫描仪等
2. **输出设备**：将计算结果输出，例如：显示器，打印机等
3. **输入输出设备**：既可以输入信息，也可以输出信息，例如：磁盘驱动器，网卡等

### 1.2.2. 按交互功能划分
1. **人机交互设备**：用于用户与计算机之间的交互通信，例如：鼠标，键盘，显示器等
2. **存储设备**：持久性地存储大量信息并快速检索，例如：磁盘驱动器，光盘驱动器等
3. **机机通信设备**：用于计算机和计算机之间的通信，例如：网卡，调制解调器等

### 1.2.3. 按设备管理(I/O信息交换单位)划分
1. **字符设备**
   1. 以**字符**为单位进行信息交换，发送或接收一个字符流。
   2. 严格依赖新消息的物理位置进行定位和读写。
   3. 输入输出设备、人机交互设备大多是字符设备，例如鼠标、显示器等。
2. **块设备**
   1. 以固定大小的数据块(块是存储介质上连续信息组成的一个区域)进行信息交换。
   2. 存取任何一个物理块所需的时间几乎不依赖于此信息所处的位置。
   3. 存储设备通常为块设备，例如磁盘驱动器等。
3. **网络设备**：用于与远程设备通信的设备
   1. 机机通信设备为**网络设备**，例如网卡等
   2. 网络设备可以抽象为传送字符流的特殊**字符设备**，也可以抽象为传送连续小块数据的**块设备**

## 1.3. 设备管理的目标
1. 目标一：解决设备和CPU速度的不匹配，使主机和设备并行工作，提高设备使用效率

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/1.png)

2. 目标二：对设备进行抽象，屏蔽设备的**物理细节和操作过程**，配置驱动程序，提供统一界面，供用户或高层软件使用
   1. 抽象为**裸设备**：不被操作系统直接管理，由应用程序读写，I/O效率更高
   2. 抽象为**设备文件**：文件系统中的节点，统一管理
3. 文件系统：按名存储、提高文件的标准化操作，设备管理转换为文件管理。

## 1.4. 设备管理的功能
1. 设备中断处理：中断最初来源于设备
2. **缓冲区**管理
3. 设备的分配和去配：合适给进程**分配进程以及回收**
4. 设备驱动调度
5. 实现虚拟设备

## 1.5. 设备管理的层次
1. I/O硬件
   1. I/O设备及其接口线路
   2. 控制部件
   3. 通道
2. I/O软件
   1. 系统I/O软件
   2. 用户空间I/O软件

# 2. I/O控制方式

## 2.1. 轮询方式(程序直接控制方式)

### 2.1.1. 流程
1. 处理器向控制器发送一个I/O命令
2. 如果设备未就绪，则**重复测试过程**，直至设备就绪
3. 执行数据交换：CPU从I/O接口(数据寄存器)读取一个字，然后用存储指令保存到内存。
4. 等待I/O操作完成后，才可以继续其它操作

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/3.png)

### 2.1.2. 涉及指令
1. 查询指令：查询是否就绪
2. 读写指令：就绪执行数据交换
3. 转移指令：未就绪转向查询

### 2.1.3. 特点和评价
1. 处理I/O请求会**终止**原程序的执行，浪费时间，并且CPU需要等待I/O设备就绪
2. CPU需要参与数据传送
3. 总而言之，CPU和设备只能**串行**工作，效率低下

## 2.2. 中断方式

### 2.2.1. 流程
1. 处理器向控制器发出一个I/O命令，然后**继续执行后续指令**
   1. 如果该进程不需要等待I/O完成，后续指令可以仍是该进程中的指令。
   2. 否则，该进程在这个中断上挂起，处理器执行其他工作
2. 控制器检查设备状态，按照I/O命令要求完成相应I/O操作，就绪后发起中断
3. CPU响应中断，转向中断处理程序
4. 中断处理程序，执行数据读写操作
5. 退出中断处理程序，返回发生中断前的执行状态。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/4.png)

### 2.2.2. 特点和评价
1. 响应中断后会终止原程序的执行
2. CPU不需要等待I/O设备就绪
3. CPU需要参与数据传送，但是缓冲区满就要发起中断，会消耗较多CPU时间，如果有过多的设备可能会导致CPU来不及响应或数据丢失的想象。
4. 总而言之，CPU和设备部分并行操作，效率有所提高

## 2.3. 直接存储器访问(DMA)方式

### 2.3.1. DMA模块
1. DMA模块：模仿处理器来控制主存和设备控制器之间的数据交换
2. DMA方式中，内存和设备之间有一条数据通路成块地传送数据，无需CPU参与。
3. DMA模块完成如上描述的数据传输任务。
4. 组成结构
   1. 内存地址寄存器:存放内存中需要交换数据的地址，DMA传送之前由程序送入首地址；DMA传送过程中，每次交换数据都把地址寄存器的内容加1
   2. 字计数器:记录传送数据的总字数，每次传送一个字就把字计数器减1。
   3. 数据缓冲寄存器或数据缓冲区:暂存每次传送的数据。
   4. 设备地址寄存器:存放I/O信息的地址，如磁盘的柱面号、磁头号、扇区号。
   5. 中断机制和控制逻辑: 用于向CPU提出I/O中断请求及保存CPU发来的I/O命令，管理DMA的传送过程。DMA与内存之间采用字传送，DMA与设备之间可能是字位或字节传送，所以DMA中要设置数据移位寄存器、字节计数器等硬件逻辑。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/5.png)

5. 为什么控制器从设备读取数据后不立即送进内存，而是使用内部缓冲区？一旦磁盘开始读数据，其读出速度是恒定的，无论控制器怎样就要接收数据，如果控制器立即送进内存，则需要系统总线的控制权，但是可能会等待，因此需要内部缓冲区，使得DMA操作启动前不需要总线。

### 2.3.2. 流程
1. 处理器向DMA模块发出I/O命令
2. 处理器继续执行其它工作，DMA模块负责传送全部数据
3. 数据传送结束后，DMA中断处理器

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/6.png)

### 2.3.3. DMA方式中的周期窃取
1. 当DMA和CPU同时经总线访问内存时，CPU**总是**将总线的占有权让给DMA一个或几个主存周期，一般是1个存取周期，让设备和内存之间交换数据。
2. 周期窃取对延迟CPU与主存的数据交换影响不大
   1. 数据传送过程是不连续的和不规则的
   2. CPU大部分情况下与Cache进行数据交换，直接访问内存较少

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/7.png)

### 2.3.4. 特点和评价
1. CPU不会终止原程序的执行，不需要发生中断，提高CPU资源利用率。
2. CPU只在数据传送的开始和结束时参与。
   1. 开始时，CPU需要对DMA模块进行初始化。
   2. 结束时，CPU响应中断，但不必保存现场。
3. 优点：线路简单、价格低廉，适用于小型和微型计算机的快速设备。
4. 缺点：DMA窃取时钟周期，功能不够强不能满足复杂的I/O操作要求。

## 2.4. 小结：I/O控制方式的演化
1. 采用轮询方式的设备控制器:CPU需要等待设备就绪，且参与数据传送
2. 采用中断方式的设备控制器:CPU无需等待设备就绪，但响应中断后参与数据传送:通过DMA直接控制存储器
3. CPU在数据传送开始和结束时:参与，与主存进行数据交换时不参与

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/8.png)

## 2.5. I/O通道(第四种，更高级)

### 2.5.1. I/O通道描述
1. I/O通道又称为通道控制器、I/O处理器，用于完成逻辑上独立的I/O任务，适用于中大型计算机系统。
2. 设备控制器包含自身专用的**处理器和通道程序**，自成体系，使得**CPU与通道高度并行**，实现通道和CPU并行操作，通道之间并行操作，设备之间并行操作。
   1. I/O指令不再由处理器执行，而是存在主存中，由I/O通道所包含的**处理器**执行
   2. 采用主存，通道，控制器，设备的四级连接，实施三级控制，可控制多台同类或不同类的设备
      1. 一个CPU通常连接多个通道，通过I/O指令控制
      2. 一个通道可以连接若干控制器，通过执行通道命令控制
      3. 一个控制器可以连接若干设备，通过动作序列控制
3. DMA和I/O通道不同点：DMA中，每一个I/O指令只能读写一个数据块，而通道可以一次面向不通过的多个数据块。

### 2.5.2. I/O通道的工作流程
1. CPU在执行主程序时遇到I/O任务，启动指定通道(通过通道程序地址字CAW)上选址的设备。
2. 启动成功，通道开始控制设备进行操作，此时CPU继续执行其他任务，直到I/O操作完成。
3. 通道发出I/O操作结束中断，处理器相应并停止当前工作，转向处理I/O操作结束事件。

## 2.6. 设备控制器(偏向硬件部分)
1. 为达到模块化和通用性的设计目标，通常将I/O设备中的**机械部件和电子部件**分开处理
   1. 机械部件是指设备本身。
   2. 电子部件称为**设备控制器或适配器**
2. 设备控制器又称为设备适配器、I/O控制器、I/O控制接口，简称I/O模块或I/O接口
3. 操作系统与**控制器**交互，而非与设备交互
   1. 多数微型和小型计算机系统通过单总线模式来交互
   2. 大中型计算机采用多总线结构和多通道方式来交互。
4. 设备控制器具体控制设备进行I/O，将串行的位流装配成字节，存入控制器内部的缓冲区形成字节块，在校验和确认无错后，这块数据将被复制进入内存。

### 2.6.1. 设备控制器的主要功能
> 设备控制器是CPU与设备之间的接口

1. **接收和识别**CPU或通道发来的命令，例如磁盘控制器可以接受读写等操作
2. **实现数据交换**：包括设备和控制器之间的数据传输，且通过数据总线或通道，控制器和内存之间传输数据。
3. **发现和记录**设备及自身的状态信息，供CPU处理使用
4. **识别设备地址**，当连接多台设备时

### 2.6.2. 设备控制器的组成部分(例)
1. 状态/控制寄存器
2. 数据缓冲寄存器
3. 地址译码器和I/O控制逻辑
4. 外设接口控制逻辑

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/2.png)

> 左侧是主机侧，右侧是设备侧

## 2.7. I/O发展对总线的影响

### 2.7.1. 单总线
1. 将CPU、主存和I/O模块连接到同一组总线上

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/9.png)

1. 优点：**结构简单，易于扩充**
2. 缺点：
   1. 主存需要和I/O模块**共用总线**
   2. 设备增多会造成总线变长，进而增加传输时延
   3. **无法适用于大量高速设备**

### 2.7.2. 传统的三级总线(例)
1. 主存和Cache通过**主存总线**传送数据，CPU和Cache之间存在局部总线
2. 主存总线和扩展总线上的I/O设备之间传送数据通过**扩展总线接口**缓冲

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/10.png)

3. 优点：主存与I/O之间的数据传送与处理器的活动分离；可以支持更多的I/O设备
4. 缺点：不适用于I/O设备数据速率相差太大的情形

### 2.7.3. 采用南北桥的多级总线(例)
1. 通过存储总线、PCI总线、E(ISA)总线分别连接主存、高速I/O设备和低速I/O设备，距离CPU比较近的北桥控制器

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/11.png)

2. 优点：可以支持不同数据速率的I/O设备

### 2.7.4. 采用I/O通道的多级总线(例)
1. 支持CPU、主存和多个I/O通道之间的数据传送
2. 支持I/O通道和I/O控制器，以及I/O控制器和设备之间的数据传送

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/12.png)

# 3. I/O软件的实现

## 3.1. I/O软件

### 3.1.1. I/O软件的总体设计目标
1. **高效率**：改善设备效率，尤其是磁盘I/O操作的效率，有很大的影响
2. **通用性**：用统一的标准来管理所有设备

### 3.1.2. I/O软件设计思路
把软件组织成层次结构，低层软件用来屏蔽**硬件细节**，高层软件向用户提供简洁、友善的界面

### 3.1.3. I/O软件主要考虑的问题
1. **设备无关性**：编写访问文件的程序与物理设备无关
2. **出错处理**：低层软件能处理的错误不让高层软件感知
3. **同步/异步传输**：支持**阻塞和中断驱动**两种工作方式
   1. 同步：如果要同步就需要做等待，增加延迟
   2. 异步：可以不等待，提供并行度(不等是有前提的，运行进程的后续操作不可以依赖I/O操作的结果)
4. **缓冲技术**：建立数据缓冲区，匹配数据的到达率与离去率，提高吞吐率

## 3.2. I/O软件的层次结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/13.png)

> 为了解决I/O软件主要考虑的问题，我们将其划分为如上四个层次结构

## 3.3. I/O中断处理程序
1. I/O中断处理程序位于操作系统底层，与硬件设备密切相关，与系统其余部分尽可能少地发生联系
2. 进程请求I/O操作时，通常被挂起，直到数据传输结束后并产生I/O中断时，操作系统接管CPU后转向中断处理程序
3. 当设备向CPU提出中断请求时，CPU响应请求并转入中断处理程序
4. I/O中断处理程序的功能
   1. 检查设备状态寄存器内容，判断**产生中断的原因**，根据I/O操作的完成情况进行相应的处理
   2. 如果数据传输有错，向**上层软件**报告设备的**出错信息**，实施**重新执行**
   3. 如果正常结束，唤醒等待传输的进程，使其转换为**就绪态**
   4. 如果有等待传输的I/O命令，通知相关软件启动下一个I/O请求

## 3.4. I/O设备驱动程序
1. I/O设备驱动程序包括与设备密切相关的所有代码
2. I/O设备的功能是从独立于设备的软件中接收并执行I/O请求
3. 某些控制器一次只能接受一条命令(DMA)，有些控制器可以接受一串命令后执行(通道)

### 3.4.1. I/O设备驱动程序的任务
1. 把用户提交的**逻辑I/O请求**转化为**物理I/O操作**的启动和执行，如设备名转换为端口等
2. 监督设备是否正确执行，管理**数据缓冲区**，进行必要的纠错处理

### 3.4.2. 设备驱动程序的功能
1. **设备初始化**:在系统**初次启动或设备传输数据**时，预置设备和控制器以及通道状态
2. **执行设备驱动例程**
   1. 负责启动设备，进行数据传输
   2. 对于具有通道方式，还负责生成**通道指令和通道程序**，启动通道工作
3. **调用和执行中断处理程序**:负责处理设备和控制器及通道所发出的各种中断

### 3.4.3. 设备驱动程序的处理方式
1. **阻塞自己**：命令开始执行时，进程阻塞自己，直到昨晚才解除阻塞。
2. **无须阻塞**：很快就可以完成，比如滚屏。
3. 无论哪种，操作完成后都需要记性数据传输正确性校验，如果有错则报告。

### 3.4.4. 设备驱动程序的层次
1. 每个设备驱动程序只处理一种设备，或者一类紧密相关的设备
2. 设备驱动程序分为**整体驱动程序和分层驱动程序**
   1. **整体驱动程序**直接向操作系统提供接口和控制硬件:适用于功能简单的驱动程序，效率较高，但较难迁移
   2. **分层驱动程序**将驱动程序分成多层，放在栈中，系统接到I/O请求时先调用栈顶的驱动程序，栈顶的驱动程序可以直接处理请求或向下调用更低层的驱动程序，直至请求被处理:适用于功能复杂、重用性要求较高的驱动程序，结构清晰且便于移植，但会增加一部分系统开销

## 3.5. 独立于设备的I/O软件
1. 基本功能：执行适用于所有设备的常用I/O功能，并向**用户层软件**提供一致性接口

### 3.5.1. 设备命名
通过路径名寻址设备

### 3.5.2. 设备保护
1. 检查用户是否有权访问所申请设备
2. 多数大中型计算机系统中，用户进程对I/O设备的直接访问是绝对禁止的，I/O指令被定义为特权指令，使用系统调用方式访问。
3. 设备文件依赖于inode实现，文件目录并不能区分文件名是代表磁盘文件还是设备文件，但是inode号是不同的。
   1. 磁盘inode包含指向数据块的指针。
   2. 设备文件inode包含指向内核设备驱动程序的指针。

### 3.5.3. 提供与设备无关的数据单位
1. 操作系统会为磁盘分配记录空闲块的表或位示图。
2. 不同磁盘的扇区大小可能不同，独立于设备的I/O设备软件屏蔽这个事实，向高层软件提供统一的数据尺寸：通过将若干扇区合并成逻辑块——簇，簇大小相同。
3. 使得字符设备可以对一个字符操作，也可以对更大单位的数据操作。

### 3.5.4. 缓冲技术
1. 通过缓冲消除填满速率和清空速率的影响
   1. 网络上数据需要分析检查才知道去哪里。
   2. 有些设备有严格时间约束，比如数字音频设备。
2. 块设备和字符设备都需要缓冲技术
   1. 块设备：磁盘读写以块为单位，应用程序以任意大小单元处理设备，如果应用程序读写长度和位置不是完整扇区，则需要使用缓冲区来缓冲。
   2. 字符设备：字符设备提供数据速度快于或慢于应用程序消耗数据的速度。
3. 缓冲设计大量复制操作，对I/O性能有较大开销。

### 3.5.5. 设备分配和状态跟踪
1. 根据设备物理特性，操作系统制订分配策略
2. 策略
   1. 静态分配
   2. 动态分配
   3. 虚拟分配

### 3.5.6. 错误处理和报告
1. 错误应该在尽可能接近硬件的地方处理，想办法纠正和解决。
2. 未能解决，交给驱动程序处理，比如是磁盘块受损无法读写。
3. 驱动程序无法处理的错误，交给独立于设备的I/O软件报错。

## 3.6. 用户空间的I/O软件

### 3.6.1. 库函数
1. 一小部分I/O软件**不在**操作系统中，是与**应用程序链接在一起的库函数**，甚至完全由运行于**用户态**的程序组成
2. **系统调用通常由库函数封装后供用户使用**，封装函数只是将系统调用所用的参数放在合适位置，然后执行**访管指令**来陷入内核，再由内核函数实现真正的I/O操作

### 3.6.2. SPOOLing软件
在**内核外运行**的**系统**I/O软件，采用**预输入、缓输出和井管理**技术，是多道程序设计系统中处理**独占型设备**的一种方法，通过创建守护进程和特殊目录解决**独占型设备**的**空占**问题

## 3.7. I/O操作应执行的步骤，以读操作为例
1. 应用进程对已打开文件的文件描述符执行读**系统调用**(库函数)。
2. 独立于设备的I/O软件**检查参数**是否正确，若正确，检查**高速缓存**中有无要读取的信息块
   1. 若有，从缓冲区直接读至用户区，**完成I/O请求**。
   2. 若数据不在缓冲区，执行物理I/O操作，独立于设备的I/O软件将设备的逻辑名转换成物理名，检查对设备操作的许可权，将I/O请求排队，阻塞应用进程且等待I/O操作完成。
3. 内核启动设备驱动程序，分配存放读出块的缓冲区，准备接收数据并向设备控制寄存器发送启动命令，或建立DMA传输，启动I/O。
4. 设备控制器操作设备，执行数据传输。
5. 当采用DMA控制器控制数据传输时，一旦传输完成，硬件产生I/O结束中断。
6. CPU响应中断，转向磁盘中断处理程序。它检查中断产生原因和设备的执行状态，若设备有错，向设备驱动程序发信号，检查是否能重复执行，如果允许，重发启动设备命令，再次传输;否则，向上层软件报告错误。若设备I/O正确完成，将数据传输到指定的用户进程空间，唤醒阻塞进程并将其放人就绪队列；然后，系统检查有无I/O请求在排队，若有，再启动设备，继续传输。至此，中断处理完成且返回，将成功或失败的信息逐层向上报告。
7. 当应用进程被再次调度执行时，从I/O系统调用的断点处恢复执行。

# 4. 缓冲技术
1. 缓冲区:在**内存**中开辟的存储区，专门用于临时存放I/O操作的数据

## 4.1. 设置I/O缓冲的目的
1. 解决**CPU与设备之间速度不匹配**的矛盾，协调逻辑记录大小和物理记录大小不一致的问题
2. 减少I/O操作对CPU的中断次数
3. 放宽对CPU中断响应时间的要求
4. 提高CPU和设备的并行性

## 4.2. 实现缓冲技术的基本思想
1. **写操作**：先向系统申请一个输入缓冲区，将数据送至缓冲区，直到装满或需要写存储，待适当时候系统将缓冲区内容写到设备上
2. **读操作**：先向系统申请一个输出缓冲区，系统将设备上的物理记录读至缓冲区，根据要求将当前所需要的数据从缓冲区中读出并传送给进程

## 4.3. 单缓冲
1. 每当应用程序发出I/O操作时，操作系统在主存(内存)的系统区中开设一个缓冲区

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/14.png)

2. 如果希望输入的数据被加工后再输出，则需要双缓冲。

### 4.3.1. 工作机制
1. 输入：将数据读至缓冲区，系统将缓冲区数据送至用户区，应用程序对数据进行处理；如此往复，系统读入后续的数据
2. 输出：把数据从用户区复制到缓冲区，再将数据输出后，应用程序继续请求输出

### 4.3.2. 性能计算
> 读取到缓冲区需要时间T，从缓冲区到用户区耗时M，应用程序计算耗时C
1. 无缓冲:T + C
2. 单缓冲：max(C, T) + M，M << C,T

## 4.4. 双缓冲
1. 操作系统在主存的系统区中开设两个缓冲区

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/15.png)

### 4.4.1. 工作机制
1. 输入：
   1. 设备首先将数据输入缓冲区1，系统再从缓冲区1把数据传到用户区，供应用程序处理，同时从设备数据传送到缓冲区2
   2. 当缓冲区1为空，则再次从设备读出数据到缓冲区1，将缓冲区2的数据传送到用户区，供应用程序处理，同时从设备数据传送到缓冲区1
   3. 仅当两个缓冲区全为空，并且进程还要提取数据时等待。
2. 输出：
   1. 第一张卡片读入缓冲区1，在打印缓冲区1中数据的同时，又把第二张卡片读入缓冲区2。
   2. 缓冲区1打印完毕时，缓冲区2也刚好输入完毕，让读卡机和打印机交换缓冲区。这样，I/O设备就能够处于并行工作状态。

### 4.4.2. 性能分析
1. C < T，输入比计算慢：M << T，因此一块数据的传输和处理时间为T，即max(C, T)
2. C > T，输入比计算快：计算完成后，需要用M的时间来传输，所以一块数据的传输和处理时间为C + M，即max(C, T) + M

## 4.5. 多缓冲
1. 多缓冲组成的循环缓冲技术：解决了上面的C和T时间不匹配而导致的缓冲区被抽空或塞满的问题(**解决设备和进程速度不匹配**的问题)
2. 操作系统分配一组缓冲区，每个缓冲区度有指向下一个缓冲区的链接指针，最后一个缓冲区指针指向第一个缓冲区，组成循环缓冲，缓冲区的大小等于物理记录的大小，多缓冲的缓冲区是系统的**公共资源**，可供进程共享并由系统**统一分配和管理**。缓冲区用途可分为输人缓冲区、处理缓冲区和输出缓冲区。为了管理各类缓冲区，执行各种操作，必须设计专门的软件，这就是缓冲区自动管理系统。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/16.png)

3. 补充：数据缓冲区高速缓冲的实现思想(P267)

# 5. 驱动调度技术

## 5.1. 磁盘的物理结构
1. 磁盘是一种直接存取存储设备，又称为随机存取存储设备，每条物理记录都有明确的位置和唯一的地址。
2. 按照三维坐标进行随机存储。

### 5.1.1. 磁盘的组成
1. **磁盘**由多个**盘片**组成，每个盘片被划分为多个**同心圆**结构的磁道，每个盘片的两面都是可以数据的
2. 同盘片上位于相同位置的磁道构成的圆柱体称为**柱面**
3. 每个磁道分为固定多个或不等个数的**扇区**：为了对大量扇区寻址，操作系统将相邻的扇区组合成簇存储文件

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/17.png)

### 5.1.2. 物理块(扇面)在磁盘上的三维地址(磁头号，柱面号，扇区号)
1. 盘面号也被叫做**磁头号**
2. 磁道号也被叫做**柱面号**
3. 区别:"0面0道1扇区"中的"面"是指磁头，不是柱面
   1. **面和道都是0开始**
   2. **扇区是从1开始**

## 5.2. 磁盘读写数据
1. 读写数据时，磁头必须定位到指定的磁道上的指定扇区的开始处
2. 过程
   1. **寻道**：控制移动臂到达指定柱面，选择磁头号，**查找时间**
   2. **旋转**：等待要读写的扇区旋转到磁头下，**搜索延迟**
   3. **数据传送**
3. 高效的外存储都是用磁盘来完成的。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/18.png)

## 5.3. 磁盘存取时间
> 磁盘完成数据读写所需要的时间:是**寻道时间、旋转延迟、传送时间**的总和

$$
T_a = T_s + \frac{1}{2r} + \frac{b}{rN}
$$

- $T_a$:存取时间
- $T_s$:寻道时间
- $r$:磁盘旋转速度(单位：转/秒)
- $b$:要传送的字节数
- $N$:一个磁道中的字节数

# 6. 磁盘的驱动调度

## 6.1. 磁盘调度策略
1. 磁盘可能同时接收到若干I/O请求：如果随机选择并响应I/O请求，可能得到最坏的性能
2. 驱动调度：
   1. 系统采用一种调度策略，能够按**最佳次序**执行要求访问磁盘的多个I/O请求
   2. 能减少为若干I/O请求服务所需要消耗的**总时间**
3. 调度策略包括
   1. 旋转调度
   2. 移臂调度

## 6.2. 旋转调度
1. 目的:**使得旋转延迟的总时间最少**

### 6.2.1. 旋转排序
1. 通过优化I/O请求排序，在**最少旋转圈数**内完成位于同一柱面的访问请求
2. **旋转位置测定硬件**和多磁头同时读写技术有利于提高旋转调度的效率
3. 考虑磁道上保存四个物理块的旋转型设备，旋转1周需时20ms，假定收到以下四个I/O请求。请求次序记录号：读记录4、读记录3、读记录2、读记录1
4. 多种循环排序
   1. 方法1：按照I/O请求次序读记录4、3、2、1，平均用1/2周定位，再加上1/4周读出记录，总处理时间等于1/2+1/4+3×3/4=3周，即60ms。
   2. 方法2：如果次序为读记录1、2、3、4，总处理时间等于1/2+1/4+3×1/4=1.5周，即30ms。
   3. 方法3：如果知道当前读位置是记录3，则采用次序为读记录4、1、2、3，总处理时间等于4×1/4＝1周，即20ms。

### 6.2.2. 优化分布
1. 通过信息在存储空间的排列方式来减少旋转延迟
2. **交叉因子**：如果沿着磁道按序对扇区编号，可能由于磁盘转速太快，造成处理当前扇区的数据时，下一个扇区已经跳过，需要再转一圈才能继续读数据。因此，对扇区编号时会间隔编号，例如交叉因子为2:1表示相邻编号之间会间隔1个扇区，3:1表示会间隔2个扇区。
3. 按柱面而非盘面进行数据读写：连续记录数据时，先记录在同一柱面的不同磁道上，然后再更换柱面，可以减少数据读写时的移臂操作
4. 考虑10个逻辑记录A，B，...，J被存于旋转型设备上，每道存放10个记录，安排如下：
   1. 按照优化前：处理10个记录的总时间：10ms(移动到记录A的平均时间)+ 2ms(读记录A)+4ms(处理记录A)+9×[16ms(访问下一记录) +2ms(读记录)+4ms(处理记录)] ＝214ms
   2. 按照优化后：处理10个记录的总时间为：10ms(移动到记录A的平均时间)+10×[ 2ms(读记录) + 4ms(处理记录) ]=70ms

| 优化前               | 优化后               |
| -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/27.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/28.png) |


## 6.3. 移臂调度
目的：使移动臂的移动时间最短，从而减少寻道总时间

### 6.3.1. 先来先服务算法 FCFS
1. 移臂距离大，性能不好，移动臂是**随机移动**，寻道性能较差
3. 按顺序处理请求，对所有进程公平

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/22.png)

### 6.3.2. 最短查找时间优先(最小短距离法) SSTF，Shortest Service Time First
1. 先执行**查找时间最短**的请求，具有较好的寻道性能，**存在"饥饿"现象**：距离比较远的被满足
2. 选择使磁头臂从当前位置开始移动最少的磁盘I/O请求，因此SSTF策略总是选择导致**最小寻道时间**的请求，总是选择最小寻道时间并不能保证平均寻道时间最小，但是，它的性能比FCFS更好

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/21.png)

### 6.3.3. 扫描算法 SCAN算法
1. 移动臂每次向一个方向移动，遇到最近的I/O请求便进行处理，到达**最后一个**柱面后再向相反方向移动
2. 对最近扫描所跨越区域的请求响应较慢
3. 和电梯调度算法的不同：碰壁才会折返

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/23.png)

### 6.3.4. 分布扫描算法 N-step-SCAN
1. 进程**重复请求同一磁道会垄断整个设备造成磁头臂的粘性**，采用分步扫描可避免这类问题
   1. **把磁盘I/O请求队列分成长度为N的子队列，按照FIFI处理每一个子队列，每个子队列内部使用扫描算法**
   2. 在处理一个队列时，新请求必须添加到**其他**某个队列中
   3. 处理完一个子队列后再服务下一个队列
2. 如果在扫描的最后剩下的请求数小于N，则它们全部将在下一次扫描时处理
   1. 当$N \rightarrow \infty$时，N-step-SCAN的性能接近SCAN
   2. 当$N = 1$时，实际上是FIFO

### 6.3.5. 电梯调度(LOOK 算法)
1. 无请求时移动臂停止不动，有请求时按电梯规律移动
2. 每次选择沿移动臂的移动方向最近的柱面
3. 如果当前移动方向上没有但相反方向有请求时，改变移动方向

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/26.png)

### 6.3.6. 循环扫描(C-SCAN)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/24.png)

1. 把扫描限定在一个方向
2. 当访问到沿某个方向的最后一个磁道时，磁头臂返回到磁盘相反方向磁道的末端，并再次开始扫描

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/38.png)

### 6.3.7. 补充：后进先出(LIFO，Last-in,first-out)
1. 在事务处理系统中，把设备资源提供给最近的用户，会导致磁头臂**在一个顺序文件中移动时移动得很少，甚至不移动**
2. **利用这种局部性可以提高吞吐量，减少队列长度**
3. 只要一个作业积极地使用文件系统，它就可以尽可能快地得到处理
4. 如果由于工作量大而**磁盘保持忙**状态，就有可能出现**饿死**的情况
5. 当一个作业已经往队列中送入一个I/O请求，并且错过了可以提供服务的位置时，该作业就有可能永远得不到服务，除非它之前的队列变为空

### 6.3.8. 补充：单向扫描
1. 移动臂总向一个方向扫面，归途中不提供服务
2. 适用于不断有大量柱面均匀分布的请求的情形
3. 要求磁头臂仅仅沿一个方向移动，并在途中满足所有为完成的请求，直到它到达这个方向上的**最后一个磁道**，或者**在这个方向上没有其他请求**为止，后一种改进有时候称为LOOK策略 (又称为电梯调度算法)
4. 接着反转服务方向，沿着相反方向扫描，同样按顺序完成所有请求

## 6.4. 提高磁盘I/O速度的办法
1. 提前读：按照顺序访问时，可以读当前磁盘块时，提前把下一个磁盘块的数据也读入磁盘缓冲区。
2. 延迟写：由于缓冲区的数据不久以后还会再次被进程访问，因此不立即将缓冲区中的数据写回盘，而是挂载空闲缓冲区队列队尾，直到移动到空闲缓冲区队首时在写回。
3. 虚拟盘：用内存空间仿真磁盘，又叫RAM盘，相应的操作在内存中执行而不是硬盘中，比如：浏览器缓存等。

## 6.5. 磁盘循环冗余阵列

### 6.5.1. RAID 0(无冗余)
1. RAID 0连续的数据条带(每个条带可规定为1个或多个扇区)以轮转方式写到全部磁盘上。
2. 然后，采用并行交叉存取，减少I/O请求排队时间，适用于大数据量的I/O请求，但并**无冗余校验功能，可靠性较差。**

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/29.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/30.png) |
| -------------------- | -------------------- |

### 6.5.2. RAID 1(镜像)
1. RAID 1采用镜像盘双份所有数据来提高容错性，读请求拥有最小寻道时间，写请求可并行完成。**缺点是容量下降一半，故成本很高**

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/31.png)

### 6.5.3. RAID 2(通过海明码冗余)
1. RAID 2采用数据字或字节交叉存放，**并行存取获得高性能**，使用**海明校验码**，适合大量顺序数据访问。由于**使用多个冗余盘，成本较高**
2. <a href = "https://blog.csdn.net/weixin_42426249/article/details/89428080">海明校验码</a>
3. 按照海明码编码方式我们首先对原数据生成新数据，然后之后校验数据将对应校验码做异或，如果全为0则为正确，否则则为错误位置。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/32.png)

### 6.5.4. RAID 3(交错位奇偶校验)
1. RAID 3是RAID 2的简化版本，差别是它仅用一只冗余盘，采
用奇偶校验技术。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/33.png)

### 6.5.5. RAID 4(块奇偶校验)
1. RAID 4采用**独立存取磁盘阵列，数据条带交叉存放**，访问请求可并行地获得满足，适合有较高I/O请求速度的应用场合，使用一只冗余盘存放奇偶校验90码

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/34.png)

### 6.5.6. RAID 5(块分布奇偶校验)
1. RAID 5与RAID 4的组织类似，但奇偶校验码循环分布在每个盘上使容错性更好。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/35.png)

### 6.5.7. RAID 6(双重冗余)
1. RAID 6采用双重冗余技术， P和Q是两种不同的数据校验算法，其中一种是RAID 4和RAID 5所使用是异或计算，另一种是独立数据校验算法，即使有两个数据磁盘发生错误，也可重新生成数据。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/36.png)

## 6.6. 磁盘Cache
1. 磁盘高速缓存是主存中为磁盘扇区设置的一个缓冲区，包含磁盘中某些扇区的副本
3. 利用局部性原理，可以减少平均存储器存取时间

### 6.6.1. 替换策略:LRU
1. 替换在高速缓存中**未被访问的时间最长**的块
2. 逻辑上，高速缓存有一个关于块的栈组成，最近访问过的块在栈顶，当高速缓存中的一个块被访问到时，它从栈中当前的位置移到栈顶
3. 当一个块从辅存中取入时，把位于栈顶的那一块移出，并把新到来的块压入栈顶
4. 并不需要在主存中真正移动这些块，有一个栈指针与高速缓存相关联

### 6.6.2. 替换策略:LFU(Least Frequently Used)
1. 替换集合中**被访问次数最少**的块
2. LFU可以通过给每个块关联一个计数器来实现
3. 当一个块被读入时，它的计数器被指定为1；当每次访问到这一块时，它的计数器增1
4. 当需要替换时，选择计数器值最小的块
5. 直觉上，LFU比LRU更适合，因为LFU使用了关于每个块的更多的相关信息

# 7. 设备分配

## 7.1. 设备独立性
1. 问题：作业执行前对设备提出申请时，指定某台具体的物理设备会让设备分配变得简单，但如果所指定设备出现故障，即便计算机系统中有同类设备也不能运行
2. **设备独立性**：用户通常不指定物理设备，而是指定**逻辑设备**，使得用户作业和物理设备分离开来，再通过其它途径建立逻辑设备和物理设备之间的映射，包含两种
   1. **静态重定位**
   2. **动态重定位**：当前多用，对硬件要求更高一些。
3. 设备管理的功能就是将**逻辑设备名转换为物理设备名**，为此系统需要提供逻辑设备名和物理设备名的对应表以供转换使用。
   1. 逻辑设备号由用户定义。
   2. 物理设备号由系统规定，不可修改。
4. 微型计算机的操作系统中不一定支持设备独立性。
5. 设备独立性的优点
   1. 应用程序与**具体物理设备**无关，系统增减或变更设备时不需要修改源程序
   2. 易于应对**I/O设备故障**，提高系统可靠性
   3. 增加设备分配的**灵活性**，更有效地利用设备资源，实现多道程序设计

## 7.2. 设备分配方式
1. 设备管理的功能之一就是为计算机系统所接纳的每个计算任务分配所需要的外部设备。

### 7.2.1. 设备的物理特性
1. **独占型设备**：一次只能由一个进程独占使用
   1. 只能由一个进程独占式使用
   2. 可以让多个进程同时使用的设备称为"共享设备"，其管理工作主要是驱动调度和实施驱动，一般不必分配
2. 共享设备
3. 虚拟设备

### 7.2.2. 分配方式
1. **静态分配**：进程运行前申请，实现简单，能够防止系统发生**死锁**，但会降低设备利用率，独占型设备多选
2. **动态分配**：进程随用随申请，提高设备利用率，但是对于打印机等独占型设备使用动态分配可以显著提高设备利用率。

### 7.2.3. 联系PV操作
1. 操作过程：$... P(S_1) ... D(S_1)...$
2. $P(S_1)$:申请$D_1$设备
3. 然后在临界区内互斥使用该设备，独占式
4. $V(S_1)$:归还$D_1$设备
5. $S_1$代表设备$D_1$资源，P操作前和V操作后都是代码
6. 存在死锁风险

## 7.3. 设备分配的数据结构

### 7.3.1. 设备类表
1. 每类设备对应于**设备类表**的中的一栏
2. 包括：设备类、总台数、空闲台数、设备表起始地址等
3. 支持设备独立性时才会使用

### 7.3.2. 设备表
1. 每类设备都有**各自的设备表**，用来登记这类设备中的**每台物理设备**
2. 包括：物理设备名(号)、逻辑设备名(号)、占有设备的进程号、是否分配、好/坏标志等

### 7.3.3. 通道结构系统
1. 需要对通道、控制器和每台物理设备进行管理和控制，必须设置系统设备表、通道控制表、控制器控制表和设备控制表。
   1. 整个系统建立一张系统设备表，记录系统配置的所有物理设备的情况，每台物理设备占有一栏，包括设备类型、台数、设备号、设备控制表指针等。
   2. 对于通道控制表、控制器控制表和设备控制表，每个通道、控制器、设备各设置一张，分别记录各自的地址（标识符）、状态（忙/闲、已分配/未分配）、等待获得此部件的进程队列指针及一次分配后相互链接的指针，以备分配和执行I/O操作时使用。

## 7.4. 虚拟设备
1. 使用一类物理设备模拟另一类物理设备的技术，让独享型设备变为共享设备
2. 示例
   1. 内存卡模拟磁盘
   2. 块设备模拟字符设备
   3. 输入输出重定向

### 7.4.1. SPOOLing设备
1. 在**内核外运行**的**系统**I/O软件，采用**预输入、缓输出和井管理**技术，是多道程序设计系统中处理**独占型设备**的一种方法，通过创建守护进程和特殊目录解决**独占型设备**的**空占**问题
2. 为存放输入数据和输出数据，系统在磁盘上开辟**输入井和输出井**
3. "井"是用作缓冲的存储区域，采用井的技术能调节**供求之间的矛盾**，消除**人工干预**带来的损失。
4. 不仅**设备利用率提高**，作业的**运行时间也会缩短**，每个作业都感觉各自拥有所需的独占设备

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/19.png)

### 7.4.2. SPOOLing设备组成
1. **预输入**程序
   1. 将数据从**输入设备**传送到**磁盘输入井**
   2. 操作系统将一批作业从输入设备上预先输入到磁盘的输入缓冲区中暂时保存，这称为"预输入"
   3. 此后，由**作业调度程序**调度作业执行，作业使用数据时不必再启动输入设备，只要从磁盘的输入缓冲区中读入
2. **缓输出**程序
   1. 将数据从**磁盘输出井**传送到**输出设备**
   2. 作业执行中不必**直接**启动输出设备，只要将作业的输出数据暂时保存到磁盘的输出缓冲区
   3. 当作业执行完毕后，由操作系统组织信息成批输出
3. **井管理**程序
   1. 控制作业和井之间的数据交换
   2. 放置在井中的文件被称为**井文件**，经文件空间管理简单，它被划分为等长的的物理块，每块用来存放一条或多条逻辑记录。
4. 系统有一张作业表来登记进入系统的所有作业的JCB，包括作业名、作业状态等信息。
5. 预输入表用来登记作业的各个输入文件的情况。
6. 缓输出表用来登记作业的各个输出文件的情况。

### 7.4.3. 输入井的作业状态
1. 输入状态：正在预输入
2. 收容状态：预输入完成，等待执行
3. 执行状态：作业选中执行，正在从输入井读取输入，向输出井写入数据
4. 完成状态：作业已经撤离，输出结果等待缓输出。
5. 通过预处理，结合井管理，可以实现为**脱机状态**，从联机(online)到脱机(offline)，成功耦合。

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/20.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-OS/img/lec4/37.png) |
| -------------------- | -------------------- |

1. 作业调度：决定有生命周期的进程的道数

### 7.4.4. SPOOLing步骤
1. **预输入**：操作系统将作业需要的输入数据成批从输入设备上预先输入至磁盘的输入缓冲区中暂存:调度作业执行时，作业使用数据不必再启动输入设备，从磁盘的输入缓冲区读入即可
2. **缓输出**：作业不启动输出设备，只是将输出数据暂存到磁盘的输出缓冲区:作业执行完毕后，处理器空闲时，操作系统调用缓输出程序执行缓输出。

### 7.4.5. 打印机SPOOLing
1. 打印机空占问题：如果用户进程通过打开打印机的设备文件来申请和使用打印机，往往会造成该进程打开**设备文件**后长达数小时不用，但**其他进程又无法使用打印机**
2. 打印机守护进程和SPOOLing打印目录
   1. **守护进程**是唯一有**特权**使用打印机设备的进程
   2. 打印文件前，用户进程先产生完整的**待输出文件**，并存放在打印目录下
   3. 打印机空闲时，启动守护进程，打印**待输出文件**

### 7.4.6. 网络通信SPOOLing守护进程
1. SPOOLing技术不仅可用于打印机，还可用于其他场合。
2. 例如，在网络上传输文件常使用网络守护进程，发送文件之前先将其放在特定的网络SPOOL目录下，而后由网络通信守护进程将其取出并发送出去。
3. 这种文件传送方式的用途之一是因特网电子邮件系统
   1. 此网络将全世界数以千万台计的计算机连接在一起，通过通信网络进行通信。
   2. 当向某人发送电子邮件时，用户使用一个类似于send的程序，它接收所要发送的信件并将其送人固定的电子邮件SPOOL目录下等待以后发送，整个电子邮件系统在操作系统之外作为一种应用程序运行。