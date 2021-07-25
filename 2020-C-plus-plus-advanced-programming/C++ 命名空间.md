命名空间
---

<!-- TOC -->

- [1. 命名空间的理念和作用](#1-命名空间的理念和作用)
  - [1.1. 命令空间的目的](#11-命令空间的目的)
  - [1.2. 命令空间的理念](#12-命令空间的理念)
  - [1.3. 命名空间的快速要求](#13-命名空间的快速要求)
  - [1.4. 例子](#14-例子)
- [2. 命名空间的两种形式](#2-命名空间的两种形式)
  - [2.1. 细节](#21-细节)

<!-- /TOC -->

# 1. 命名空间的理念和作用
1. 理念
    1. 兼容
    2. 快速:理解、实现
2. 作用:进一步解决了全局变量/函数的名冲突
3. 在约束作用域方向，替代static
4. 细节特点:
    1. 别名
    2. 全局
    3. 开放
    4. 可嵌套
    5. 可重载
5. 不可以在同一作用域两次使用using-directive
```c++
namespace L{
    int k;
    void f(int);
}
//using-declaration
using L::k;
using L::f;
k = 0;
f(6);
//using-directive
k = 0;
f(6);
```

## 1.1. 命令空间的目的
1. 解决lib的冲突的
2. 是在94标准化中出现的
3. 重要的原因:避免一些命名问题、宏问题和类问题
4. 可以将优先作用域更加有效的表示出来。

## 1.2. 命令空间的理念
1. 兼容
    + link不冲突
    + 程序中定义新名称时不必担心与其他(比如库)冲突
    + 在库里增加名字，不影响用户
    + 不同库里含有同名元素，可选择
    + 不修改函数的前提下，可消解名冲突
    + 避免命名空间的名字之间发生冲突
    + 使名字空间可以处理标准库
2. 原则：
    + 防冲突
    + 遇冲突，可选择
    + 易扩展，与用户独立

## 1.3. 命名空间的快速要求
1. 理解:10 minutes
2. 时间:2 weeks

## 1.4. 例子
```c++
#define Func(x,y) x ## y//连接x和y
Func(my,_f)();
//my_f()
Func(your,_f)()
```

# 2. 命名空间的两种形式
```c++
namespace L
{
    int k;
    void f(int);
}
```
1. declaration:对每一个变量进行管理控制
```c++
using L::k;
using L::f; 

k=0;
f(6);
```
2. directive:全局应用
```c++
using namespace L;

k=0;
f(6);
```
3. 在约束作用域方面，替代static

## 2.1. 细节
1. 别名(namespace本身名字也会冲突)
```c++
namespace American_Telephone_and_Telegraph {}
namespace ATT = American_Telephone_and_Telegraph
```
2. 全局：无命名空间，只有`::`默认为全局变量
```c++
int a;
namespace X{
    int a;
    void f(){
        int a=0;
        a++;
        X::a++;
        ::a++;//无命名空间则为全局变量，全局变量默认最外层
    }
}
```
1. 开放:可以多次定义，持续扩展
```c++
namespace A
{   int a;
}

namespace A
{   void f() ;
}
```
4. 可嵌套
```c++
namespace L1{
    int a;
    namespace L2{
        void f() ;
    }
}
L1::L2::f(); 
using namespace L1;
L2::f();
```
5. 重载
```c++
namespace B{
    void f(int) ;
}
namespace A{
    void f(char) ;
}
void f();
using namespace A;//A::f和f形成了重载关系

void g(){
   f('1');
}
```
```c++
//错误
//不要在同一个作用域中两次使用using-directive
using namespace B;
using namespace A;
…….
void g()
{ 
    f('1');
}

```
6. 向前兼容:新的语言成分不应该对以前的程序的影响
    + 优先考虑:using-declaration
    + .h和非.h文件:如果使用stdio需要写`using namespace std`;
```c++
#include <stdio.h>
int main(){
    printf("hello, world\n"); 
}
//stdio
namespace std { 
int printf( const char *, …);
}
//stdio.h

namespace std { 
int printf( const char *, …);
}
using namespace std;
```