Hw01-Homework for uC/OS-II
---
1. uC/OS-II的多任务实验

# 1. 固定优先级调度
1. uC/OS-II支持固定优先级调度
2. 易于实施RM

# 2. 周期任务

## 2.1. 调用OSTaskCreate来创建任务
```c++
//A straightforward emulation of (c,p)
while(1){
  Start=OSTimeGet() ;
  While(OStimeGet()-start < c) ;
  OSTimeDly (p-c) ;
}
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/hw01/2.png)

- 问题：如果[开始，结束]之间存在抢占，则任务未获得CPU时间的c个单位

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/hw01/1.png)

- C =任务的时钟滴答花费
- delay = p-(end - start)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/hw01/3.png)

- 使用计时器来计时
```c++
void Task()
{
  int start ; //the start time
  int end ; //the end time
  int toDelay;
  start=0 ;
  while(1) {
    while(OSTCBCur->compTime>0) //C ticks
    {
      // do nothing
    }
    end=OSTimeGet() ; // end time
    toDelay=T-(end-start) ;
    start=start+T ; // next start time
    OSTCBCur->compTime=C ; // reset the counter (c ticks for computation)
    OSTimeDly (toDelay); // delay and wait (T-C) times
  }
}
```

## 2.2. OSInitExit
1. 在OS_CORE.C中定义
2. 该功能将在系统从ISR调用返回后管理调度
3. 我们需要在此处打印"抢先"事件

## 2.3. OS_Sched
1. 在OS_CORE.C中定义
2. 当任务自愿放弃对CPU的占有时，调用OS_Sched()
3. 我们需要在这里打印出"完整"事件

## 2.4. Printing messages
1. Print messages
2. `printf("\n%10d Preempt ",timestamp);`
3. 期望输出格式:
```
Current time | Event | [From Task ID] | [To Task ID]
Time tick (priority) | Preempt | TaskID(priority) | TaskID
```

# 3. 定义
1. 实施两组定期任务。
   1. TaskSet 1 = {t1(1,3), t2(3,6)}
   2. TaskSet 2 = {t1(1,3), t2(3,6), t3(4,9) }}
   3. 任务到达时间均为0
   4. 显示上下文切换行为
   5. 显示违反期限的情况

# 4. 课程
1. 如何创建在每p单位时间中精确执行c单位时间的任务？(c，p)
2. 我们可以在内核中的哪个位置添加用于观察上下文切换行为的代码？
  
# 5. 注意
1. 在实时应用程序中，确定任务周期，并通过硬件中断调用任务调用
2. 任务计算时间由最坏情况计算时间分析(WCET)确定
3. 在此项目中，我们将模拟这种行为，更重要的是，获得有关如何将CPU时间分配给任务的见解

# 6. 测试任务集合
1. 测试集1：{t1(1,3) , t2(3,5) }
2. 测试集2：{t1(1,4) , t2(2,5) , t3(2,10)}

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/hw01/4.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Introduction-to-Embedded-Systems/img/hw01/5.png)

# 7. 实验内容
1. ⽬标： 在ucOS-II上多任务实验。
2. 要求：
   1. 在pc上的ucOS-II移植版本上实现，参⻅Moodle上Lecture Notes下的实验⽬录uCOSII下的源码。
   2. MISRA C 2004 Guidelines for the use of the C language in critical systems
3. 提交
   1. 提交格式：学号_姓名.rar
   2. 完整的⽂档说明实现步骤，包括所增加的代码与注释，执⾏结果截图。
4. 任务集，包含3个周期性任务，选择合理的参数ti(ci,pi)，分别给出两种情况的输出：
   1. 任务之间没有相关性
   2. 任务之间有数据相关性(优先级最⾼与最低任务之间)