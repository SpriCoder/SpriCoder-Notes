IR1-中间代码生成概述
---

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/1.png)

# 1. Intermediate Representation (IR)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/2.png)

1. **精确**:不能丢失源程序的信息
2. **独立**:不依赖特定的源语言与目标语言(如,没有复杂的寻址方式)
3. 图(抽象语法树)、三地址代码、C语言：C语言也可以作为中间代码，比如Haskel和早期的C++

# 2. 表达式的有向无环图
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/3.png)

> 针对生成的有向无环图来生成中间表示是合适的。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/4.png)

> 在创建节点之前,先判断是否已存在(哈希表)，如果已经常见直接用指针指向即可。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/5.png)

# 3. Definition (三地址代码(Three-Address Code (TAC; 3AC)))
> 每个TAC指令最多包含三个操作数。

1. 三地址代码指令

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/6.png)

2. 调用p函数，有n个参数，返回值为y

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/7.png)

3. 数组则要涉及到地址距离计算

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/8.png)

$$
\begin{aligned}
  &do \\
  &\qquad i = i + 1;\\
  &while(a[i] < v);
\end{aligned}
$$

> 由于三地址代码，所以我们会引入大量的中间代码

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/9.png)

# 4. 三地址代码的四元式表示
> 代码优化暂时不考虑

## 4.1. Definition (四元式(Quadruple))
> 一个四元式包含四个字段,分别为op、arg1、arg2与result。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/10.png)

1. =[] 和 []= 都是我们约定好的操作符号。

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/11.png)

## 4.2. 表达式的中间代码翻译
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/12.png)

1. $E.code$是生成的中间代码
2. $E.addr$是地址
3. 得到$E$之前，要先知道$E_1$和$E_2$的三地址代码，然后并且赋值给$E_3$
4. $id$则是仅仅获得地址即可
5. 重难点

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/13.png)

5. 只需要$E.addr$，我们使用全局缓冲区解决传递拷贝三地址代码的问题。

## 4.3. 表达式的中间代码翻译(增量式)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/14.png)

## 4.4. 数组引用的中间代码翻译
1. 声明:$int\ a[2][3]$
2. 数组引用:$x=a[1][2];a[1][2] =x$
3. 需要计算$a[1][2]$的相对于数组基地址a的偏移地址

> 语法分析格式分析

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/15.png)

> 存储空间推导

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/16.png)

> 复杂的SDT实现

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/17.png)

### 4.4.1. 和L相关的综合属性
1. 综合属性$L.array.base$:数组基地址(即,数组名)，符号表可以查找到
2. 综合属性$L.addr$:偏移地址

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/18.png)

### 4.4.2. 和L相关的产生式

> 综合属性$L.array$:数组名id对应的符号表条目

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/19.png)

> 综合属性$L.type$:(当前)元素类型

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/20.png)

> 综合属性$L.addr$:(当前)偏移地址

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/21.png)
![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-Compilation-Principle/img/lec5/22.png)

$$
\begin{array}{l}
  t_1 = i * 12 \\
  t_2 = j * 4 \\
  t_3 = t_1 + t_2 \\
  t_4 = a[t_3] \\
  t_5 = c + t_4 \\
  \\
  int\ a[2][3]\\
\end{array}
$$

