Lecture07-The Real-Time Kernel
---

<!-- TOC -->

- [1. 任务管理](#1-任务管理)
  - [1.1. 任务主函数](#11-任务主函数)
  - [1.2. 任务优先级](#12-任务优先级)
  - [1.3. 空闲任务和统计任务](#13-空闲任务和统计任务)
  - [1.4. 任务控制块TCB](#14-任务控制块tcb)
  - [1.5. 栈指针](#15-栈指针)
  - [1.6. 链表指针](#16-链表指针)
  - [1.7. 空闲TCB链表](#17-空闲tcb链表)
  - [1.8. 指针数组(指向相应TCB)](#18-指针数组指向相应tcb)
  - [1.9. 状态的转换](#19-状态的转换)
  - [1.10. 任务就绪表](#110-任务就绪表)
    - [1.10.1. 根据优先级确定就绪表](#1101-根据优先级确定就绪表)
    - [1.10.2. 使任务脱离就绪态](#1102-使任务脱离就绪态)
  - [1.11. 任务的调度](#111-任务的调度)
  - [1.12. 根据就绪表确定最高优先级(为什么右移三位)](#112-根据就绪表确定最高优先级为什么右移三位)
  - [1.13. 任务调度器](#113-任务调度器)
  - [1.14. 源代码中使用了查表法](#114-源代码中使用了查表法)
  - [1.15. 优先级判定表OSUnMapTbl[256]](#115-优先级判定表osunmaptbl256)
  - [1.16. 从64->256](#116-从64-256)
  - [1.17. 任务切换](#117-任务切换)
    - [1.17.1. 任务级的任务切换OS_TASK_SW()](#1171-任务级的任务切换os_task_sw)
    - [1.17.2. 任务切换OS_TASK_SW()的代码](#1172-任务切换os_task_sw的代码)
    - [1.17.3. 给调度器上锁](#1173-给调度器上锁)
  - [1.18. 任务管理的系统服务](#118-任务管理的系统服务)
    - [1.18.1. 创建任务](#1181-创建任务)
    - [1.18.2. OSTaskCreate()](#1182-ostaskcreate)
    - [1.18.3. OSTaskCreate()的实现过程](#1183-ostaskcreate的实现过程)
    - [1.18.4. OSTaskCreateExt()](#1184-ostaskcreateext)
    - [1.18.5. 任务的栈空间](#1185-任务的栈空间)
    - [1.18.6. 动态分配](#1186-动态分配)
    - [1.18.7. 内存碎片问题](#1187-内存碎片问题)
    - [1.18.8. 栈的增长方向](#1188-栈的增长方向)
  - [1.19. 删除任务](#119-删除任务)
  - [1.20. 挂起和恢复任务](#120-挂起和恢复任务)
- [2. 中断和时间管理](#2-中断和时间管理)
  - [2.1. 中断处理](#21-中断处理)
  - [2.2. 中断服务程序ISR](#22-中断服务程序isr)
  - [2.3. 用户ISR的框架](#23-用户isr的框架)
    - [2.3.1. OSIntEnter()](#231-osintenter)
    - [2.3.2. OSIntExit()](#232-osintexit)
    - [2.3.3. OSIntCtxSw()](#233-osintctxsw)
    - [2.3.4. 调用中断切换函数OSIntCtxSw() 后的堆栈情况](#234-调用中断切换函数osintctxsw-后的堆栈情况)
  - [2.4. 时钟节拍](#24-时钟节拍)
    - [2.4.1. 时钟节拍ISR](#241-时钟节拍isr)
    - [2.4.2. 时钟节拍函数 OSTimetick()](#242-时钟节拍函数-ostimetick)
  - [2.5. 时间管理](#25-时间管理)
    - [2.5.1. OSTimeDLY()](#251-ostimedly)
    - [2.5.2. 问题](#252-问题)
    - [2.5.3. 解决方案](#253-解决方案)
    - [2.5.4. OSTimeDlyHMSM()](#254-ostimedlyhmsm)
    - [2.5.5. OSTimeDlyResume()](#255-ostimedlyresume)
    - [2.5.6. 系统时间](#256-系统时间)
    - [2.5.7. 何时启动系统定时器](#257-何时启动系统定时器)
    - [2.5.8. 时钟节拍的启动](#258-时钟节拍的启动)
    - [2.5.9. 系统的初始化与启动](#259-系统的初始化与启动)
  - [2.6. μC/OS-II的启动](#26-μcos-ii的启动)
    - [2.6.1. OSStart()](#261-osstart)
    - [2.6.2. 统计任务初始化函数 OSStatInit (void)](#262-统计任务初始化函数-osstatinit-void)
- [3. 任务之间的通信与同步](#3-任务之间的通信与同步)
  - [3.1. 事件控制块ECB](#31-事件控制块ecb)
  - [3.2. 任务和ISR之间的通信方式](#32-任务和isr之间的通信方式)
  - [3.3. 等待任务列列表](#33-等待任务列列表)
  - [3.4. 使任务进⼊入/脱离等待状态](#34-使任务进⼊入脱离等待状态)
  - [3.5. 在等待事件的任务列列表中查找优先级最高的](#35-在等待事件的任务列列表中查找优先级最高的)
  - [3.6. 空闲ECB的管理](#36-空闲ecb的管理)
  - [3.7. ECB的基本操作](#37-ecb的基本操作)
  - [3.8. 同步与互斥](#38-同步与互斥)
  - [3.9. μC/OS-II中开关中断的方法](#39-μcos-ii中开关中断的方法)
  - [3.10. μC/OS-II中采用了3种开关中断的方法](#310-μcos-ii中采用了3种开关中断的方法)
  - [3.11. 信号量](#311-信号量)
  - [3.12. 任务、ISR和信号量的关系](#312-任务isr和信号量的关系)
    - [3.12.1. 创建一个信号量](#3121-创建一个信号量)
  - [3.13. 无等待地请求一个信号量](#313-无等待地请求一个信号量)
  - [3.14. 查询一个信号量的当前状态](#314-查询一个信号量的当前状态)
  - [3.15. 任务间通信](#315-任务间通信)
  - [3.16. 共享内存](#316-共享内存)
  - [3.17. 消息邮箱](#317-消息邮箱)
  - [3.18. 任务、ISR和消息邮箱的关系](#318-任务isr和消息邮箱的关系)
  - [3.19. 邮箱的系统服务](#319-邮箱的系统服务)
  - [3.20. 消息队列](#320-消息队列)
  - [3.21. 消息队列列的体系结构](#321-消息队列列的体系结构)
  - [3.22. 队列列控制块](#322-队列列控制块)
  - [3.23. 空闲队列控制块的管理](#323-空闲队列控制块的管理)
  - [3.24. 消息缓冲区](#324-消息缓冲区)
  - [3.25. 创建一个消息队列列](#325-创建一个消息队列列)
  - [3.26. 队列列控制块与事件控制块](#326-队列列控制块与事件控制块)
  - [3.27. 请求消息队列列中的消息](#327-请求消息队列列中的消息)
  - [3.28. 向消息队列列发送一个消息](#328-向消息队列列发送一个消息)
  - [3.29. 清空操作与查询操作](#329-清空操作与查询操作)
- [4. 存储管理](#4-存储管理)
  - [4.1. 概述](#41-概述)
  - [4.2. malloc/free？](#42-mallocfree)
  - [4.3. μC/OS中的存储管理理](#43-μcos中的存储管理理)
  - [4.4. 内存控制块](#44-内存控制块)
  - [4.5. 内存管理初始化](#45-内存管理初始化)
  - [4.6. 创建一个内存分区](#46-创建一个内存分区)
  - [4.7. 分配一个内存块](#47-分配一个内存块)
  - [4.8. 释放一个内存块](#48-释放一个内存块)
  - [4.9. 等待一个内存块](#49-等待一个内存块)
  - [4.10. freertos内存管理理](#410-freertos内存管理理)
  - [4.11. Heap_1.c](#411-heap_1c)
  - [4.12. Heap_2.c](#412-heap_2c)
  - [4.13. Heap_3.c](#413-heap_3c)

<!-- /TOC -->

# 1. 任务管理

## 1.1. 任务主函数
> 开源代码用来学习是可以的，但是如果要商用，则需要获取到开源代码所有者的商业许可。

```c++
void YourTask (void *pdata) {
  for (;;) {
    /* USER CODE
    Call one of uC/OS-II's services:
    OSFlagPend();
    OSMboxPend();
    OSMutexPend();
    OSQPend();
    OSSemPend();
    OSTaskSuspend(OS_PRIO_SELF);
    OSTimeDly();
    OSTimeDlyHMSM();
    /* USER CODE */
  }
}
  // 或者是
void YourTask (void *pdata) {
  /* USER CODE */
  OSTaskDel(OS_PRIO_SELF);
}
```

## 1.2. 任务优先级
1. μC/OS-II最多可以管理64个任务
2. 尽管μC/OS-II保留了四个最高优先级任务和四个最低优先级任务供自己使用。但是，此时，μC/OS-II实际上仅使用两个优先级：OSTaskCreate和OS_LOWEST_PRIO-1(请参阅OS_CFG.H)。这使您最多可以执行56个应用程序任务。
3. 优先级的值越小，任务的优先级越高。
4. 在当前版本的μC/ OS-II中，任务优先级编号也用作任务标识符。
5. 任务优先级一致怎么办：
   1. 时间片流转:先使用一定的时间片完成，然后将结果给下一个使用
   2. 先到先服务

## 1.3. 空闲任务和统计任务
1. 内核总是创建一个空闲任务OSTaskIdle()
   1. 总是设置为最低优先级，OS_LOWEST_PRIOR
   2. 当所有其他任务都未在执行时，空闲任务开始执行
   3. 应用程序不能删除该任务；
   4. 空闲任务的工作就是把32位计数器OSIdleCtr加1，该计数器被统计任务所使用；
2. 统计任务OSTaskStat()，提供运行时间统计。每秒钟运⾏一次，计算当前的CPU利⽤率。其优先级是OS_LOWEST_PRIOR-1，可选。

## 1.4. 任务控制块TCB
1. 任务控制块 OS_TCB是描述⼀个任务的核⼼数据结构，存放了任务的各种管理信息，包括任务堆栈指针，任务的状态、优先级，任务链表指针等；
2. ⼀旦任务建⽴了，任务控制块OS_TCB将被赋值。

```c++
typedef struct os_tcb
{
  //栈指针；
  //INT16U OSTCBId; /*任务的ID*/
  //链表指针；
  //OS_EVENT *OSTCBEventPtr; /*事件指针*/
  //void *OSTCBMsg; /*消息指针*/
  //INT8U OSTCBStat; /*任务的状态*/
  //INT8U OSTCBPrio; /*任务的优先级*/
  //其他……
} OS_TCB;
```

## 1.5. 栈指针
1. OSTCBStkPtr：指向当前任务栈顶的指针，每个任务可以有自己的栈，栈的容量可以是任意的；
2. OSTCBStkBottom：指向任务栈底的指针；
3. OSTCBStkSize：栈的容量，用可容纳的指针数目而不是字节数(Byte)来表⽰。

## 1.6. 链表指针
1. 所有的任务控制块分属于两条不同的链表，单向的空闲链表(头指针为OSTCBFreeList)和双向的使用链表(头指针为OSTCBList)；
2. OSTCBNext、OSTCBPrev：⽤于将任务控制块插⼊到空闲链表或使⽤链表中。每个任务的任务控制块在任务创建的时候被链接到使⽤链表中，在任务删除的时候从链表中被删除。双向连接的链表使得任⼀成员都能快速插⼊或删除。

## 1.7. 空闲TCB链表
1. 所有的任务控制块都被放置在任务控制块列表数组OSTCBTbl[]中，系统初始化时，所有TCB被链接成空闲的单向链表，头指针为OSTCBFreeList。当创建⼀个任务后，就把OSTCBFreeList所指向的TCB赋给了该任务，并将它加⼊到使⽤链表中，然后把OSTCBFreeList指向空闲链表中的下一个结点。
2. 为什么空闲是单项链表，使用是双项链表？因为双向链表有利于将时间复杂度降低为常数。
   1. 遍历链表的时间复杂度是O(n)
   2. 期望遍历复杂度是O(1)，常数，开辟一个数据存放所有任务和TCB地址
   3. 用空间换时间

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/1.png)

## 1.8. 指针数组(指向相应TCB)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/2.png)

## 1.9. 状态的转换
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/3.png)

## 1.10. 任务就绪表
1. 每个任务的就绪态标志放⼊在就绪表中，就绪表中有两个变量OSRdyGrp和OSRdyTbl[]。
2. 在OSRdyGrp中，任务按优先级分组，8个任务为⼀组。OSRdyGrp中的每⼀位表⽰8组任务中每⼀组中是否有进⼊就绪态的任务。任务进⼊就绪态时，就绪表OSRdyTbl[]中的相应元素的相应位也置位。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/4.png)

- (0, 0)是优先级最高的任务，(7, 7)是优先级最低的

### 1.10.1. 根据优先级确定就绪表
1. 假设优先级为12(优先级为0)的任务进⼊就绪状态，12=1100b,则OSRdyTbl[1]的第4位置1，且OSRdyGrp的第1位置1，相应的数学表达式为: 
   1. `OSRdyGrp |= 0x02`
   2. `OSRdyTbl[1] |= 0x10`
2. ⽽优先级为21的任务就绪21=10 101b，则OSRdyTbl[2]的第5位置1，且OSRdyGrp的第2位置1,相应的数学表达式
   1. `OSRdyGrp |= 0x04`
   2. `OSRdyTbl[2] |= 0x20`
3. 从上⾯的计算可知: 若OSRdyGrp及OSRdyTbl[] 的第n位置1，则应该把OSRdyGrp及`OSRdyTbl[]`的值与$2^n$相或。uC/OS中，把$2^n$的n=0-7的8个值先计算好存在数组OSMapTbl`[7]`中,也就是：
   1. OSMapTbl[0] = $2^0$ = 0x01(0000 0001)
   2. OSMapTbl[1] = $2^1$ = 0x02(0000 0010)
   3. OSMapTbl[7] = $2^7$ = 0x80(1000 0000)
4. 如果prio是任务的优先级，即任务的标识号，则将任务放⼊就绪表，使任务进入就绪态的⽅法是：
   1. `OSRdyGrp |= OSMapTbl[prio>>3]`
   2. `OSRdyTbl[prio>>3] |= OSMapTbl[prio&0x07]`
5. 假设优先级为12:1100b
   1. `OSRdyGrp |= OSMapTbl[12>>3](0x02)`
   2. `OSRdyTbl[1] |= 0x10`

### 1.10.2. 使任务脱离就绪态
1. 将任务就绪表OSRdyTbl[prio>>3]相应元素的相应位清零，⽽且当OSRdyTbl[prio>>3]中的所有位都为零时，即该任务所在组的所有任务中没有⼀个进⼊就绪态时，OSRdyGrp的相应位才为零：`if((OSRdyTbl[prio>>3] &= ~OSMapTbl[prio&0x07]) == 0) OSRdyGrp &= ~OSMapTbl[prio>>3];`

## 1.11. 任务的调度
1. μC/OS-II是可抢占实时多任务内核，它总是运⾏就绪任务中优先级最⾼的那⼀个。
2. μC/OS-II中不⽀持时间⽚轮转法，每个任务的优先级要求不⼀样且是唯⼀的，所以任务调度的⼯作就是：查找准备就绪的最⾼优先级的任务并进⾏上下⽂切换。
3. μC/OS-II任务调度所花的时间为常数，与应⽤程序中建⽴的任务数⽆关。
4. 确定哪个任务的优先级最⾼，应该选择哪个任务去运⾏，这部分的⼯作是由调度器(Scheduler)来完成的。
   1. 任务级的调度是由函数OSSched()完成的；
   2. 中断级的调度是由另⼀个函数OSIntExt()完成的。

## 1.12. 根据就绪表确定最高优先级(为什么右移三位)
1. 两个关键:
   1. 将优先级数分解为高三位和低三位分别确定；
   2. 高优先级有着小的优先级号
2. 根据就绪表确定最高优先级
   1. 通过OSRdyGrp值确定⾼3位，假设OSRdyGrp＝0x08=0x00001000，第3位为1，优先级的⾼3位为011;
   2. 通过OSRdyTbl[3]的值来确定低3位，假设OSRdyTbl[3]＝0x3a，第1位为1，优先级的低3位为001，3*8+2-1=25

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/5.png)

## 1.13. 任务调度器
```c++
void OSSched (void){
  INT8U y;
  OS_ENTER_CRITICAL();
  // 检查是否中断调⽤和允许任务调⽤
  if ((OSLockNesting | OSIntNesting) == 0) {
    y = OSUnMapTbl[OSRdyGrp];
    // 找到优先级最⾼的任务
    OSPrioHighRdy = (INT8U)((y << 3) + OSUnMapTbl[OSRdyTbl[y]]);
    // 该任务是否正在运行
    if (OSPrioHighRdy != OSPrioCur) {
      OSTCBHighRdy=OSTCBPrioTbl[OSPrioHighRdy];
      OSCtxSwCtr++;
      OS_TASK_SW();
    }
  }
  OS_EXIT_CRITICAL();
}
```

## 1.14. 源代码中使用了查表法
1. 查表法具有确定的时间，增加了系统的可预测性，uC/OS中所有的系统调用时间都是确定的
   1. `Y = OSUnMapTbl[OSRdyGrp]`
   2. `X = OSUnMapTbl[OSRdyTbl[Y]]`
   3. `Prio = (Y<<3) + X;`

## 1.15. 优先级判定表OSUnMapTbl[256]

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/6.png)

- $2^8 = 256$:一共有256种情况，查表解释即可
- 空间换时间，用来快速查找当前优先级最高的部分

## 1.16. 从64->256
```c++
static void OS_SchedNew (void)
{
#if OS_LOWEST_PRIO <= 63//μC/OS-II v2.7之前⽅式
  INT8U y;
  y = OSUnMapTbl[OSRdyGrp];
  OSPrioHighRdy = (INT8U)((y << 3) + OSUnMapTbl[OSRdyTbl[y]]);
#else
  INT8U y;
  INT16U *ptbl;
  //OSRdyGrp为16位
  if ((OSRdyGrp & 0xFF) != 0) {
    y = OSUnMapTbl[OSRdyGrp & 0xFF];
  } else {
    y = OSUnMapTbl[(OSRdyGrp >> 8) & 0xFF] + 8;//矩形组号y>=8
  }
  ptbl = &OSRdyTbl[y];//取出x方向的16bit数据
  if ((*ptbl & 0xFF) != 0) {
    OSPrioHighRdy = (INT8U)((y << 4) + OSUnMapTbl[(*ptbl & 0xFF)]);//*16
  }
  else {
    OSPrioHighRdy = (INT8U)((y << 4) + OSUnMapTbl[(*ptbl >> 8) & 0xFF] + 8);
  }
#endif
}
```

1. 未超过64位，则用上面的，如果超过了64位则使用下半部分
2. 仔细分析一下:判定低八位是否为0，如果低八位不为0，则直接对低八位操作即可，如果低八位为0，则在高八位，所以需要加8

## 1.17. 任务切换
1. 将被挂起任务的寄存器内容⼊栈；
2. 将较高优先级任务的寄存器内容出栈，恢复到硬件寄存器中。

### 1.17.1. 任务级的任务切换OS_TASK_SW()
1. 保护当前任务的现场
2. 恢复新任务的现场
3. 执行中断返回指令
4. 开始执⾏新的任务

| 调用OS_TASK_SW()前的数据结构 | 保存当前CPU寄存器的值 | 重新装入要运行的任务 |
| ---------------------------- | --------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/7.png)          | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/8.png)   | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/9.png)  |

### 1.17.2. 任务切换OS_TASK_SW()的代码
```c++
Void OSCtxSw(void)
{
  //将R1,R2,R3及R4推⼊当前堆栈；
  OSTCBCur->OSTCBStkPtr = SP;
  OSTCBCur = OSTCBHighRdy;
  SP = OSTCBHighRdy->OSTCBSTKPtr;
  //将R4,R3,R2及R1从新堆栈中弹出；
  //执⾏中断返回指令；
}
```

### 1.17.3. 给调度器上锁
1. OSSchedlock()：给调度器上锁函数，用于禁⽌任务调度，保持对CPU的控制权(即使有优先级更⾼的任务进⼊了就绪态)；
2. OSSchedUnlock()：给调度器开锁函数，当任务完成后调用此函数，调度重新得到允许；
3. 当低优先级的任务要发消息给多任务的邮箱、消息队列、信号量时，它不希望⾼优先级的任务在邮箱、队列和信号量还没有得到消息之前就取得了CPU的控制权，此时，可以使用调度器上锁函数。

## 1.18. 任务管理的系统服务
1. 创建任务
2. 删除任务
3. 修改任务的优先级
4. 挂起和恢复任务
5. 获得一个任务的有关信息

### 1.18.1. 创建任务
1. 创建任务的函数
   1. OSTaskCreate();
   2. OSTaskCreateExt();
2. OSTaskCreateExt()是OSTaskCreate()的扩展版本，提供了⼀些附加的功能；
3. 任务可以在多任务调度开始 (即调⽤OSStart()) 之前创建，也可以在其它任务的执⾏过程中被创建。但在OSStart()被调⽤之前，⽤户必须创建⾄少⼀个任务；
4. 不能在中断服务程序(ISR)中创建新任务。

### 1.18.2. OSTaskCreate()

```c++
INT8U OSTaskCreate (
  void (*task)(void *pd), //任务代码指针
  void *pdata, //任务参数指针
  OS_STK *ptos, //任务栈的栈顶指针
  INT8U prio //任务的优先级
);
```

- 返回值
  - OS_NO_ERR：函数调用成功；
  - OS_PRIO_EXIT：任务优先级已经存在；
  - OS_PRIO_INVALID：任务优先级⽆效。

### 1.18.3. OSTaskCreate()的实现过程
1. 任务优先级检查
   1. 该优先级是否在0到OS_LOWSEST_PRIO之间？
   2. 该优先级是否空闲？
2. 调⽤OSTaskStkInit()，创建任务的栈帧
3. 调⽤OSTCBInit()，从空闲的OS_TCB池(即OSTCBFreeList链表)中获得⼀个TCB并初始化其内容，然后把它加⼊到OSTCBList链表的开头，并把它设定为就绪状态
4. 任务个数OSTaskCtr加1
5. 调用用户自定义的函数OSTaskCreateHook()
6. 判断是否需要调度(调用者是正在执行的任务)

### 1.18.4. OSTaskCreateExt()
```c++
INT8U OSTaskCreateExt(
  //前四个参数与OSTaskCreate相同，
  INT16U id, //任务的ID
  OS_STK *pbos, //指向任务栈底的指针
  INT32U stk_size, //栈能容纳的成员数⽬
  void *pext,//指向⽤户附加数据域的指针
  INT16U opt //⼀些选项信息
);
```
- 返回值：与OSTaskCreate()相同。

### 1.18.5. 任务的栈空间
1. 每个任务都有自己的栈空间(Stack)，栈必须声明为OS_STK类型，并且由连续的内存空间组成；
2. 栈空间的分配方法
   1. 静态分配：在编译的时候分配，例如：`static OS_STK MyTaskStack[stack_size];`、`OS_STK MyTaskStack[stack_size];`
   2. 动态分配：在任务运⾏的时候使⽤malloc()函数来动态申请内存空间；

### 1.18.6. 动态分配
```c++
OS_STK *pstk;
pstk = (OS_STK *)malloc(stack_size);
/* 确认malloc()能得到⾜够的内存空间 */
if (pstk != (OS_STK *)0)
{
  // Create the task;
}
```

### 1.18.7. 内存碎片问题
1. 在动态分配中，可能存在内存碎片问题。特别是当用户反复地建立和删除任务时，内存堆中可能会出现⼤量的碎⽚，导致没有⾜够⼤的⼀块连续内存区域可⽤作任务栈，这时malloc()便⽆法成功地为任务分配栈空间。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/10.png)

### 1.18.8. 栈的增长方向
1. 栈的增长方向的设置
   1. 从低地址到⾼地址：在OS_CPU.H中，将常量OS_STK_GROWTH设定为 0；
   2. 从⾼地址到低地址：在OS_CPU.H中，将常量OS_STK_GROWTH设定为 1；
   3. `OS_STK TaskStack[TASK_STACK_SIZE]`;
   4. `OSTaskCreate(task, pdata,&TaskStack[TASK_STACK_SIZE-1],prio)`;

## 1.19. 删除任务
1. OSTaskDel()：删除一个任务，其TCB会从所有可能的系统数据结构中移除。任务将返回并处于休眠状态(任务的代码还在)。
   1. 如果任务正处于就绪状态，把它从就绪表中移出，这样以后就不会再被调度执⾏了；
   2. 如果任务正处于邮箱、消息队列或信号量的等待队列中，也把它移出；
   3. 将任务的OS_TCB从OSTCBList链表当中移动到OSTCBFreeList。
2. 任务也可以自我删除(并⾮真的删除，只是内核不再知道该任务)
```c++
void MyTask (void *pdata)
{
  ...... /* ⽤户代码 */
  OSTaskDel(OS_PRIO_SELF);
}
```

- OSTaskChangePrio()：在程序运⾏期间，⽤户可以通过调⽤本函数来改变某个任务的优先级。`INT8U OSTaskChangePrio(INT8U oldprio, INT8U newprio)`
- OSTaskQuery()：获得⼀个任务的有关信息:获得的是对应任务的OS_TCB中内容的拷贝。

## 1.20. 挂起和恢复任务
1. OSTaskSuspend()：挂起⼀个任务
   1. 如果任务处于就绪态，把它从就绪表中移出；
   2. 在任务的TCB中设置OS_STAT_SUSPEND标志，表明该任务正在被挂起。
2. OSTaskResume()：恢复⼀个任务
   1. 恢复被OSTaskSuspend()挂起的任务；
   2. 清除TCB中OSTCBStat字段的OS_STAT_SUSPEND位

# 2. 中断和时间管理

## 2.1. 中断处理
1. 中断：由于某种事件的发生而导致程序流程的改变。产生中断的事件称为中断源。
2. CPU响应中断的条件：
   1. ⾄少有⼀个中断源向CPU发出中断信号；
   2. 系统允许中断，且对此中断信号未予屏蔽。

## 2.2. 中断服务程序ISR
1. 中断⼀旦被识别，CPU会保存部分(或全部)运⾏上下⽂(context，即寄存器的值)，然后跳转到专门的⼦程序去处理此次事件，称为中断服务⼦程序(ISR)。
2. μC/OS-Ⅱ中，中断服务⼦程序要⽤汇编语⾔来编写，然⽽，如果⽤户使⽤的C语⾔编译器⽀持在线汇编语⾔的话，⽤户可以直接将中断服务⼦程序代码放在C语⾔的程序⽂件中。

## 2.3. 用户ISR的框架
1. 保存全部CPU寄存器的值;
2. 调⽤OSIntEnter()，或直接把全局变量OSIntNesting
(中断嵌套层次)加1；
3. 执⾏⽤户代码做中断服务;
4. 调⽤OSIntExit()；
5. 恢复所有CPU寄存器；
6. 执⾏中断返回指令。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/11.png)

### 2.3.1. OSIntEnter()
```c++
/* 在调⽤本函数之前必须先将中断关闭 */
void OSIntEnter (void){
  if (OSRunning == TRUE) {
      if (OSIntNesting < 255) {
         OSIntNesting++;
      }
  }
}
```

### 2.3.2. OSIntExit()
```c++
void OSIntExit (void)
{
  OS_ENTER_CRITICAL(); //关中断
  if ((--OSIntNesting|OSLockNesting) == 0) //判断嵌套是否为零
  { //把⾼优先级任务装⼊
    OSIntExitY = OSUnMapTbl[OSRdyGrp];
    OSPrioHighRdy=(INT8U)((OSIntExitY<< 3) +
    OSUnMapTbl[OSRdyTbl[OSIntExitY]]);
    if (OSPrioHighRdy != OSPrioCur) {
      OSTCBHighRdy = OSTCBPrioTbl[OSPrioHighRdy];
      OSCtxSwCtr++;
      OSIntCtxSw();
    }
  }
  OS_EXIT_CRITICAL(); //开中断返回
}
```

### 2.3.3. OSIntCtxSw()
1. 在任务切换时，为什么使⽤OSIntCtxSw()⽽不是调度函数中的OS_TASK_SW()？
2. 原因如下：
   1. 一半的任务切换工作，即CPU寄存器入栈，已经在前面做完了；
   2. 需要保证所有被挂起任务的栈结构是一样的。

### 2.3.4. 调用中断切换函数OSIntCtxSw() 后的堆栈情况
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/12.png)

## 2.4. 时钟节拍
1. 时钟节拍是⼀种特殊的中断；
2. μC/OS需要⽤户提供周期性信号源，⽤于实现时间延时和确认超时。节拍率应在10到100Hz之间，时钟节拍率越⾼，系统的额外负荷就越重；
3. 时钟节拍的实际频率取决于⽤户应⽤程序的精度。时钟节拍源可以是专门的硬件定时器，或是来⾃50/60Hz交流电源的信号。

### 2.4.1. 时钟节拍ISR
```c++
void OSTickISR(void){
  //(1)保存处理器寄存器的值；
  //(2)调⽤OSIntEnter()或将OSIntNesting加1;
  //(3)调⽤OSTimeTick(); /*检查每个任务的时间延时*/
  //(4)调⽤OSIntExit();
  //(5)恢复处理器寄存器的值;
  //(6)执⾏中断返回指令;
｝
```

### 2.4.2. 时钟节拍函数 OSTimetick()
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/13.png)

## 2.5. 时间管理
1. 与时间管理相关的系统服务:
   1. OSTimeDLY()
   2. OSTimeDLYHMSM()
   3. OSTimeDlyResume()
   4. OSTimeGet()
   5. OSTimeSet()

### 2.5.1. OSTimeDLY()
1. OSTimeDLY()：任务延时函数，申请该服务的任务可以延时⼀段时间；
2. 调⽤OSTimeDLY后，任务进⼊等待状态；
3. 使⽤⽅法
   1. void OSTimeDly (INT16U ticks);
   2. ticks表⽰需要延时的时间长度，⽤时钟节拍的个数
来表⽰。

```c++
void OSTimeDly (INT16U ticks){
  if (ticks > 0){
    OS_ENTER_CRITICAL();
    if ((OSRdyTbl[OSTCBCur->OSTCBY] &=
    ~OSTCBCur->OSTCBBitX) == 0){
      OSRdyGrp &= ~OSTCBCur->OSTCBBitY;
    }
    OSTCBCur->OSTCBDly = ticks;
    OS_EXIT_CRITICAL();
    OSSched();
  }
}
```

### 2.5.2. 问题

|                      |                      |                      |
| -------------------- | -------------------- | -------------------- |
| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/14.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/15.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/16.png) |

> 这个问题是指，对于一个OSTimeDly()操作而言，其实我们是不能严格延迟一个时间周期的，因为可能出现高优先级的事务，最好是OSTimeDLY(2)，同样对于OSRTimeDly(1)而言，其实严格意义上的dly时间是不确定的(抖动)。

### 2.5.3. 解决方案
1. 增加微处理器的时钟频率
2. 增加时钟节拍的频率
3. 重新安排任务的优先级
4. 避免使用浮点运算(如果非使用不可,尽量用单精度数)
5. 使⽤能较好地优化程序代码的编译器
6. 时间要求苛刻的代码用汇编语言写
7. 如果可能,⽤同⼀家族的更快的微处理器做系统升级。如从8086向80186升级, 从68000向68020升级等
8. 不管怎么样，抖动总是存在的

### 2.5.4. OSTimeDlyHMSM()
1. OSTimeDlyHMSM()：OSTimeDly()的另⼀个版本，即按时分秒延时函数；
2. 使⽤⽅法
```c++
INT8U OSTimeDlyHMSM(
  INT8U hours, // ⼩时
  INT8U minutes, // 分钟
  INT8U seconds, // 秒
  INT16U milli // 毫秒
);
```

### 2.5.5. OSTimeDlyResume()
1. OSTimeDlyResume()：让处在延时期的任务提前结束延时，进⼊就绪状态；
2. 使⽤⽅法
   1. INT8U OSTimeDlyResume (INT8U prio);
   2. prio表⽰需要提前结束延时的任务的优先级/任务ID。

### 2.5.6. 系统时间
1. 每隔⼀个时钟节拍，发⽣⼀个时钟中断，将⼀个32位的计数器OSTime加1；
2. 该计数器在⽤户调⽤OSStart()初始化多任务和4,294,967,295个节拍执⾏完⼀遍的时候从0开始计数。若时钟节拍的频率等于100Hz，该计数器每隔497天就重新开始计数；
3. OSTimeGet()：获得该计数器的当前值；INT32U OSTimeGet (void);
4. OSTimeSet()：设置该计数器的值；void OSTimeSet (INT32U ticks);

### 2.5.7. 何时启动系统定时器
1. 如果在OSStart之前启动定时器，则系统可能⽆法正确执⾏完OSStartHighRdy
2. OSStart函数直接调⽤OSStartHighRdy去执⾏最⾼优先级的任务，OSStart不返回
3. 系统定时器应该在系统的最⾼优先级任务中启动
4. 使⽤OSRunning变量来控制操作系统的运⾏

### 2.5.8. 时钟节拍的启动
1. **用户必须在多任务系统启动以后再开启时钟节拍器，也就是调用OSStart()之后**
2. 在调⽤OSStart()之后做的第⼀件事是初始化定时器中断
```c++
void main(void)
{
  OSInit(); /* 初始化uC/OS-II*/
  /* 应⽤程序初始化代码... */
  /* 调⽤OSTaskCreate()创建⾄少⼀个任务*/
  //允许时钟节拍中断; /* 错误！可能crash!*/
  OSStart(); /* 开始多任务调度 */
}
```

### 2.5.9. 系统的初始化与启动
1. 在调⽤μC/OS-II的任何其它服务之前，用户必须首先调用系统初始化函数OSInit()来初始化μC/OS的所有变量和数据结构；
2. OSInit()建立空闲任务OSTaskIdle()，该任务总是处于就绪状态，其优先级⼀般被设成最低，即OS_LOWEST_PRIO；如果需要，OSInit()还建⽴统计任务OSTaskStat()，并让其进⼊就绪状态；
3. OSInit()还初始化了4个空数据结构缓冲区：空闲TCB链表OSTCBFreeList、空闲事件链表OSEventFreeList、空闲队列链表OSQFreeList和空闲存储链表OSMemFreeList。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/17.png)

## 2.6. μC/OS-II的启动
1. 多任务的启动是⽤户通过调⽤OSStart()实现的。然⽽，启动μC/OS-Ⅱ之前，⽤户⾄少要建⽴⼀个应⽤任务。

```c++
void main (void)
{
  OSInit(); /* 初始化uC/OS-II */
  ...
  通过调⽤OSTaskCreate()或OSTaskCreateExt()
  创建⾄少⼀个任务;
  ...
  OSStart(); /*开始多任务调度! 永不返回*/
}
```

### 2.6.1. OSStart()
```c++
void OSStart (void)
{
  INT8U Y;
  INT8U X;
  if (OSRunning == FALSE) {
      y = OSUnMapTbl[OSRdyGrp];
      x = OSUnMapTbl[OSRdyTbl[y]];
      OSPrioHighRdy = (INT8U)((Y<<3) + X);
      OSPrioCur = OSPrioHighRdy;
      OSTCBHighRdy = OSTCBPrioTbl[OSPrioHighRdy];
      OSTCBCur = OSTCBHighRdy;
      OSStartHighRdy();
  }
}
```

### 2.6.2. 统计任务初始化函数 OSStatInit (void)
```c++
void OSStatInit (void){
  OSTimeDly(2);
  OS_ENTER_CRITICAL();
  OSIdleCtr = 0L;
  OS_EXIT_CRITICAL();
  OSTimeDly(OS_TICKS_PER_SEC);
  OS_ENTER_CRITICAL();
  OSIdleCtrMax = OSIdleCtr;
  OSStatRdy = TRUE;
  OS_EXIT_CRITICAL();
}
```
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/18.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/19.png)

# 3. 任务之间的通信与同步
1. 任务间通信的管理：事件控制块ECB
2. 同步与互斥
   1. 临界区(Critical Sections)
   2. 信号量(Semaphores)
3. 任务间通信
   1. 邮箱(Message Mailboxes)
   2. 消息队列(Message Queues)

## 3.1. 事件控制块ECB
1. 所有的通信信号都被看成是事件(event), μC/OS-II通过
事件控制块(ECB)来管理每⼀个具体事件。

```c++
// ECB数据结构
typedef struct {
  void *OSEventPtr; /*指向消息或消息队列列的指针*/
  INT8U OSEventTbl[OS_EVENT_TBL_SIZE];//等待任务列列表
  INT16U OSEventCnt; /*计数器器(当事件是信号量量时)*/
  INT8U OSEventType; /*事件类型：信号量量、邮箱等*/
  INT8U OSEventGrp; /*等待任务组*/
} OS_EVENT;
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/20.png)

## 3.2. 任务和ISR之间的通信方式
1. 一个任务或ISR可以通过事件控制块ECB(信号量、邮箱或消息队列)向另外的任务发信号；
2. 一个任务还可以等待另一个任务或中断服务子程序给它发送信号。对于处于等待状态的任务，还可以给他指定一个最长等待时间。
3. 多个任务可以同时等待同一个事件的发生。当该事件发⽣后，在所有等待该事件的任务中，优先级最高的任务得到了该事件并进⼊就绪状态，准备执⾏。

## 3.3. 等待任务列列表
1. 每个正在等待某个事件的任务被加⼊到该事件的ECB的等待任务列表中，该列表包含两个变量OSEventGrp和OSEventTbl[]。
2. 在OSEventGrp中，任务按优先级分组，8个任务为⼀组，共8组，分别对应OSEventGrp 当中的8位。当某组中有任务处于等待该事件的状态时，对应的位就被置位。同时， OSEventTbl[]中的相应位也被置位。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/21.png)

## 3.4. 使任务进⼊入/脱离等待状态
1. 将⼀个任务插⼊到事件的等待任务列表中

```c++
pevent->OSEventGrp |= OSMapTbl[prio >> 3];
pevent->OSEventTbl[prio >> 3] |= OSMapTbl[prio & 0x07];
```

2. 从等待任务列表中删除⼀个任务

```c++
if ((pevent->OSEventTbl[prio >> 3] &= ~OSMapTbl[prio & 0x07]) == 0) {
   pevent->OSEventGrp &= ~OSMapTbl[prio >> 3];
}
```

## 3.5. 在等待事件的任务列列表中查找优先级最高的
1. 在等待任务列表中查找最高优先级的任务

```c++
y = OSUnMapTbl[pevent->OSEventGrp];
x = OSUnMapTbl[pevent->OSEventTbl[y]];
prio = (y << 3) + x;
```

## 3.6. 空闲ECB的管理
1. ECB的总数由⽤户所需要的信号量、邮箱和消息队列的总数决定，由OS_CFG.H中的#define OS_MAX_EVENTS定义。
2. 在调⽤OSInit()初始化系统时，所有的ECB被链接成⼀个单向链表——空闲事件控制块链表；
3. 每当建⽴⼀个信号量、邮箱或消息队列时，就从该链表中取出⼀个空闲事件控制块，并对它进⾏初始化。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/22.png)

## 3.7. ECB的基本操作
1. OSEventWaitListInit()
   1. 初始化⼀个事件控制块。当创建⼀个信号量、邮箱或消息队列时，相应的创建函数会调⽤本函数对ECB的内容进⾏初始化，将OSEventGrp和OSEventTbl[]数组清零；
   2. OSEventWaitListInit (OS_EVENT *pevent)；
   3. pevent：指向需要初始化的事件控制块的指针。
2. OSEventTaskRdy()。
   1. 使⼀个任务进⼊就绪态。当⼀个事件发⽣时，需要将其等待任务列表中的最⾼优先级任务置为就绪态；
   2. OSEventTaskRdy (OS_EVENT *pevent, void *msg, INT8U msk)；
   3. msg：指向消息的指针；msk：⽤于设置TCB的状态。
3. OSEventTaskWait()
   1. 使⼀个任务进⼊等待状态。当某个任务要等待⼀个事件的发⽣时，需要调⽤本函数将该任务从就绪任务表中删除，并放到相应事件的等待任务表中；
   2. OSEventTaskWait (OS_EVENT *pevent)；

## 3.8. 同步与互斥
1. 为了实现资源共享，⼀个操作系统必须提供临界区操作的功能；
2. μC/OS采⽤关闭/打开中断的⽅式来处理临界区代码，从⽽避免竞争条件，实现任务间的互斥；
3. μC/OS定义两个宏(macros)来开关中断，即：OS_ENTER_CRITICAL()和OS_EXIT_CRITICAL()；
4. 这两个宏的定义取决于所⽤的微处理器，每种微处理器都有⾃⼰的OS_CPU.H⽂件。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/23.png)

## 3.9. μC/OS-II中开关中断的方法
1. 当处理临界段代码时，需要关中断，处理完毕后，再开中断；
2. 关中断时间是实时内核最重要的指标之一；
3. 在实际应用中，关中断的时间很大程度中取决于微处理器的结构和编译器生成的代码质量；

## 3.10. μC/OS-II中采用了3种开关中断的方法
1. OS_CRITICAL_METHOD==1
   1. 用处理器指令关中断，执⾏OS_ENTER_CRITICAL()，开中断执⾏OS_EXIT_CRITICAL()；
2. OS_CRITICAL_METHOD==2
   1. 实现OS_ENTER_CRITICAL()时，先在堆栈中保存中断的开/关状态，然后再关中断；实现OS_EXIT_CRITICAL()时，从堆栈中弹出原来中断的开/关状态；
3. OS_CRITICAL_METHOD==3
   1. 把当前处理器的状态字保存在局部变量中(如OS_CPU_SR)，关中断时保存，开中断时恢复

## 3.11. 信号量
1. 信号量在多任务系统中的功能
   1. 实现对共享资源的互斥访问(包括单个共享资源或多个相同的资源)；
   2. 实现任务之间的⾏为同步；
2. 必须在OS_CFG.H中将OS_SEM_EN开关常量置为1，这样μC/OS才能⽀持信号量。
3. uC/OS中信号量由两部分组成：信号量的计数值(16位⽆符号整数)和等待该信号量的任务所组成的等待任务表；
4. 信号量系统服务
   1. OSSemCreate()
   2. OSSemPend(), OSSemPost()
   3. OSSemAccept(), OSSemQuery()

## 3.12. 任务、ISR和信号量的关系
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/24.png)

### 3.12.1. 创建一个信号量
1. OSSemCreate()
   1. 创建⼀个信号量，并对信号量的初始计数值赋值，该初始值为0到65,535之间的⼀个数；
   2. OS_EVENT *OSSemCreate(INT16U cnt);
   3. cnt：信号量的初始值。
2. 执行步骤
   1. 从空闲事件控制块链表中得到⼀个ECB；
   2. 初始化ECB，包括设置信号量的初始值、把等待任务列表清零、设置ECB的事件类型等；
   3. 返回⼀个指向该事件控制块的指针。
3. OSSemPend()
   1. 等待⼀个信号量，即操作系统中的P操作，将信号量的值减1；
   2. `OSSemPend (OS_EVENT *pevent, INT16U timeout, INT8U *err);`
4. 执⾏步骤
   1. 如果信号量的计数值⼤于0，将它减1并返回；
   2. 如果信号量的值等于0，则调⽤本函数的任务将被阻塞起来，等待另⼀个任务把它唤醒
   3. 调⽤OSSched()函数，调度下⼀个最⾼优先级的任务运⾏。
5. OSSemPost()
   1. 发送⼀个信号量，即操作系统中的V操作，将信号量的值加1；
   2. OSSemPost (OS_EVENT *pevent);
6. 执⾏步骤
   1. 检查是否有任务在等待该信号量，如果没有，将信号量的计数值加1并返回；
   2. 如果有，将优先级最⾼的任务从等待任务列表中删除，并使它进⼊就绪状态；
   3. 调⽤OSSched()，判断是否需要进⾏任务切换。

## 3.13. 无等待地请求一个信号量
1. OSSemAccept()
   1. 当⼀个任务请求⼀个信号量时，如果该信号量暂时⽆效，则让该任务简单地返回，⽽不是进⼊等待状态；
   2. INT16U OSSemAccept(OS_EVENT *pevent);
2. 执⾏步骤
   1. 如果该信号量的计数值⼤于0，则将它减1，然后将信号量的原有值返回；
   2. 如果该信号量的值等于0，直接返回该值(0)。

## 3.14. 查询一个信号量的当前状态
1. OSSemQuery()
   1. 查询⼀个信号量的当前状态；
   2. INT8U OSSemQuery(OS_EVENT *pevent,OS_SEM_DATA *pdata);
   3. 将指向信号量对应事件控制块的指针pevent所指向的ECB的内容拷贝到指向⽤于记录信号量信息的数据结构OS_SEM_DATA数据结构的指针pdata所指向的缓冲区当中。

## 3.15. 任务间通信
1. 低级通信
   1. 只能传递状态和整数值等控制信息，传送的信息量⼩；
   2. 例如：信号量
2. ⾼级通信
   1. 能够传送任意数量的数据；
   2. 例如：共享内存、邮箱、消息队列

## 3.16. 共享内存
1. 在μC/OS-II中如何实现共享内存？
   1. 内存地址空间只有⼀个，为所有的任务所共享！
   2. 为了避免竞争状态，需要使⽤信号量来实现互斥访问。

## 3.17. 消息邮箱
1. 邮箱(MailBox)：⼀个任务或ISR可以通过邮箱向另⼀个任务发送⼀个指针型的变量，该指针指向⼀个包含了特定"消息"(message)的数据结构；
2. 必须在OS_CFG.H中将OS_MBOX_EN开关常量置为1，这样μC/OS才能⽀持邮箱。
3. ⼀个邮箱可能处于两种状态：
   1. 满的状态：邮箱包含⼀个⾮空指针型变量；
   2. 空的状态：邮箱的内容为空指针NULL；
4. 邮箱的系统服务
   1. OSMboxCreate()
   2. OSMboxPost()
   3. OSMboxPend()
   4. OSMboxAccept()
   5. OSMboxQuery()

## 3.18. 任务、ISR和消息邮箱的关系
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/25.png)

## 3.19. 邮箱的系统服务
1. OSMboxCreate()：创建⼀个邮箱
   1. 在创建邮箱时，须分配⼀个ECB，并使⽤其中的字段OSEventPtr指针来存放消息的地址；
   2. OS_EVENT *OSMboxCreate(void *msg);
   3. msg：指针的初始值，⼀般情形下为NULL。
2. OSMboxPend()：等待⼀个邮箱中的消息
   1. 若邮箱为满，将其内容(某消息的地址)返回；若邮箱为空，当前任务将被阻塞，直到邮箱中有了消息或等待超时
   2. OSMboxPend (OS_EVENT *pevent,INT16U timeout, INT8U *err);
3. OSMboxPost()：发送⼀个消息到邮箱中
   1. 如果有任务在等待该消息，将其中的最⾼优先级任务从等待列表中删除，变为就绪状态；
   2. OSMboxPost(OS_EVENT *pevent, void *msg);
4. OSMboxAccept()：无等待地请求邮箱内容
   1. 若邮箱为满，返回它的当前内容；若邮箱为空，返回空指针；
   2. OSMboxAccept (OS_EVENT *pevent);
5. OSMboxQuery()：查询⼀个邮箱的状态
   1. OSMboxQuery (OS_EVENT *pevent,OS_MBOX_DATA *pdata)；

## 3.20. 消息队列
1. 消息队列(Message Queue)：消息队列可以使⼀个任务或ISR向另⼀个任务发送多个以指针⽅式定义的变量；
2. 为了使μC/OS能够⽀持消息队列，必须在OS_CFG.H中将OS_Q_EN开关常量置为1，并且通过常量OS_MAX_QS来决定系统⽀持的最多消息队列数。
3. ⼀个消息队列可以容纳多个不同的消息，因此可把它看作是由多个邮箱组成的数组，只是它们共⽤⼀个等待任务列表：
4. 消息队列的系统服务
   1. OSQCreate()
   2. OSQPend()、OSQAccept()
   3. OSQPost()、OSQPostFront()
   4. OSQFlush()
   5. OSQQuery()

## 3.21. 消息队列列的体系结构
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/26.png)

## 3.22. 队列列控制块
1. 队列控制块数据结构
```c++
typedef struct os_q {
   struct os_q *OSQPtr;//空闲队列控制块指针
   void **OSQStart; //指向消息队列的起始地址
   void **OSQEnd; //指向消息队列的结束地址
   void **OSQIn; //指向消息队列中下⼀个插⼊消息的位置
   void **OSQOut;//指向消息队列中下⼀个取出消息的位置
   INT16U OSQSize; //消息队列中总的单元数
   INT16U OSQEntries; //消息队列中当前的消息数量
} OS_EVENT;
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/27.png)

## 3.23. 空闲队列控制块的管理
1. 每⼀个消息队列都要⽤到⼀个队列控制块。在μC/OS中，队列控制块的总数由OS_CFG.H中的常量OS_MAX_QS定义。
2. 在系统初始化时，所有的队列控制块被链接成⼀个单向链表——空闲队列控制块链表OSQFreeList。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/28.png)

## 3.24. 消息缓冲区
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/29.png)

## 3.25. 创建一个消息队列列
1. OSQCreate()
   1. OS_EVENT *OSQCreate (void **start, INT16U size);
   2. start：指针数组，⽤来存放各个消息的地址
   3. size：数组的⼤⼩(即消息队列的元素个数)
2. 执⾏步骤
   1. 从空闲事件控制块链表中取得⼀个ECB；
   2. 从空闲队列控制块列表中取出⼀个队列控制块，并对其进⾏初始化；
   3. 初始化ECB的内容(事件类型、等待任务列表)，并将OSEventPtr指针指向队列控制块。

## 3.26. 队列列控制块与事件控制块
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/30.png)

## 3.27. 请求消息队列列中的消息
1. OSQPend()：等待⼀个消息队列中的消息
   1. void *OSQPend (OS_EVENT *pevent, INT16U timeout, INT8U *err);
   2. 如果消息队列中有⾄少⼀条消息，返回消息的地址；
   3. 如果没有消息，相应任务进⼊等待状态。
2. OSQAccept()：⽆等待地请求消息队列中的消息
   1. void *OSQAccept(OS_EVENT *pevent)；
   2. 如果消息队列中有消息，返回消息的地址；
   3. 如果消息队列中没有消息，返回NULL。

## 3.28. 向消息队列列发送一个消息
1. OSQPost()：以FIFO⽅式向消息队列发送⼀个消息
   1. INT8U OSQPost (OS_EVENT *pevent, void *msg);
   2. 如果有任务在等待该消息队列，唤醒其中优先级最⾼的任务，并重新调度；
   3. 如果没有任务在等待该消息队列，⽽且此时消息队列未满，则以FIFO⽅式插⼊这个消息。
2. OSQPostFront()：以LIFO⽅式向消息队列发送⼀个消息:INT8U OSQPostFront(OS_EVENT *pevent, void *msg)；

## 3.29. 清空操作与查询操作
1. OSQFlush()：清空⼀个消息队列
   1. INT8U OSQFlush (OS_EVENT *pevent);
   2. 删除⼀个消息队列中的所有消息；
2. OSQQuery()：查询⼀个消息队列的状态
   - INT8U OSQQuery (OS_EVENT *pevent,OS_Q_DATA *pdata)；

# 4. 存储管理

## 4.1. 概述
1. μC/OS中是实模式存储管理
   1. 不划分内核空间和⽤户空间，整个系统只有⼀个地址空间，即物理内存空间，应⽤程序和内核程序都能直接对所有的内存单元进⾏访问；
   2. 系统中的"任务"，实际上都是线程–––只有运⾏上下⽂和栈是独享的，其他资源都是共享的。
2. 内存布局:代码段(text)、数据段(data)、bss段、堆空间、栈空间；

## 4.2. malloc/free？
1. 在ANSI C中可以⽤malloc()和free()两个函数动态地分配内存和释放内存。在嵌⼊式实时操作系统中，容易产⽣碎⽚。
2. 由于内存管理算法的原因，malloc()和free()函数执⾏时间是不确定的。μC/OS-II 对malloc()和free()函数进⾏了改进，使得它们可以分配和释放固定⼤⼩的内存块。这样⼀来，malloc()和free()函数的执⾏时间也是固定的了

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/31.png)

## 4.3. μC/OS中的存储管理理
1. μC/OS采⽤的是固定分区的存储管理⽅法
   1. μC/OS把连续的⼤块内存按分区来管理，每个分区包含有整数个⼤⼩相同的块；
   2. 在⼀个系统中可以有多个内存分区，这样，⽤户的应⽤程序就可以从不同的内存分区中得到不同⼤⼩的内存块。但是，特定的内存块在释放时必须重新放回它以前所属于的内存分区；
   3. 采⽤这样的内存管理算法，上⾯的内存碎⽚问题就得到了解决。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/32.png)

## 4.4. 内存控制块
1. 为了便于管理，在μC/OS中使用内存控制块MCB(Memory Control Block)来跟踪每⼀个内存分区，系统中的每个内存分区都有它自己的 MCB。
```c++
typedef struct {
   void *OSMemAddr; /*分区起始地址*/
   void *OSMemFreeList;//下⼀个空闲内存块
   INT32U OSMemBlkSize; /*内存块的⼤⼩*/
   INT32U OSMemNBlks; /*内存块数量*/
   INT32U OSMemNFree; /*空闲内存块数量*/
} OS_MEM;
```

## 4.5. 内存管理初始化
1. 如果要在μC/OS-II中使用内存管理，需要在OS_CFG.H⽂件中将开关量OS_MEM_EN设置为1。这样μC/OS-II 在系统初始化OSInit()时就会调⽤OSMemInit()，对内存管理器进⾏初始化，建⽴空闲的内存控制块链表。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/33.png)

## 4.6. 创建一个内存分区
1. OSMemCreate()

```c++
OS_MEM *OSMemCreate (
void *addr, // 内存分区的起始地址
INT32U nblks, // 分区内的内存块数
INT32U blksize,// 每个内存块的字节数
INT8U *err); // 指向错误码的指针
```
- 例⼦
```
OS_MEM *CommTxBuf;
INT8U CommTxPart[100][32];
CommTxBuf = OSMemCreate(CommTxPart, 100, 32, &err);
```
1. OSMemCreate()
   1. 从系统的空闲内存控制块中取得⼀个MCB；
   2. 将这个内存分区中的所有内存块链接成⼀个单向链表；
   3. 在对应的MCB中填写相应的信息。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/34.png)

## 4.7. 分配一个内存块
1. `void *OSMemGet(OS_MEM *pmem, INT8U *err);`
2. 功能：从已经建⽴的内存分区中申请⼀个内存块。该函数的唯⼀参数是指向特定内存分区的指针。如果没有空闲的内存块可⽤，返回NULL指针。
3. 应⽤程序必须知道内存块的⼤⼩，并且在使⽤时不能超过该容量。

## 4.8. 释放一个内存块
1. INT8U OSMemPut(OS_MEM *pmem, void *pblk);
2. 功能：将⼀个内存块释放并放回到相应的内存分区中。
3. 注意：⽤户应⽤程序必须确认将内存块放回到了正确的内存分区中，因为OSMemPut()并不知道⼀个内存块是属于哪个内存分区的。

## 4.9. 等待一个内存块
1. 如果没有空闲的内存块，OSMemGet()⽴即返回NULL。能否在没有空闲内存块的时候让任务进⼊等待状态？
2. μC/OS-II本⾝在内存管理上并不⽀持这项功能，如果需要的话，可以通过为特定内存分区增加信号量的⽅法，来实现此功能。
3. 基本思路：当应⽤程序需要申请内存块时，⾸先要得到⼀个相应的信号量，然后才能调⽤OSMemGet()函数。

```c++
OS_EVENT *SemaphorePtr;
OS_MEM *PartitionPtr;
INT8U Partition[100][32];
OS_STK TaskStk[1000];
void main(void){
   INT8U err;
   OSInit();
   ...
   SemaphorePtr = OSSemCreate(100);
   PartitionPtr = OSMemCreate(Partition, 100, 32, &err);
   OSTaskCreate(Task, (void *)0, &TaskStk[999], &err);
   OSStart();
}
void Task (void *pdata){
   INT8U err;
   INT8U *pblock;
   for (;;) {
      OSSemPend(SemaphorePtr, 0, &err);
      pblock = OSMemGet(PartitionPtr, &err);
      /* 使⽤内存块 */
      ...
      OSMemPut(PartitionPtr, pblock);
      OSSemPost(SemaphorePtr);
   }
}
```

## 4.10. freertos内存管理理
1. 三种pvPortMalloc()和vPortFree()的实现范例

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/35.png)

## 4.11. Heap_1.c
1. 其实现了⼀个⾮常基本的pvPortMalloc()版本，⽽没有实现vPortFree()。如果应⽤程序不需要删除任务，队列或者信号量，则其具有使⽤heap_1的潜质。其具有确定性。
2. 这种分配⽅案将FreeRTOS的内存堆空间堪称⼀个简单的数组。当调⽤pvPortMalloc()时，则将数组又简单的细分成为更⼩的内存块。数组⼤⼩在FreeRTOSConfig.h中由configTOTAL_HEAP_SIZE定义。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/36.png)

## 4.12. Heap_2.c
1. 其采⽤了⼀个最佳匹配算法来分配内存，并⽀持内存释放。由于声明了⼀个静态数组，所以会让整个应⽤程序看起来耗费了很多内存，即使是在数组没有进⾏任何实际分配之前。
2. 最佳匹配算法保证pvPortMalloc()会使⽤最接近请求⼤⼩的空间块。例如：
   1. 对空间包含了三个空闲内存块，分别为5字节，25字节和100字节。
   2. pvPortMalloc()被调⽤⽤以请求分配20字节⼤⼩的内存空间。
3. Heap_2.c不会把相邻的空闲块合并成⼀个更⼤的内存块，所以会产⽣内存碎⽚如果分配和释放的总是相同⼤⼩的内存块，则内存碎⽚不会称为⼀个问题。所以Heap_2.c适合于那些重复创建与删除具有相同空间任务的应⽤程序。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/lec7/37.png)

## 4.13. Heap_3.c
1. 简单的调⽤了标准库malloc()和free()，但是通过暂时挂起调度器使得函数调⽤具备了线程安全特性。