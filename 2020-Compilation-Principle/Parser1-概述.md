Lecture3-Parser
---

1. **输入**:程序文本/字符串s & **词法单元(token) 的规约**

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/1.png)

2. **输出**:词法单元流

# 1. 语法分析举例
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/2.png)

# 2. 语法分析阶段的主题

## 2.1. 上下文无关文法
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/3.png)

1. 我们需要递归来提升我们语言的能力。

## 2.2. 构建语法分析树
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec3/4.png)

1. 自顶向上构造：比较符合直观，但是能力有限
2. 自底向下构造：Knuth算法

## 2.3. 错误恢复
1. 报错
2. **恢复**：现在的程序是比较大的，如果直接停止编译则导致有多少错误就需要编译多少次，不合适。
3. 继续分析