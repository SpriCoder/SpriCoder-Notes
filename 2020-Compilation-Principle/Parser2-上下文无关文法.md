上下文无关文法(CFG, Context-Free Grammer, 上下文无关文法)
---
1. LL(1)可以完成手写分析器
2. LR(1)可以更不容易出现细节问题
3. Bison工具是本实验使用的工具。

# 1. 上下文无关文法(CFG)定义
1. 上下文无关文法$G$是一个四元组$G=(T,N,P,S)$:
   1. T是**终结符号 Terminal**集合, 对应于词法分析器产生的词法单元
   2. N是**非终结符号 Non-terminal**集合
   3. P是**产生式 Production**集合

$$
A \in N \rightarrow \alpha \in (T \cup N)*
$$

2. 头部/左部(Head)$A$:
   1. **单个**非终结符，必须只有一个，是命名为上下文无关文法的原因。
   2. 如果有多个则不符合上下文无关文法，会被成为上下文有关文法，但是几乎无法处理。
3. 体部/右部(Body)$\alpha$:
   1. 终结符与非终结符构成的串
   2. 也可以是空串$\epsilon$
4. $S$为开始(Start)符号
5. 要求$S \in N$且唯一。

## 1.1. 上下文无关文法示例
1. 一个符号要么是终结符号，要么是非终结符号
2. 终结符号表示到此为止，无法再进行替换

$$
\begin{array}{l}
   G = (\{S\}, \{(, )\}, P, S) \\
   S \rightarrow SS \\
   S \rightarrow (S) \\
   S \rightarrow () \\
\end{array}
$$

> 上面的文法表示任意嵌套的所有匹配好的括号串

$$
\begin{array}{l}
   G = (\{S\}, \{a, b\}, P, S) \\
   S \rightarrow aSb \\
   S \rightarrow \epsilon \\
\end{array}
$$

> 可以有很多的情况

## 1.2. 条件语句文法
1. 条件语句文法中包含**悬空(Dangling)-else**文法的问
2. 这样的文法是有问题，我们进一步分析才可以，OTHER作为终结符。

## 1.3. 约定
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/5.png)

> **约定**: 如果没有明确指定, 第一个产生式的头部就是**开始符号**，用来避免写如上例子中的一些描述

## 1.4. 关于终结符号的约定
> 下述符号是终结符号:(通常的约定)

1. 在字母表里排在前面的**小写字母**，比如a、b、c。
2. **运算符号**，比如+、*等。
3. **标点符号**，比如括号、逗号等。
4. **数字**，0、1、.... 9。
5. **黑体字符串**，比如id或if。每个这样的字符串表示一个终结符号。
  
## 1.5. 关于非终结符号的约定
> 下述符号是**非终结符号**:

1. 在字母表中排在前面的**大写字母**，比如A、B、C。
2. **字母S**。它出现时通常表示开始符号。
3. 小写、斜体的名字，比如expr或stmt.

# 2. 语义
1. 上下文无关文法$G$定义了一个语言$L(G)$
2. 语言是**串**的集合

# 3. 推导(Derivation)的定义

## 3.1. 表达式文法
$$
E \rightarrow -E|E + E | E ∗ E | (E) | id
$$

1. 推导即是将某个产生式的左边**替换**成它的右边
2. 每一步推导需要选择替换**哪个非终结符号**，以及使用**哪个产生式**

$$
E \Rightarrow -E \Rightarrow −(E) \Rightarrow −(E+E) \Rightarrow −(id+E) \Rightarrow −(id+id)
$$

$$
\begin{array}{l}
   E \Rightarrow −E : 经过一步推导得出 \\
   E \xRightarrow{+} −(id + E):经过一步或多步推导得出 \\
   E \xRightarrow{*} −(id +E):经过零步或多步推导得出 \\
\end{array}
$$

$$
E \Rightarrow -E \Rightarrow −(E) \Rightarrow −(E+E) \Rightarrow −(E+id) \Rightarrow −(id+id)
$$

## 3.2. Definition (Sentential Form，句型)
> 如果$S \xRightarrow{*} \alpha$，且$\alpha \in ( T \cup N)^*$，则称$\alpha$是文法G的一个句型(包含非终结符)

$$
\begin{array}{l}
   E \rightarrow -E | E + E | E ∗ E | (E) | id \\
   E \Rightarrow -E \Rightarrow −(E) \Rightarrow −(E+E) \Rightarrow −(id+E) \Rightarrow −(id+id)
\end{array}
$$

## 3.3. Definition (Sentence，句子)
1. 如果$S \xRightarrow{*} w$，且$w \in T^*$，则称w是文法G的一个**句子**(没有非终结符了)
2. 句子就是这个语言中的串

# 4. Definition (文法G生成的语言L(G))
> 文法F的**语言**L(G)是它能推导出的**所有句子**构成的集合。

$$
w \in L(G) \Leftrightarrow S \xRightarrow{*} w
$$

## 4.1. 关于文法G的两个基本问题
1. Membership问题:给定字符串$x \in T^*, x \in L(G)$？字符串可不可以由文法推理得到
2. L(G)究竟是什么？

### 4.1.1. 问题一:Membership问题
1. 给定字符串$x \in T^*, x \in L(G)$，(即检查x是否符合文法G)
2. 这就是**语法分析器**的任务:为输入的词法单元流寻找推导、**构建语法分析树**, 或者**报错**

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/14.png)

1. **根节点**是文法G的起始符号
2. **叶子节点**是输入的词法单元流
3. 常用的语法分析器以**自顶向下**或**自底向上**的方式构建中间部分

### 4.1.2. 问题二:L(G) 是什么?
> 这是程序设计语言设计者需要考虑的问题

#### 4.1.2.1. 根据文法G推导语言L(G)
> 例子一
$$
\begin{array}{l}
   S \rightarrow SS \\
   S \rightarrow (S) \\
   S \rightarrow () \\
   S \rightarrow \epsilon \\
   L(G) = \{良匹配括号串\} \\
\end{array}
$$

> 例子二
$$
\begin{array}{l}
   S \rightarrow aSb \\
   S \rightarrow \epsilon \\
   L(G) = {a^nb^n|n \geq 0 } \\
\end{array}
$$

#### 4.1.2.2. 根据语言L(G)来推导文法G
1. 目标生成：字母表$\sum = {a, b}$上的所有**回文串**(Palindrome)构成的语言

$$
\begin{array}{l}
   S \rightarrow aSa \\
   S \rightarrow bSb \\
   S \rightarrow a \\
   S \rightarrow b \\
   S \rightarrow ϵ \\
   S \rightarrow aSa|bSb|a|b|\epsilon \\
\end{array}
$$

2. 目标生成：${b^na^mb^{2n}|n \geq 0, m \geq 0}$
$$
\begin{array}{l}
   S \rightarrow bSbb|A \\
   A \rightarrow aA|\epsilon \\
\end{array}
$$

3. 目标生成：$\{x\in \{a, b\}^* | x 中a,b个数相同 \}$
   1. 证明：a可以是空串
   2. 证明：a以a开头，那么后面肯定能找到**一个**b保证被分为了aVbV并且V中的ab数量均相同，以b开头类似。

$$
\begin{array}{l}
   V \rightarrow aVbV | bVaV | \epsilon \\
\end{array}
$$

4. 目标生成：$\{x\in \{a, b\}^* | x 中a,b个数不同 \}$
   1. T表示a多一个或者更多
   2. U表示b多一个或者更多
   3. UT不能同时出现，和V去组合即可
   4. 证明

$$
\begin{array}{l}
   S \rightarrow T | U \\
   T \rightarrow VaT |VaV \\
   U \rightarrow VbU | VbV \\
   V \rightarrow aVbV | bVaV | \epsilon \\
\end{array}
$$

## 4.2. 顺序语句、条件语句、打印语句
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/5.png)

> 上图中的L是顺序语句

# 5. L-System(不考)
> <a href = "https://en.wikipedia.org/wiki/L-system">L-System</a>:这不是上下文无关文法, 但精神高度一致

$$
\begin{array}{l}
   variables: A B \\
   constants: + - \\
   start: A \\
   rules:(A \rightarrow B-A-B),(B \rightarrow A+B+A) \\
   angles:60' \\
\end{array}
$$


1. $A,B$:向前移动并画线
2. +:左转
3. -:右转
4. 每一步都**并行地**应用**所有**规则

| ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/15.png) | ![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/16.png) |
| -------------------- | -------------------- |

$$
\begin{array}{l}
   variables: X Y
   constants: F + -
   start: FX
   rules:(X \rightarrow X+YF+),(Y \rightarrow -FX-Y)
   angles:90'
\end{array}
$$

1. $F$:向前移动并画线
2. +:右转
3. -:左转
4. X:仅用于展开，在作画时被忽略
5. 每一步都**并行地**应用**所有**规则

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/17.png)

# 6. 最左(leftmost) 推导与最右(rightmost) 推导
$$
\begin{array}{l}
   E \rightarrow E + E | E * E | (E) | id \\
   E \xRightarrow[lm]{} -E \xRightarrow[lm]{} -(E) \xRightarrow[lm]{} -(E+E) \xRightarrow[lm]{} -(id + E) \xRightarrow[lm]{} -(id+id)
\end{array}
$$

1. $E \xRightarrow[lm]{} -E$:经过一步最左推导得出
2. $E \xRightarrow[lm]{+} -(id + E)$:经过一步或多步最左推导得出
3. $E \xRightarrow[lm]{*} -(id + E)$:经过零步或多步最左推导得出
4. **最左推导**是有非终结符优先选择**最左侧**的进行推导
5. **最右推导**是有非终结符有限选择**最右侧**的进行推导

$$
E \xRightarrow[rm]{} -E \xRightarrow[rm]{} -(E) \xRightarrow[rm]{} -(E+E) \xRightarrow[rm]{} -(E + id) \xRightarrow[rm]{} -(id+id)
$$

## 6.1. Definition (Left-sentential Form，最左句型)
1. 如果$S \xRightarrow[lm]{*} \alpha$, 并且$\alpha \in (T \cup N)^*$，则称$\alpha$是文法G的一个**最左句型**。

$$
E \xRightarrow[lm]{} -E \xRightarrow[lm]{} -(E) \xRightarrow[lm]{} -(E+E) \xRightarrow[lm]{} -(id + E) \xRightarrow[lm]{} -(id+id)
$$

## 6.2. Definition (Right-sentential Form，最右句型)
1. 如果$S \xRightarrow[rm]{*} \alpha$, 并且$\alpha \in (T \cup N)^*$，则称$\alpha$是文法G的一个**最右句型**。

$$
E \xRightarrow[rm]{} -E \xRightarrow[rm]{} -(E) \xRightarrow[rm]{} -(E+E) \xRightarrow[rm]{} -(id + E) \xRightarrow[rm]{} -(id+id)
$$

# 7. 语法分析树
1. 语法分析树是静态的, 它不关心动态的推导顺序

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/18.png)

2. 一棵语法分析树对应多个推导
3. 但是, 一棵语法分析树与**最左(最右) 推导**一一对应

## 7.1. 二义性引入
4. 1 - 2 - 3的语法树的两种不同表达形式
5. 以下的两棵语法树是不同的，生成出来的目标代码也是不同的
6. 这个文法是有问题的，这个文法具有二义性，我们需要通过**修改文法**避开二义性问题。
7. 语法没有二义性的描述，L(G)本身只是一个串的集合。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/19.png)

## 7.2. Definition (二义性(Ambiguous) 文法)
1. 如果L(G) 中的**某个**句子有**一个以上**语法树/最左推导/最右推导,则文法G是二义性的。
2. 1 + 2 * 3的语法树

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/20.png)

## 7.3. 悬空-else
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/6.png)

# 8. 二义性文法
1. 不同的语法分析树产生不同的语义
2. 所有语法分析器都要求文法是**无二义性**的

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/7.png)

3. Q:如何识别二义性文法?这是**不可判定**的问题，是指没有通用的算法，可以判断任意的文法G
4. Q:如何消除文法的二义性?

## 8.1. 消除文法二义性
1. 四则运算均是左结合的
2. **优先级**: 括号最先, 先乘除后加减
3. 二义性表达式文法以**相同的方式**处理所有的算术运算符
4. 要消除二义性, 需要**区别对待**不同的运算符
5.  将运算的"先后" 顺序信息编码到语法树的"层次"结构中

$$
\begin{array}{l}
   E \rightarrow E + E | id \\
\end{array}
$$

## 8.2. 左结合文法
$$
\begin{array}{l}
   E \rightarrow E + T \\
   T \rightarrow id \\
\end{array}
$$

## 8.3. 右结合文法
$$
\begin{array}{l}
   E \rightarrow T + E \\
   T \rightarrow id \\
\end{array}
$$

## 8.4. 使用左(右)递归实现左(右)结合

## 8.5. 括号最先, 先乘后加文法
> 乘号更靠近叶子节点

$$
\begin{array}{l}
   E \rightarrow E + E|E*E|(E)|id \\
   E \rightarrow E + T|T \\
   T \rightarrow T * F | F\\
   F \rightarrow (E)|id
\end{array}
$$

## 8.6. Summary
$$
\begin{array}{l}
   E \rightarrow E + E|E - E|E*E|E/E|(E)|id|number \\
   E \rightarrow E + T | E - T|T \\
   T \rightarrow T * F | T/F | F \\
   F \rightarrow (E) | id | number \\
\end{array}
$$

1. **无二义性**的表达式文法
   1. E:表达式(expression)
   2. T:项(term)
   3. F:因子(factor)
2. **将运算的"先后"顺序信息编码到语法树的"层次"结构中**

## 8.7. IF-Then-Else问题

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/8.png)

> 每个else与**最近的尚未匹配的**then匹配

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/13.png)

1. 基本思想: **then与else**之间的语句必须是"**已匹配的**"
2. 证明两件事情：证明部分不作为重点
   1. $L(G) = L(G')$
   2. $G'$是无二义性的

### 8.7.1. $L(G) = L(G')$证明过程
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/13.png)

$$
\begin{array}{l}
   L(G') \subseteq L(G) 简单容易证明\\
\end{array}
$$

> 文法是递归的，我们可以使用数学归纳法，对推导步骤进行归纳
$$
\begin{array}{l}
   L(G) \subseteq L(G') \\
   x \in L(G) \rightarrow x \in L(G') \\
   stmt \rightarrow ... \rightarrow x \\
\end{array}
$$

1. 只要G中展开一步，G'中都有相应的对应即证明了$L(G) \subseteq L(G')$

### 8.7.2. $G'$ 是无二义性的
1. 每个句子对应的**语法分析树**是唯一的
2. 只需证明: 每个非终结符的**展开方式**是唯一的

$$
\begin{array}{l}
   L(matched\_stmt) \cap L(open\_stmt) = \emptyset \\
   L(matched\_stmt_1) \cap L(matched\_stmt_2) = \emptyset \\
   L(open\_stmt_1) \cap L(open\_stmt_2) = \emptyset \\
\end{array}
$$

> 上面的下标代表子句   


1. Q：为什么不使用优雅、强大的**正则表达式**描述程序设计语言的语法?
2. A：正则表达式的表达能力**严格弱于**上下文无关文法

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/10.png)

> 每个**正则表达式**r对应的语言L(r) 都可以使用**上下文无关文法**来描述

$$
r=(a|b)^∗abb
$$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/11.png)

1. 此外, 若$\delta(A_i,\epsilon) = A_j$，则添加$A_i \rightarrow A_j$

$$
\begin{array}{l}
   S \rightarrow aSb \\
   S \rightarrow \epsilon \\
   L = {a^nb^n|n \geq 0} \\
\end{array}
$$

1. 该语言**无法**使用正则表达式来描述
2. 定理:$L = \{a^nb^n | n ≥ 0\}$ 无法使用正则表达式描述
3. 反证法
   1. 假设存在正则表达式r:$L(r) = L$
   2. 则存在**有限**状态自动机D(r):$L(D(r)) = L$; 设其状态数为k
   3. 考虑输入$a^m(m>k)$

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/12.png)

1. $D(r)$也能接受a^{i+j}b^i，**矛盾**！
2. Pumping Lemma for Regular Languages：$L = {a^nb^n | n \geq 0}$
3. Pumping Lemma for Context-free Languages:$L = {a^nb^nc^n | n \geq 0}$
4. 只考虑无二义性的文法这意味着,每个句子对应唯一的一棵语法分析树
