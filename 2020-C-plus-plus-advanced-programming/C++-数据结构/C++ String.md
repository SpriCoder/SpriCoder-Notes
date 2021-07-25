string类
---
1. <a href = "https://www.cnblogs.com/engraver-lxw/p/7581540.html">相关方法</a>
2. 复制用=号
3. 连接用+号
4. 比较直接用是运算符
5. 支持字符串数组

<!-- TOC -->

- [1. c++中的字符串的表示](#1-c中的字符串的表示)
- [2. string操作](#2-string操作)
  - [2.1. getline 三个参数](#21-getline-三个参数)
  - [2.2. 从string中获取char字符](#22-从string中获取char字符)
  - [2.3. replace](#23-replace)
  - [2.4. 比较](#24-比较)
  - [2.5. 连接](#25-连接)
  - [2.6. 长度](#26-长度)
  - [2.7. 查找](#27-查找)
  - [2.8. 其他操作一览](#28-其他操作一览)
  - [2.9. 字符串分隔](#29-字符串分隔)
  - [2.10. string的大小写转换](#210-string的大小写转换)
- [3. string和数值类型转换](#3-string和数值类型转换)
  - [3.1. C++11标准:string转换成数值类型](#31-c11标准string转换成数值类型)
  - [3.2. string转换成数值类型(sscanf方法)](#32-string转换成数值类型sscanf方法)
  - [3.3. int转换成string](#33-int转换成string)
    - [3.3.1. 实例代码](#331-实例代码)
    - [3.3.2. 处理复用问题和内存问题](#332-处理复用问题和内存问题)
  - [3.4. 数字转换为字符串](#34-数字转换为字符串)
  - [3.5. C++11标准:数字转字符串](#35-c11标准数字转字符串)
  - [3.6. 字符串转换为char数组](#36-字符串转换为char数组)
  - [3.7. 字符串切片](#37-字符串切片)
  - [3.8. 字符转换整数或者浮点数](#38-字符转换整数或者浮点数)
- [4. 参考](#4-参考)

<!-- /TOC -->

# 1. c++中的字符串的表示
1. 使用string的形式来做，我们需要使用头文件<string.h>
2. char* 指向字符串的指针，实质上是指向字符串的首字母
3. const char* 一个不可以被修改的字符串
4. char[] 一个字符数组

# 2. string操作
1. 读入:
    1. 不能读入空格，以空格、制表符、回车符作为结束标志
    2. cin >> s
```c++
string str1,str2,str3;
cin >> str1 >> str2 >> str3;
cout << str1 << "|" << str2 << "|" << str3 << "|";
```
2. getline(cin,s):是指一次读一行，可以读入空格和制表符，以回车为结束符
```c++
string str1,str2,str3;
getline(cin,str1);
getline(cin,str2);
getline(cin,str3);
```

## 2.1. getline 三个参数
1. 可以添加第三个参数是结束符
2. 第一个参数是cin输入流，第二个参数是字符串，第三个是结束符。
```c++
//输入 a b"c"\nC
getline(cin,str1," ");//a
getline(cin,str2,"'");//b
getline(cin,str3,"'");//c
getline(str4);//\n
getchar();//C
//注意回车的存在
```
3. 可以进行分隔来进行进一步处理
4. 实现split:`,`分隔
```c++
string inputValues
getline(cin,inputValues);
vector<int> num;
istringstream iss(inputValues);
string temp;
while(getline(iss,temp,',')){
  num.push_back(stoi(temp));
}
```

## 2.2. 从string中获取char字符
1. str.at(int index)
2. str[index]

## 2.3. replace

| 函数名                           | 作用                                                                  |
| -------------------------------- | --------------------------------------------------------------------- |
| replace(num1,num2,str)           | 将从num1开始的num2个字符替换成为str                                   |
| replace(num1,num2,str,num3,num4) | 将当前字符串的第num1开始的num2个字符替换成str的nums3开始的nums4个字符 |
| replace(num1,num2,num3,char)     | 字符串第num1位置上以及后面的num2个字符替换成num3个char                |

## 2.4. 比较
1. compare
```c++
if(s1 < s2)
s1.compare(s2)
//0 表示 相同
//1 表示 大于
//-1 表示 小于
```
2. strcmp
```
int strcmp(const char *str1, const char *str2)
如果返回值 < 0，则表示 str1 小于 str2
如果返回值 > 0，则表示 str2 小于 str1
如果返回值 = 0，则表示 str1 等于 str2
```
## 2.5. 连接
1. string = string1 + string2
2. string1.append(string2)

## 2.6. 长度
1. str.size() 或者 str.length()

## 2.7. 查找

| 函数名              | 作用                    |
| ------------------- | ----------------------- |
| str.find(str1)      | 从前往后第一次找到      |
| str.find(str1,num)  | 从num开始第一次找到str  |
| str.rfind(str1)     | 从后往前第一次找到      |
| str.rfind(str1,num) | 从后面向前第一次找到str |
| str.substr(pos,n)   | 从pos开始取n个字符      |

## 2.8. 其他操作一览

| 函数名                                                   | 作用                       |
| -------------------------------------------------------- | -------------------------- |
| strcat(char[],const char[])                              | 字符串连接                 |
| strcpy(char *dest,const char *src)                       | 字符串复制函数             |
| strlen(const char[])                                     | 字符串长度函数             |
| getchar()                                                | 获取一个字符               |
| str.erase(num1,num2)                                     | 擦除从num1开始的num2个字符 |
| str.insert(num,str)                                      | 在第num个位置上插入str2    |
| reverse(str.begin(),str.end())                           | 将字符串反过来             |
| transformer(str.begin(),str.end(),str.begin(),::toupper) | 转换                       |

## 2.9. 字符串分隔
1. 原型:char* strtok(char* str,char* delim)|
2. 用来进行分解字符串,将str按照delim进行分割，返回第一个分隔值，之后只要循环进行分隔就行。
3. sentence中间是第一个分隔的。
```c++
char sentence[] = "This is a sentence";
char *tokenPtr = strtok(sentence," ")
while(tokenPtr!= NULL){
  tokenPtr = strtok(NULL," ");//继续分隔之前的
}
```

## 2.10. string的大小写转换
1. 使用`string.h`头文件
```c++
//char[]数组，同样string也是可以的
char s[100];
s[i] = toupper(s[i]);//转换为大写
s[i] = tolower(s[i]);//转换为大写
```
2. 使用`algorithm`头文件
```c++
s1[i] = toupper(s1[i]);//转换为大写
transform(s.begin(),s.end(),s.begin(),::toupper);//转换大写
transform(s.begin(),s.end(),s.begin(),::tolower);
//转换小写
```

# 3. string和数值类型转换

## 3.1. C++11标准:string转换成数值类型
```c++
int i = stoi(str);
//64位 long = int
long i = std::stol(str);//stoll long long
float i = std::stof(str);
double i = str::stod(str);//越界会报错
```
1. 具体的整数部分函数:其中b表示转换所用的基数，默认为10(表示十进制).p是size_t的指针，用来保存s中第一个非数值字符的下标，p默认为0，即函数不返回下标.
   1. stoi(s,p,b):int
   2. stol(s,p,b):long
   3. stoul(s,p,b):unsigned long
   4. stoll(s,p,b):long long
   5. stoull(s,p,b):unsigned long long;
2. 具体的小数部分函数:参数p的作用与整数转换函数中的一样。
   1. stof(s, p):float
   2. stod(s, p):double
   3. stold(s, p):long double

## 3.2. string转换成数值类型(sscanf方法)
1. sscanf() 用于将字符串转化为数字

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
  char str[]="1234321"; 
  int a; 
  sscanf(str,"%d",&a); 
  cout<<a<<endl;
  char str1[]="123.321"; 
  double b; 
  sscanf(str1,"%lf",&b); 
  cout<<b<<endl;
  return 0;
}
```

## 3.3. int转换成string
1. 使用Stringstream
2. 头文件:`#include<sstream>`
  
### 3.3.1. 实例代码
```c++
#include <iostream>
#include <sstream>
#include <string>
using namespace std;
int main(){
    //clear()很好解决复用问题但内存消耗大
    int size = 100;  
    stringstream strStream;  
    for (int i = 1; i < size; ++i){  
      strStream.clear();
      strStream << i;//数字转换成流
      string numStr;
      strStream >> numStr;//流输出为字符串  
      cout<<numStr<<" ";
      strStream.str("");
    }  
    cout<<endl;
    printf("size=%d\n", strStream.str().capacity());  
    return 0;  
}
```

### 3.3.2. 处理复用问题和内存问题
1. 每次调用strStream.clear()是希望在每次使用完strStream之后清理strStream占用的资源，但stringstream的clear方法并没有真正地释放strStream占用的空间，这样strStream所占用的空间一直在增长。当size较大时，strStream消耗的内存迅速增长，可能出现严重问题。
2. 所以我们使用`strStream.str("")`来清空缓存区

## 3.4. 数字转换为字符串
1. 更加自由，不限制于整数
2. sprintf() 用于将数字转化为字符串:`sprintf(res,"%s%s",a,b)`
3. 简单转换方法:`to_string()`
```c++
std::to_string(num);
```

```c++
#include <iostream>
#include <string>
using namespace std;
int main(){
    char str[10]; 
    int a=1234321;
    //将整数转化为字符串
    sprintf(str,"%d",a);
    int len=strlen(str);
    cout<<"字符串"<<str<<endl;
    cout<<"长度"<<len<<endl;
    char str1[10]; 
    double b=123.321;
    //将浮点数转化为字符串
    sprintf(str1,"%.3lf",b);
    int len1=strlen(str1);
    cout<<"字符串"<<str1<<endl;
    cout<<"长度"<<len1<<endl;
    return 0;
}
```

## 3.5. C++11标准:数字转字符串
1. 标准库中定义了to_string(val);可以将其它类型转换为string。还定义了一组stoi(s,p,b)、stol(s,p,b)、stod(s,p,b)等转换函数，可以函数，可以分别转化成int、long、double等.

## 3.6. 字符串转换为char数组
```c++
getline(cin,input);
strcpy_s(str, input.c_str());
```

## 3.7. 字符串切片
```c++
int main() {
	string test = "123";
	cout << test.substr(1, test.size() - 2);//'2'
	cout << test.substr(1, test.size() - 1);//'23'
}
```

## 3.8. 字符转换整数或者浮点数
1. atof:转换为浮点数
2. atoi:转换为整数

# 4. 参考
1. <a herf = "https://blog.csdn.net/l631068264/article/details/25115917">Stringstream 缓冲区清空方法 和 复用StringStream 不是clear那么简单</a>
2. <a href = "https://www.cnblogs.com/houchen/p/8984164.html">c++数字和字符串的转换</a>
3. <a href = "https://blog.csdn.net/HiccupHiccup/article/details/62421032">【整理】C++ string转int，string转double，string转long，int转string，double转string…</a>