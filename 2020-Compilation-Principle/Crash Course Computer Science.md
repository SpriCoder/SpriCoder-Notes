Crash Course Computer Science
---

# 1. 第五讲：算数逻辑单元-ALU
1. 计算机目标是计算，有意义的处理数字。
2. ALU负责完成计算，基本其他所有的部件都会用到它。
3. Eg.ALU Intel 74181:1970年发布时，是第一个封装在单个芯片内的完整的ALU，只可以进行4位计算
4. ALU：使用AND、OR、NOT和XOR逻辑门
   1. 1个算术单元：负责所有数字操作，例如增量计算
   2. 1个逻辑单元：计算AND、OR或NOT操作

## 1.1. 算术单元

### 1.1.1. 半加器
1. XOR可以作为一位加法器
2. 1+1是特殊的
3. 我们使用AND来进行检查进位
4. 得到两个门的电路是半加器

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/1.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/2.png)

### 1.1.2. 全加器
1. 增加一个输入(进位)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/3.png)

### 1.1.3. 制作：8位行波加法器
1. overflow：最后一位溢出

### 1.1.4. 超前进位加法器

### 1.1.5. ALU可以做基本操作
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/4.png)

## 1.2. 逻辑单元
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/5.png)

> 检查是否为全0

## 1.3. ALU的代表
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/6.png)

# 2. 寄存器&内存
1. RAM:随机存储器，在有电的时候存储信息
2. 持久存储，电源关闭，数据也不会丢失

## 2.1. 存储1位的单元
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/7.png)

- 永久记录1

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/8.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/9.png)

- 锁存：可以读写

## 2.2. 门锁
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/10.png)

## 2.3. 多位存储
1. 寄存器位宽：可以存储多长数据

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/11.png)

2. 存储256位只需要513根线
3. 使用矩阵，网格存储所有的锁存器，使用仅需要打开对应的行线和列线(使用AND门)，允许我们使用一根数据线进行相应操作。
4. 一共只需要35根线：
   1. 一根数据线
   2. 一根允许写入线
   3. 一根允许读取线
   4. 16行线和16列线
5. 多路复用器：确定行和列的位置
6. 我们使用1-16多路复用器，一个多路复用器给行，一个给列

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/12.png)

## 2.4. 内存特性
1. 内存可以任意访问存储位置.

# 3. CPU
1. 指令指示计算机执行相应操作。
2. 微体系结构
3. 指令表

## 3.1. CPU执行指令
1. 取指令阶段
2. 解码阶段：根据指令表，用电路来检查操作码
3. 执行阶段：最后将指令地址寄存器+1
4. 执行下一条指令

> 讲解了一个加法过程:Control Unit有一个寄存器先存储结果，避免ALU无限加。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/hw1/13.png)

- 时钟来推进操作
- 时钟速度：CPU取指令->解码->执行的速度，动态调整频率(时钟频率)

# 4. 指令和程序
1. 因为可编程，所有CPU是强大的，可以被软件控制的。
2. 将之前的部分翻译成更容易理解的语言。
3. JUMP指令会结合flag位
4. HALT使用区分数据和指令的命令
5. 软件实现了硬件不能实现的部分，比如除法。
6. 为了可以访问更多的操作码
   1. 更多位来表示操作码，比如32位或64位。
   2. 可变长操作码