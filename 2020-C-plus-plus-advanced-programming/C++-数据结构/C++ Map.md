Map
---
1. map(正序默认是字典序): map.ﬁnd(y1)==m.end()
  + 没有y1这个key 直接m[y1]取出 value 逆序遍

```c++
map<int, int>::reverse_iterator iter;
for (iter = m.rbegin(); iter != m.rend(); iter++) {//逆序遍历
  if (iter->second != 0) {
    if (iter == m.rbegin()){
      cout << iter->second << "x^" << iter->first;
    }else{
      cout << " + " << iter->second << "x^" << iter->first;
    }
  }
}
```

2. 正序遍历
```c++
map<int,int>::iterator iter;
for (iter = m.begin();iter != m.end(); iter++){
  cout << iter->first << "-" << iter->second << endl;
}
```