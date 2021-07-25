struct 结构体
---

1. 赋值-同类型:同类型一共就两种情况
   1. 同类型:Memory copy
   2. 同类型:Typedef
   3. 内存布局就算是一样也不认为是相同的。
2. alignment:一般是指内存对齐(存在于大多数编程语言中)
   1. 契合硬件
   2. 提升效率
3. 我们使用参数传递
4. C++向前兼容，class不写访问权限，全部都是private，struct不写访问权限，全部都是public
5. struct也可以被理解成为类
6. 结构体是按名访问
7. typedef:是重命名

```c++
struct B
{
    char  b; //1
    int   a; //4
    short c; //2
};
cout << sizeof(B);//12
//为什么是12，是因为内存空间对齐，提高内存访问效率
```
```c++
//可关闭
__declspec(align(8))
#pragma pack(n)
//可以调整内存布局，将c和b整合到一起，然后B就是大小为8
```
8. 使用pack可以让其摒弃用存储空间换取时间的做法，将空间尽可能的利用起来。