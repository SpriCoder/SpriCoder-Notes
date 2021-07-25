```c++
#include<iostream>
#include<string>
#include<sstream>
#include<fstream>
using namespace std;
int main() {
    string str1;
    string str2;
    getline(cin, str1);
    getline(cin, str2);
    string str = str1 + "\n" + str2;
    std::ofstream f("D:\\answer\\answer.txt", std::ios::app);
    f << str << std::endl;
    f.close();
}
```

# 1. 考试注意事项
1. 多次扩容，嵌套操作
2. int输入可能导致内部 long long
