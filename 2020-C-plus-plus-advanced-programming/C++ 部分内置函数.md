C++部分内置函数
---

<!-- TOC -->

- [1. 内置函数](#1-内置函数)
- [2. 系统时间](#2-系统时间)
  - [2.1. 通过SYSTEMTIME来进行获取](#21-通过systemtime来进行获取)
  - [2.2. 参考](#22-参考)
- [3. sort函数的用法](#3-sort函数的用法)
  - [3.1. sort()的标准型](#31-sort的标准型)
  - [3.2. 参考](#32-参考)
- [4. put()和write()](#4-put和write)
  - [4.1. put()](#41-put)
  - [4.2. write()](#42-write)
  - [4.3. 参考](#43-参考)

<!-- /TOC -->

# 1. 内置函数
函数|作用
--|--
max(a,b)|取最大值
min(a,b)|取最小值

# 2. 系统时间

## 2.1. 通过SYSTEMTIME来进行获取
1. 相应头文件:`windows.h`
2. 变量类型：SYSTEMTIME sys;
3. 获取当前系统时间:`GetLocalTime(&sys)`
4. 其结构定义如下:
```c++
typedef struct _SYSTEMTIME {
    WORD wYear;//年
    WORD wMonth;//月
    WORD wDayOfWeek;//星期
    WORD wDay;//日
    WORD wHour;//时
    WORD wMinute;//分
    WORD wSecond;//秒
    WORD wMilliseconds;//毫秒
  } SYSTEMTIME;
```

## 2.2. 参考
<a href = "https://blog.csdn.net/TweeChalice/article/details/96501332">SYSTEMTIME</a>

# 3. sort函数的用法
1. 被包含的头文件:`#include<algorithm>`

## 3.1. sort()的标准型
1. `sort(a,b,function_name)`
  + 可以调用定义的函数，default->整数的
  + function要求他们的参数应当为两个。
2. 可以自定义的函数cmp(a,b)

```c++
sort(first_pointer,second_pointer,cmp);
//cmp(a,b)可以自定义
//返回1表示a在b前，返回0表示a在b后面
bool cmp(const int &a,const int &b) {
	return a > b;
}

int main() {
	vector<int> temp = { 6, 5, 4, 3, 2, 1 };
	out(temp);
	sort(temp.begin(), temp.end() , cmp);
	out(temp);
}
```

## 3.2. 参考
1. <a href = "https://blog.csdn.net/fadedsun/article/details/78796158">c++sort函数的用法</a>

# 4. put()和write()

## 4.1. put()
1. 原型:`put()`:适用于wchar_t
  + `osrteam &put(char)`
  + 返回一个指向调用对象的引用，也就是可以直接拼接输出

## 4.2. write()
1. 原型:`basic_ostream<charT,traits> &write(const char_type* s,streamsize n);`
2. write():方式返回一个指向调用它对象的引用，所以可以拼接，并不会遇到空制度时自动停止打印字符，而是打印指定数目的字符。

## 4.3. 参考
1. <a href = "https://www.cnblogs.com/maqiang/archive/2012/05/02/2478400.html">c++ put()与write()</a>