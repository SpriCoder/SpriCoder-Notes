list类
---

<!-- TOC -->

- [1. 定义](#1-定义)
- [2. 定义和初始化](#2-定义和初始化)
- [3. List常用操作函数](#3-list常用操作函数)
- [4. 链表操作](#4-链表操作)
  - [4.1. 插入](#41-插入)
  - [4.2. 删除](#42-删除)
- [5. 其他参考](#5-其他参考)

<!-- /TOC -->

# 1. 定义
1. 是一个stl实现的双向链表，与vectors相比，允许快速的插入和删除，但是随即访问却比较慢。
2. 使用头文件`#include<list>`

# 2. 定义和初始化
```c++
list<int> lst1;          //创建空list
list<int> lst2(5);       //创建含有5个元素的list
list<int> lst3(3,2);  //创建含有3个元素的list
list<int> lst4(lst2);    //使用lst2初始化lst4
list<int> lst5(lst2.begin(),lst2.end());  //同lst4
```

# 3. List常用操作函数

| 函数名               | 函数作用                       |
| -------------------- | ------------------------------ |
| Lst1.assign()        | 给list赋值                     |
| Lst1.back()          | 返回最后一个元素               |
| Lst1.begin()         | 返回指向第一个元素的迭代器     |
| Lst1.clear()         | 删除所有元素                   |
| Lst1.empty()         | 如果list是空的则返回true       |
| Lst1.end()           | 返回末尾的迭代器               |
| Lst1.erase()         | 删除一个元素                   |
| Lst1.front()         | 返回第一个元素                 |
| Lst1.get_allocator() | 返回list的配置器               |
| Lst1.insert()        | 插入一个元素到list中           |
| Lst1.max_size()      | 返回list能容纳的最大元素数量   |
| Lst1.merge()         | 合并两个list                   |
| Lst1.pop_back()      | 删除最后一个元素               |
| Lst1.pop_front()     | 删除第一个元素                 |
| Lst1.push_back()     | 在list的末尾添加一个元素       |
| Lst1.push_front()    | 在list的头部添加一个元素       |
| Lst1.rbegin()        | 返回指向第一个元素的逆向迭代器 |
| Lst1.remove()        | 从list删除元素                 |
| Lst1.remove_if()     | 按指定条件删除元素             |
| Lst1.rend()          | 指向list末尾的逆向迭代器       |
| Lst1.resize()        | 改变list的大小                 |
| Lst1.reverse()       | 把list的元素倒转               |
| Lst1.size()          | 返回list中的元素个数           |
| Lst1.sort()          | 给list排序                     |
| Lst1.splice()        | 合并两个list                   |
| Lst1.swap()          | 交换两个list                   |
| Lst1.unique()        | 删除list中重复的元素           |

# 4. 链表操作

## 4.1. 插入
```c++
if(!head){
    // 空表插入
    head = tempNew;
}else if(value <= head -> val){
    //插入头部
    tempNew->next = head;
    head = tempNew;
}else{
    //在中间插入
    Node* p = head;
    while(p -> next != NULL && value > p->next->value){
        p = p -> next;
    }
    tempNew->next = p -> next;
    p -> next = tempNew;
}
```

## 4.2. 删除
```c++
if( value == head->value){
    head = head->next;
    delete cur;
}else{
    while(cur -> next != NULL && cur -> next -> value != value){
        cur = cur -> next;
    }
    Node* needDel = cur -> next;
    cur -> next = needDel -> next;
    delete needDel;
}
```

# 5. 其他参考

<a href ="https://blog.csdn.net/fanyun_01/article/details/56881515"></a>