lec09-板级支持包与系统引导
---

<!-- TOC -->

- [1. 嵌入式软件运行流程](#1-嵌入式软件运行流程)
  - [1.1. 上电复位、板级初始化阶段](#11-上电复位板级初始化阶段)
  - [1.2. 系统引导/升级阶段](#12-系统引导升级阶段)
  - [1.3. 系统引导阶段，系统引导有⼏种情况：](#13-系统引导阶段系统引导有种情况)
  - [1.4. 系统升级阶段](#14-系统升级阶段)
  - [1.5. 系统初始化阶段](#15-系统初始化阶段)
  - [1.6. 应⽤初始化阶段](#16-应初始化阶段)
  - [1.7. 多任务应⽤运⾏阶段](#17-多任务应运阶段)
- [2. 板级支持包BSP](#2-板级支持包bsp)
  - [2.1. BSP在嵌入式系统中所处的位置](#21-bsp在嵌入式系统中所处的位置)
  - [2.2. BSP中的驱动程序](#22-bsp中的驱动程序)
  - [2.3. BSP和BIOS/UEFI的区别](#23-bsp和biosuefi的区别)
  - [2.4. 不同系统中的BSP](#24-不同系统中的bsp)
  - [2.5. BSP的特点与功能](#25-bsp的特点与功能)
  - [2.6. 嵌入式系统初始化以及BSP的功能](#26-嵌入式系统初始化以及bsp的功能)
  - [2.7. 初始化过程](#27-初始化过程)
    - [2.7.1. 片级初始化](#271-片级初始化)
    - [2.7.2. 板级初始化](#272-板级初始化)
    - [2.7.3. 系统级初始化](#273-系统级初始化)
- [3. Bootloader](#3-bootloader)
  - [3.1. RTOS的引导模式](#31-rtos的引导模式)
  - [3.2. BootLoader](#32-bootloader)
  - [3.3. PC机中的引导加载程序](#33-pc机中的引导加载程序)
  - [3.4. 嵌入式系统中引导加载程序](#34-嵌入式系统中引导加载程序)
  - [3.5. 固态存储设备的典型空间分配结构](#35-固态存储设备的典型空间分配结构)
  - [3.6. 用来控制Boot Loader的设备或机制](#36-用来控制boot-loader的设备或机制)
  - [3.7. Boot Loader的启动过程是单阶段还是多阶段的](#37-boot-loader的启动过程是单阶段还是多阶段的)
  - [3.8. Boot Loader的操作模式(Operation Mode)](#38-boot-loader的操作模式operation-mode)
  - [3.9. BootLoader与主机之间进行文件传输所用的通信设备及协议](#39-bootloader与主机之间进行文件传输所用的通信设备及协议)
  - [3.10. Boot Loader的主要任务](#310-boot-loader的主要任务)
  - [3.11. Boot Loader 的Stage2可执⾏映像被拷⻉到内存后内存布局情况](#311-boot-loader-的stage2可执映像被拷到内存后内存布局情况)
  - [3.12. BootLoader的调试](#312-bootloader的调试)
  - [3.13. U-boot](#313-u-boot)
  - [3.14. RedRoot](#314-redroot)
  - [3.15. vivi](#315-vivi)

<!-- /TOC -->

# 1. 嵌入式软件运行流程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/1.png)

## 1.1. 上电复位、板级初始化阶段
1. 嵌⼊式系统上电复位后完成板级初始化⼯作。
2. 板级初始化程序具有完全的硬件特性，⼀般采⽤汇编语⾔实现。不同的嵌⼊式系统，板级初始化时要完成的⼯作具有⼀定的特殊性，但以下⼯作⼀般是必须完成的：
   1. CPU中堆栈指针寄存器的初始化。
   2. BSS段(Block Storage Space表示未被初始化的数据)的初始化。
   3. CPU芯⽚级的初始化：中断控制器、内存等的初始化。

## 1.2. 系统引导/升级阶段
1. 根据需要分别进⼊系统软件引导阶段或系统升级阶段。
2. 软件可通过测试通信端⼝数据或判断特定开关的⽅
式分别进⼊不同阶段。

## 1.3. 系统引导阶段，系统引导有⼏种情况：
1. 将系统软件从NOR Flash中读取出来加载到RAM中运⾏：这种⽅式可以解决成本及Flash速度⽐RAM慢的问题。软件可压缩存储在Flash中。
2. 不需将软件引导到RAM中⽽是让其直接在NorFlash上运⾏，进⼊系统初始化阶段。
3. 将软件从外存(如NandFlash、CF卡、MMC等)中读取出来加载到RAM中运⾏：这种⽅式的成本更低。

## 1.4. 系统升级阶段
1. 进⼊系统升级阶段后系统可通过⽹络进⾏远程升级或通过串⼝进⾏本地升级。
2. 远程升级⼀般⽀持TFTP、FTP、HTTP等⽅式。
3. 本地升级可通过Console⼝使⽤超级终端或特定的升级软件进⾏。

## 1.5. 系统初始化阶段
1. 在该阶段进⾏操作系统等系统软件各功能部分必需的初始化⼯作，如根据系统配置初始化数据空间、初始化系统所需的接⼝和外设等。
2. 系统初始化阶段需要按特定顺序进⾏，如⾸先完成内核的初始化，然后完成⽹络、⽂件系统等的初始化，最后完成中间件等的初始化⼯作。

## 1.6. 应⽤初始化阶段
1. 在该阶段进⾏应⽤任务的创建，信号量、消息队列的创建和与应⽤相关的其它初始化⼯作。

## 1.7. 多任务应⽤运⾏阶段
1. 各种初始化⼯作完成后，系统进⼊多任务状态，操作系统按照已确定的算法进⾏任务的调度，各应⽤任务分别完成特定的功能。

# 2. 板级支持包BSP
1. BSP全称"板级⽀持包"(Board Support Packages)，说的简单⼀点，就是⼀段启动代码，和计算机主板的BIOS差不多，但提供的功能区别就相差很⼤。

## 2.1. BSP在嵌入式系统中所处的位置
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/2.png)

## 2.2. BSP中的驱动程序
1. 抽象物理设备或虚拟设备的功能软件，⽤于管理这些设备的操作。
2. 驱动程序的基本功能
   1. 对设备初始化和释放
   2. 对设备进⾏管理
   3. 读取应⽤程序传送给设备⽂件的数据，并回送应⽤程序的请求数据
   4. 检测和处理设备出现的错误

## 2.3. BSP和BIOS/UEFI的区别
1. BIOS主要是负责在电脑开启时检测、初始化系统设备(设置栈指针，中断分配，内存初始化..)、装⼊操作系统并调度操作系统向硬件发出的指令。 UEFI,"统⼀的可扩展固件接⼝",旨在代替BIOS, 提⾼软件互操作性和解决BIOS的局限性。
2. BSP是和操作系统绑在⼀起运⾏，尽管BSP的开始部分和BIOS所做的⼯作类似，但是 BSP还包含和系统有关的基本驱动 。
3. BIOS程序是⽤户不能更改，编译编程的，只能对参数进⾏修改设置，但是程序员还可以编程修改BSP，在BSP中任意添加⼀些和系统⽆关的驱动或程序，甚⾄可以把上层开发的统统放到BSP中

## 2.4. 不同系统中的BSP
1. ⼀个嵌⼊式操作系统针对不同的CPU，会有不同的BSP。
2. 即使同⼀种CPU，由于外设的⼀点差别BSP相应的部分也不⼀样

## 2.5. BSP的特点与功能
1. 硬件相关性：因为嵌⼊式实时系统的硬件环境具有应⽤相关性，所以，作为⾼层软件与硬件之间的接⼝，BSP必须为操作系统提供操作和控制具体硬件的⽅法。
2. 操作系统相关性：不同的操作系统具有各⾃的软件层次结构，因此，不同的操作系统具有特定的硬件接⼝形式。

## 2.6. 嵌入式系统初始化以及BSP的功能
1. 嵌⼊式系统的初始化过程是⼀个同时包括硬件初始化和软件初始化的过程；⽽操作系统启动以前的初始化操作是BSP的主要功能之⼀
2. 初始化过程总可以抽象为三个主要环境，按照⾃底向上、从硬件到软件的次序依次为：
   1. ⽚级初始化
   2. 板级初始化
   3. 系统级初始化

## 2.7. 初始化过程

### 2.7.1. 片级初始化
1. 主要完成CPU的初始化
   1. 设置CPU的核⼼寄存器和控制寄存器
   2. CPU核⼼⼯作模式
   3. CPU的局部总线模式等
2. ⽚级初始化把CPU从上电时的缺省状态逐步设置成为系统所要求的⼯作状态
3. 这是⼀个纯硬件的初始化过程初始化过程

### 2.7.2. 板级初始化
1. 完成CPU以外的其他硬件设备的初始化
2. 同时还要设置某些软件的数据结构和参数，为随后的系统级初始化和应⽤程序的运⾏建⽴硬件和软件环境
3. 这是⼀个同时包含软硬件两部分在内的初始化过程

### 2.7.3. 系统级初始化
1. 这是⼀个以软件初始化为主的过程，主要进⾏操作系统初始化
2. BSP将控制转交给操作系统，由操作系统进⾏余下的初始化操作：
   1. 包括加载和初始化与硬件⽆关的设备驱动程序
   2. 建⽴系统内存区
   3. 加载并初始化其他系统软件模块(如⽹络系统、⽂件系统等)
3. 最后，操作系统创建应⽤程序环境并将控制转交给应⽤程序的⼊⼝

# 3. Bootloader

## 3.1. RTOS的引导模式
1. 操作系统引导概念：将操作系统装⼊内存并开始执⾏的过程。
2. 按时间效率和空间效率不同的要求，分为两种模式：
   1. 不需要BootLoader的引导模式：时间效率⾼，系统快速启动，直接在NOR flash或ROM系列⾮易失性存储介质中运⾏，但不满⾜运⾏速度的要求。
   2. 需要BootLoader的引导模式：节省空间，牺牲时间，适⽤于硬件成本低，运⾏速度快，但启动速度相对慢

## 3.2. BootLoader
1. 嵌⼊式系统中的 OS 启动加载程序
2. 引导加载程序
   1. 包括固化在固件(firmware)中的 boot 代码(可选)，和Boot Loader两⼤部分
   2. 是系统加电后运⾏的第⼀段软件代码
3. 相对于操作系统内核来说，它是⼀个硬件抽象层

## 3.3. PC机中的引导加载程序
1. 两部分组成
   1. BIOS(其本质就是⼀段固件程序)
   2. 位于硬盘 MBR 中的 OS Boot Loader(如LILO 和 GRUB 等)
2. 流程
   1. BIOS 在完成硬件检测和资源分配后，将硬盘 MBR 中的 Boot Loader 读到系统的 RAM 中，然后将控制权交给 OS Boot Loader
   2. Boot Loader 的主要运⾏任务就是将内核映象从硬盘上读到 RAM 中，然后跳转到内核的⼊⼝点去运⾏，即开始启动操作系统。


## 3.4. 嵌入式系统中引导加载程序
1. 没 BIOS 那样的固件程序：有的嵌⼊式 CPU 也会内嵌⼀段短⼩的启动程序
2. 系统的加载启动任务就完全由 Boot Loader 来完成
   1. ARM7TDMI中，系统在上电或复位时从地址 0x00000000 处开始执⾏
   2. 这个地址是Boot Loader 程序
3. 存储位置
   1. 按地址随机存取的永久性记忆存储器
   2. ⽀持NANDFlash启动的SOC
4. 复制过程
   1. 硬件⽅式
   2. 软件⽅式
   3. 内存映射

## 3.5. 固态存储设备的典型空间分配结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/3.png)

## 3.6. 用来控制Boot Loader的设备或机制
1. 主机和⽬标机之间⼀般通过串⼝建⽴连接
2. Boot Loader执⾏时通常会通过串⼝进⾏ I/O：如输出打印信息到串⼝，从串⼝读取⽤户控制字符等

## 3.7. Boot Loader的启动过程是单阶段还是多阶段的
1. 多阶段的 Boot Loader
   1. 提供更为复杂的功能，以及更好的可移植性
   2. 从固态存储设备上启动的 Boot Loader ⼤多都是 2 阶段的启动过程
2. BOOTLOADER⼀般分为2部分
   1. 汇编部分执⾏简单的硬件初始化
   2. C语⾔部分负责复制数据,设置启动参数,串⼝通信等功能
3. BOOTLOADER的⽣命周期
   1. 初始化硬件,如设置UART(⾄少设置⼀个),检测存储器等
   2. 设置启动参数,告诉内核硬件的信息,如⽤哪个启动界⾯,波特率.
   3. 跳转到操作系统的⾸地址.
   4. 消亡

## 3.8. Boot Loader的操作模式(Operation Mode)
1. 两种不同的操作模式
   1. 启动加载模式
      1. ⾃主(Autonomous)模式
      2. 从⽬标机上的某个固态存储设备上将操作系统加载到 RAM 中运⾏
      3. Boot Loader 的正常⼯作模式
   2. 下载模式
      1. 通过串⼝连接或⽹络连接等通信⼿段从主机(Host)下载文件，如：下载内核映像和根⽂件系统映像等。
      2. 从主机下载的⽂件通常⾸先被 Boot Loader 保存到⽬标机的 RAM 中，然后再被 BootLoader 写到⽬标机上的FLASH 类固态存储设备中
      3. 通常在第⼀次安装内核与根⽂件系统时被使⽤
      4. 系统更新也会使⽤ Boot Loader 的这种⼯作模式
      5. 通常都会向它的终端⽤户提供⼀个简单的命令⾏接⼝
2. Blob 或 U-Boot 等功能强⼤的 Boot Loader 通常同时⽀持这两种⼯作模式
   1. 允许⽤户在这两种⼯作模式之间进⾏切换，如Blob 在启动时处于正常的启动加载模式，但是它会延时 10 秒等待终端⽤户按下任意键⽽将blob 切换到下载模式。如10秒内没有⽤户按键，则 blob 继续启动 Linux 内核

## 3.9. BootLoader与主机之间进行文件传输所用的通信设备及协议
1. 通常⽬标机上的 Boot Loader 通过串⼝与主机之间进⾏⽂件传输
2. 传输协议：通常是 xmodem／ymodem／zmodem 协议中的⼀种
3. 可通过以太⽹连接并借助 TFTP 协议来下载⽂件
   1. 串⼝传输的速度是有限的
   2. 主机提供 TFTP 服务

## 3.10. Boot Loader的主要任务
1. stage1 通常包括以下步骤
   1. 硬件设备初始化
   2. 为加载 Boot Loader 的 stage2 准备 RAM 空间
   3. 拷⻉ Boot Loader 的 stage2 到 RAM 空间中
   4. 设置好堆栈
   5. 跳转到 stage2 的 C ⼊⼝点
2. Boot Loader 的 stage2 通常包括以下步骤
   1. 初始化本阶段要使⽤到的硬件设备
   2. 检测系统内存映射(memory map)
   3. 将 kernel 映像和根⽂件系统映像从 flash 上读到 RAM 空间中
   4. 为内核设置启动参
   5. 调⽤内核

## 3.11. Boot Loader 的Stage2可执⾏映像被拷⻉到内存后内存布局情况
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/4.png)

## 3.12. BootLoader的调试
1. 从交叉调试的技术实现途径及应⽤场合看，分为：
   1. 硬件调试：调试⽅便，价格昂贵
   2. 源码软件调试：点灯或串⼝输出
      1. 串⼝终端显示乱码或根本没有显示
         1. boot loader 对串⼝的初始化设置不正确。
         2. 运⾏在 host 端的终端仿真程序对串⼝的设置不正确，这包括：波特率、奇偶校验、数据位和停⽌位等⽅⾯的设置

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/5.png)

## 3.13. U-boot
1. 德国DENX软件⼯程中⼼的Wolfgang Denk
2. 全称Universal Boot Loader
   1. 遵循GPL条款的开放源码项⽬
   2. http://sourceforge.net/projects/U-Boot
   3. 从FADSROM、8xxROM 、PPCBOOT逐步发展演化⽽来
   4. 其源码⽬录、编译形式与Linux内核很相似
   5. 源码就是相应Linux内核源程序的简化，尤其是设备驱动程序
3. ⽀持
   1. 嵌⼊式Linux/NetBSD/VxWorks/QNX/RTEMS/ARTOS/LynxOS
   2. PowerPC、MIPS、x86、ARM 、Nios、XScale等处理器
   3. 对PowerPC系列处理器/对Linux的⽀持最完善

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec9/6.png)

## 3.14. RedRoot
1. Redhat公司随eCos发布的⼀个BOOT⽅案
2. 开源项⽬
3. ⽀持：ARM，MIPS，PowerPC，x86。。。
4. 使⽤X-modem或Y-modem协议经由串⼝下载，也可以经由以太⽹⼝通过BOOTP/DHCP服务获得IP参数，使⽤TFTP⽅式下载程序映像⽂件，常⽤于调试⽀持和系统初始化(Flash下载更新和⽹络启动)
5. Redboot可以通过串⼝和以太⽹⼝与GDB进⾏通信，调试应⽤程序，甚⾄能中断被GDB运⾏的应⽤程序
6. Redboot为管理FLASH映像，映像下载，Redboot配置以及其他如串⼝、以太⽹⼝提供了⼀个交互式命令⾏接⼝，⾃动启动后，REDBOOT⽤来从TFTP服务器或者从Flash下载映像⽂件加载系统的引导脚本⽂件保存在Flash上

## 3.15. vivi
1. vivi是由韩国Mizi公司开发的⼀种Bootloader
2. 适合于ARM9处理器
3. 源代码可以在http://www.mizi.com⽹站下载