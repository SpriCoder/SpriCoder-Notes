IR4-函数与补充
---

# 1. 函数和过程

## 1.1. 函数/过程的中间代码翻译
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/62.png)

> call语句：$call\ name,\ param\_number$

## 1.2. 新增文法以支持函数定义与调用
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/63.png)

## 1.3. 函数定义
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/64.png)

1. 函数名id放入当前符号表,建立新的符号表,处理形参F与函数体S

## 1.4. 函数调用
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/65.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/66.png)

> C语言并未规定参数计算的顺序

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/67.png)

> 集中生成param指令,代码更紧凑

# 2. if/if-else

# 3. Pumping Lemma
1. RE(NFA, DFA)
2. CFG

# 4. Elemination of Left-Recursion
1. 左递归问题的消除：
   1. $A \rightarrow Ax | b$
   2. $A \xrightarrow{+} Ax|b$

# 5. Code Generation

# 6. 考试
1. 正则表达式与自动机(10 = 3:4:3)
2. LL语法分析(10 = 2:4:3:1)
3. LR语法分析(10 = 2:3:2:3)
4. 语法指导定义与翻译(10 = 6:4):第一问比较简单
5. 中间代码生成(10 = 3:3:4)
6. ???(附加题5分)