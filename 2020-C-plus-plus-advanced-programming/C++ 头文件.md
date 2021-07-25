C++ 头文件
---

<!-- TOC -->

- [1. 头文件](#1-头文件)
- [2. 头文件主要内容](#2-头文件主要内容)

<!-- /TOC -->

# 1. 头文件
1. `#include`
2. iostream：输入输出流
3. cmath：数学函数
4. iomanip：I/O流控制符

# 2. 头文件主要内容
1. 头文件可以包含常量定义、变量/函数声明、编译预处理、类型定义、内联函数
```c++
//const.h
const double pi = 3.1415926;
```
```c++
//a.h
extern float salary;
extern void show();
```
2. 调用头文件:`#include "a.h"`