Sematics3-实验代码示例
---

# 1. while语句的翻译
1. 类型声明与使用(符号表)
2. 类型检查
3. 中间代码生成,要有大局观
4. 认清"你"在语法分析树中所处的位置

## 1.1. While语句的SDD
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/49.png)

$$
S.code = ···|goto\ L1
$$

1. C.code是返回回来的
   1. C.false的赋值就是告诉其应该跳转到哪里，这里跳转到S.next，也就是跳转到S的兄弟节点
   2. C.true的赋值就是跳转到L2进行
2. S1.next = L1是保证其可以完成循环中提前跳转，比如continue
3. 后面那是S1.code
4. C.true和C.false都是继承属性。

## 1.2. while语句的SDT
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/50.png)

## 1.3. 用一个递归下降语法分析器实现while语句的翻译
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/51.png)

1. next是S的继承属性

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/52.png)

1. 使用全局缓冲区
   1. 比如L1在缓冲区，C生成的部分放到缓冲区即可，以此类推。
   2. 避免了出现中间代码有重复
   3. 避免了拼接的问题

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/53.png)

# 2. Definition (符号表(Symbol Table))
> **符号表**是用于保存各种信息的**数据结构**。

1. 标识符:词素、类型、大小、存储位置等

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/54.png)

2. 通常使用HashTable

## 2.1. 为每个作用域建立单独的符号表
> 可以使用符号表栈实现树形的嵌套关系

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/55.png)

1. 每一个作用于都会有一张单独的符号表(哈希表)
2. 符号表栈：及时出栈

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/56.png)

> 翻译任务:忽略声明部分,为每个标识符标明类型

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/57.png)

## 2.2. Definition (类型表达式(Type Expressions))
1. 基本类型是类型表达式;
   1. char, bool, int, float, double, void,. . .
2. 类名是类型表达式;
3. 如果t是类型表达式,则array(num, t)是类型表达式;
4. record(⟨id : t, . . .⟩)是类型表达式;
5. 如果$s$和$t$是类型表达式,则$s * t$(笛卡尔积)是类型表达式;
6. 如果$s$和$t$是类型表达式,则$s \rightarrow t$(表示函数，$s$输入，$t$为输出)是类型表达式;
7. 类型表达式可以包含取值为类型表达式的变量。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/58.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/59.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/60.png)

## 2.3. 类型声明
1. 符号表中记录标识符的类型、宽度(width)、偏移地址(offset)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/61.png)

## 2.4. 需要为每个record生成单独的符号表
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/62.png)

1. 全局变量t与w将B的类型与宽度信息递给产生式$C \rightarrow \epsilon$
2. float x

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/63.png)

## 2.5. 数组类型的语法制导
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/64.png)

$$
int[2][3]
$$

1. 全局变量offset表示变量的相对地址
2. 全局变量top表示当前的符号表

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/65.png)

$$
float\ x; float\ y;
$$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/66.png)

4. record类型表达式:record(top)
5. 全局变量top表示当前的符号表
6. 全局变量Env表示符号表栈
7. record { float x; float y; } p;

## 2.6. 完整的例子

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/67.png)

- offset稳定增长
- top可能会回退

## 2.7. 类型检查的常见形式
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/68.png)

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/69.png)

## 2.8. 结构等价和名等价

### 2.8.1. Definition (结构等价(Structurally Equivalent))
1. 两种类型结构等价当且仅当以下任一条件为真:
   1. 它们是相同的基本类型;
   2. 它们是将相同的类型构造算子应用于结构等价的类型而构造得到;
   3. 一个类型是另一个类型表达式的名字。

### 2.8.2. Definition (名等价(Name Equivalent))
1. 两种类型名等价当且仅当以下任一条件为真:
   1. 它们是相同的基本类型;
   2. 它们是将相同的类型构造算子应用于结构等价的类型而构造得到。

### 2.8.3. 结构等价中的"结构"又是什么意思?
```
array(n, t)       array(m, t)
record(⟨a: int⟩)   record(⟨b: int⟩)
```

1. 取决于语言设计者的"大局观"

## 2.9. 类型综合
> 根据子表达式的类型确定表达式的类型

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/70.png)

$$
E_1+E_2
$$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/71.png)

1. 重载函数的类型综合规则

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/72.png)

## 2.10. 类型推导
> 根据某语言结构的使用方式确定表达式的类型

- null(x) :x是一个列表,它的元素类型未知
- C++ 的 Template

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/73.png)

## 2.11. 类型转换
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/74.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/75.png)

1. 拓宽是从下向上，比如short和char做运算，那么会都先转化为int然后计算，也就是找到最小共有祖先。
2. 窄化是从上向下

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec4/76.png)

1. 类型不相同，但是兼容，则转化。