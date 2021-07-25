C++ 输入输出
---

<!-- TOC -->

- [1. I/O](#1-io)
  - [1.1. 标准库对象](#11-标准库对象)
- [2. 输入](#2-输入)
  - [2.1. 输入原理](#21-输入原理)
  - [2.2. cin](#22-cin)
    - [2.2.1. 数组输入](#221-数组输入)
    - [2.2.2. 解决格式化输入问题](#222-解决格式化输入问题)
    - [2.2.3. get方法](#223-get方法)
    - [2.2.4. cin.getline()](#224-cingetline)
    - [2.2.5. getline()](#225-getline)
  - [2.3. cin异常处理机制](#23-cin异常处理机制)
    - [2.3.1. 标志位](#231-标志位)
    - [2.3.2. rdstate()](#232-rdstate)
    - [2.3.3. bool ios::fail()const](#233-bool-iosfailconst)
    - [2.3.4. bool ios::bad() const](#234-bool-iosbad-const)
    - [2.3.5. bool ios::good()const](#235-bool-iosgoodconst)
    - [2.3.6. voidios::clear(iostate _State=goodbit)](#236-voidioscleariostate-_stategoodbit)
    - [2.3.7. void ios::setstate(iostate_State)](#237-void-iossetstateiostate_state)
    - [2.3.8. 例子](#238-例子)
    - [2.3.9. basic_istream&ignore(streamsize _Count = 1, int_type _Delim = traits_type::eof());](#239-basic_istreamignorestreamsize-_count--1-int_type-_delim--traits_typeeof)
    - [2.3.10. 丢弃一个字符](#2310-丢弃一个字符)
    - [2.3.11. 清除缓冲区](#2311-清除缓冲区)
  - [2.4. 函数输出](#24-函数输出)
    - [2.4.1. getchar()](#241-getchar)
    - [2.4.2. putchar()](#242-putchar)
- [3. 输出](#3-输出)
  - [3.1. 标准输出流 cout](#31-标准输出流-cout)
    - [3.1.1. 格式化输出](#311-格式化输出)
  - [3.2. 使用命名空间std](#32-使用命名空间std)
  - [3.3. 函数输出](#33-函数输出)
- [4. 控制符](#4-控制符)
- [5. 不同类别的I/O处理](#5-不同类别的io处理)
  - [5.1. I/O流库的三类输入/输出](#51-io流库的三类输入输出)
  - [5.2. 重定向](#52-重定向)
  - [5.3. 对操作符<<和>>的重载](#53-对操作符和的重载)
  - [5.4. IO处理](#54-io处理)
  - [5.5. Virtualizing constructors 虚拟化构造器](#55-virtualizing-constructors-虚拟化构造器)
- [6. 读文件](#6-读文件)
- [7. 泛型用一个方法输出double和int](#7-泛型用一个方法输出double和int)
- [8. 参考](#8-参考)

<!-- /TOC -->

# 1. I/O
1. 输入输出流:包含在头文件`<iostream>`中
2. 开头需要进行`#include<iostream>`

## 1.1. 标准库对象
对象|功能
--|--
istream:cin|处理输入
ostream:cout|处理输出
ostream:cerr|处理错误
ostream:clog|保证log

# 2. 输入

## 2.1. 输入原理
1. 程序的输入都键入一个缓冲区，即输入缓冲区。
2. 键盘输入结束后，会将数据存入缓冲区，之后cin函数直接从输入缓冲区取数据
3. 问题在于:缓冲区中有残留数据的时候，cin输入流直接从缓冲区拿数据。

## 2.2. cin
1. `>>`是流提取符，以空格，\t(Tab),\n(回车)为终止
2. 往往使用来赋值给变量
3. cin的变量类型可以为int、float、char、char*、string等诸多类型。

### 2.2.1. 数组输入
```c++
//已知长度数组读入
for(int i = 0;i < n; i++){
    cin >> nums[i]
}
//未知长度数组读入
while(cin >> n){//如果没有数字输入则会为NULL
    nums[i] = n;
    i ++;
}
```

### 2.2.2. 解决格式化输入问题
```c++
//Ctrl + Z 表示输入结束
//读取(0,0),(1,1)
char c;//用来读取无用的
int x1,x2,y1,y2
cin >> c >> x1 >> c >> x2 >> c >> c >> c >> y1 >> c >> y2 >> c >> c;(这个很重要)
```

### 2.2.3. get方法
```c++
int get();
istream& get(char& c);
istream& get(char* s, streamsize n);
istream& get(char* s, streamsize n, char delim);
istream& get(streambuf& sb);
istream& get(streambuf& sb, char delim);
```

1. 结束符默认为enter，结束字符串的读写
2. 字符串最后一个为`\0`，并且对空格不敏感。
3. get方法**并不会将结束符从缓冲区丢弃**：务必注意是结束符！未必是回车。

```c++
//按照字符读取
cin.get(x);
cin.get(y);//\n也可以读取到
//cin.get == c语言中的getchar()

//按照字符串读取
char ch1,ch2[10];
cout<<"请输入字符串："<<endl;
cin.get(ch2,6);//在不遇到结束符的情况下，最多可接收6-1=5个字符到ch2中，注意结束符为默认Enter
cin.get(ch1);//或ch1 = cin.get();      
out<<ch2<<endl;
cout<<ch1<<"\n"<<(int)ch1<<endl;
```

1. 直接回车在上面程序中会出现错误输出(越界)，处理方法`cin.clear()`:但是不会清理终止符。

```c++
//调整结束符
cin.get(ch, 3, 'a');// 结束符为'a'，直接输入a(enter)
cin.get(ch2);

//注意cin.get()的返回值的问题
cin.get(ch, 3, 'a'); //此处输入a(enter)
ch2 = cin.get(); //注意与cin.get(ch2)不同
cout << ch2 << ' ' << (int)ch2 << endl;

//cin.get()
cin.get();//用来舍弃输入中不需要的字符(包含回车)，用来弥补不足，用来避免下次读入的时候再次读入
```

### 2.2.4. cin.getline()
1. `cin.getline(字符数组名,接收长度，结束符)`
2. cin.get()超长后不会影响cin的操作，而cin.getline()如果超长会导致之后cin的错误。

### 2.2.5. getline()
1. `getline(istream is,string str,结束符)`
```c++
getline(cin,str);
```

## 2.3. cin异常处理机制

### 2.3.1. 标志位
1. 定义在IOS类中
2. 他们不是储存异常状态常量，而是对应状态为的掩码。

名称|二进制显示|功能
--|--|--
failbit|001|输入(输出)流出现致命错误，不可挽回
eofbit|010|已经到达文件尾
badbit|100|输入(输出)流出现非致命错误，可挽回
goodbit|000|流状态完全正常，各异常标志位都为0

```c++
cout << ios::failbit << endl;
cout << ios::eofbit << endl;
cout << ios::badbit << endl; 
cout << ios::goodbit << endl;
```

### 2.3.2. rdstate()
1. rdstate():获取标志变量的值
```c++
void TestFlags( ios& x ) // 获得x流的三个标志位状态  
{  
    cout << ( x.rdstate( ) & ios::badbit ) << endl;  
    cout << ( x.rdstate( ) & ios::failbit ) << endl;  
    cout << ( x.rdstate( ) & ios::eofbit ) << endl;  
    cout << endl;  
}  
```

### 2.3.3. bool ios::fail()const
- 1 or true if rdstate & failbit is nonzero, otherwise 0 or false. (引用msdn)
- 其中rdstate即通过rdstate()取得的标识变量的值，与failbit相与，即取得failbit标志位的值，如果结果非零则放回true，否则返回false。即该函数返回failbit的状态，将标志位状态通过bool值返回。

### 2.3.4. bool ios::bad() const
- 1 or true if rdstate & badbit is nonzero; otherwise 0. (引用msdn)
与fail()相似。

### 2.3.5. bool ios::good()const
- 1 or true if rdstate == goodbit (no state flags are set), otherwise, 0 orfalse. (引用msdn)
改函数取goodbit的情况，即三个标志位都0(即没有任何异常情况)时返回true，否则返回false。

### 2.3.6. voidios::clear(iostate _State=goodbit)
- 该函数用来重置标识变量，_State是用来重置的值，默认为goodbit，即默认时将所有标志位清零。用户也可以传进参数，如：clear(failbit)，这样就将标识变量置为failbit(即：001)。
- 我们一般是用它的默认值，当cin出现异常，我们用该函数将所有标志位重置。如果cin出现异常，没有重置标志的话没法执行下一次的cin操作。如上一节的程序2的测试二为什么第二次输入操作没有执行？程序8中 cin>>ch 为什么没有执行？都是这个原因！！！
所以经常在程序中使用 cin.clear(), 为了重置错误标志！

### 2.3.7. void ios::setstate(iostate_State)
1. 这个函数也是用来设置标识变量的，但与clear()不同。clear()是将所有标志清零，在置以参数新的标志。而该函数不清零其他的标志，而只是将参数对应的标志位置位。这个函数不是经常使用，这里不再赘述。

### 2.3.8. 例子
```c++
#include<iostream>  
using namespace std;  
int main (){  
    char ch, str[20];  
    cin.getline(str, 5);  
    cout<<"flag1:"<<cin.good()<<endl;   // 查看goodbit状态，即是否有异常  
    cin.clear();                        // 清除错误标志  
    cout<<"flag1:"<<cin.good()<<endl;   // 清除标志后再查看异常状态  
    cin>>ch;   
    cout<<"str:"<<str<<endl;  
    cout<<"ch :"<<ch<<endl;  
    return 0;  
}
//测试输入：
//12345[Enter]
//输出：
//flag1:0 // good()返回false说明有异常
//flag2:1 // good()返回true说明，clear()已经清除了错误标志
//str:1234
//ch :5
```
- 【分析】程序执行结束还是只执行了一次读操作，cin>>ch还是没有从键盘读取数据，但是与程序8中不同，这里打印了ch的值为'5'，而且在cin>>ch之前已经清楚了错误标志，也就是cin>>ch的读操作实际上执行了。这就是前面讲的cin读取数据的原理：它是直接从输入缓冲区中取数据的。此例中，第一次输入"12345",而getline(str, 5)根据参数'5'只取缓冲区中的前4个字符，所以str取的是"1234"，而字符'5'仍在缓冲区中，所以cin>>ch直接从缓冲区中取得数据，没有从键盘读取数据！
- 也就是当前一次读取数据出错后，如果缓冲区没有清空的话，重置错误标志还不够！要是能将缓冲区的残留数据清空了就好了哦！下面我们再来看一个很重要的函数！

### 2.3.9. basic_istream&ignore(streamsize _Count = 1, int_type _Delim = traits_type::eof());
1. Causes a number of elements to be skipped from the current readposition
2. Parameters:
   1. _Count, The number of elements to skip from the current read position.
   2. _Delim, The element that, if encountered before count, causes ignore to returnand allowing all elements after _Delim to be read. (引用msdn)\
3. 这个函数用来丢弃输入缓冲区中的字符，第一参数定义一个数，第二个参数定义一个字符变量。下面解释一下函数是怎样执行的：函数不停的从缓冲区中取一个字符，并判断是不是_Delim，如果不是则丢弃并进行计数，当计数达到_Count退出，如果是则丢弃字符退出。例：cin.ignore(5, 'a'); 函数将不断从缓冲区中取一个字符丢弃，直到丢弃的字符数达到5或者读取的字符为'a'。下面我们看个程序例子：

```c++
#include <iostream>  
using namespace std;
int main(){
	char ch;
	cin.ignore(5, 'a');
	cin.get(ch);
	cout << (int)ch << endl;
	return 0;
}
```

4. 例子见参考三

### 2.3.10. 丢弃一个字符
1. `cin.ignore()`:删除缓冲区的第一个字符

### 2.3.11. 清除缓冲区
1. `cin.ignore(1024,'\n');`
2. `cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');`

## 2.4. 函数输出

### 2.4.1. getchar()
1. getchar()；获得一个字符
2. 可以读取到空格\n等等的字符。

### 2.4.2. putchar()
1. putchar()；输出一个字符

# 3. 输出

## 3.1. 标准输出流 cout
1. <<流插入符
2. `std::endl`:换行，可以输出一个或者多个，等价于`\n`

### 3.1.1. 格式化输出
```c++
#include<iomanip>
cout << hex << 10 << "" << oct << 8;//16进制和8进制
//hex 设定后，直接将后面所有的进行转换，知道再次设定
//hex 16
//dec 10
//oct 8
cout << setorecison(4) << 1.11111;//4位小数
cout << setw(6) << right << 10;//6位右对齐
cout << year << '-' << setw(2) << setfill('0') << month << ‘-’ << std::setw(2) << std::setfill('0') << day;
//填充
```

## 3.2. 使用命名空间std
1. using namespace std;来直接使用
2. cin,cout是C++标准库内置函数但不是关键字。

## 3.3. 函数输出
1. scanf("%d",&a);
2. printf("%d",a);

# 4. 控制符
控制符|名称|作用
--|--|--
endl|换行符|换行

# 5. 不同类别的I/O处理
1. 基于函数库的I/O
2. 基于类库的I/O

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/img/io/1.png)

## 5.1. I/O流库的三类输入/输出
1. 控制台I/O:标准I/O设备(cin、cout、cerr、clog)
2. 文件I/O
3. 字符串I/O

## 5.2. 重定向
```c++
ifstream in ("in. txt");
streambuf * cinbuf = cin. rdbuf ();//save old buf
cin. rdbuf ( in. rdbuf ());//redirect cin to in. txt !
ofstream out (" out. txt ");
streambuf * coutbuf = cout. rdbuf (); //save old buf
cout. rdbuf ( out. rdbuf ()); //redirect cout to out. txt !
string word;
cin >> word; //input from the file in. txt 
cout << word << " ";//output to the file out. txt
cin. rdbuf ( cinbuf );//reset to standard input again
cout. rdbuf ( coutbuf ); //reset to standard output again
cin >> word; //input from the standard input
cout << word; //output to the standard input
```

## 5.3. 对操作符<<和>>的重载
1. 对自定义类的对象的I/O
2. 全局(友元)函数重载

```c++
class CPoint2D{
    double x, y;
    public:
        friend ostream& operator << (ostream&, CPoint2D &);
};
//全局函数
ostream& operator << (ostream& out,  CPoint2D& a){//引用类型保证能递归显示
    out << a.x << "," << a.y << endl;
	return out;
}
CPoint2D a;
cout << a;
class CPoint3D: public CPoint2D
{   double z;
    
}
CPoint3D b;
cout << b;//只显示b.x和b.y，而没显示b.z
class CPoint3D: public CPoint2D
{   double z;
    friend ostream& operator << (ostream &, CPoint3D &);
}
ostream& operator << (ostream& out,  CPoint3D & b){
    out << b.x << "," << b.y <<","  << b.z << endl;
	return out;
}
//问题:3D对象被2D指针指向，cout调用了2D的版本，解决:虚化
```

## 5.4. IO处理
```c++
//解决上面的问题
class CPoint2D{
    double x, y;
	public:
	    virtual void display(ostream& out){
            out << x << "," << y << endl;
        }
};
//全局函数的多态，使用虚函数
ostream& operator << (ostream& out,  CPoint2D &a){//虚函数保证必然会调用对象对应的实际类型的版本的对应方法
    a.display(out);
    return out;
}

class CPoint3D: public CPoint2D{
    double z;
    public:
        void display(ostream& out){   
            CPoint2D::display();
            out << ","<< z << endl;  }
};
```

## 5.5. Virtualizing constructors 虚拟化构造器
1. 虚函数
2. 构造器

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/img/io/2.png)

```c++
class NLComponent {…};
class TextBlock :public NLComponent {…};
class Graphic :public NLComponent {…};
class NewsLetter{
    public:
        NewsLetter(istream& str){
            while (str)
                components.push_back(readComponent(str));
        }
	    static NLComponent * readComponent(istream& str);
        NewsLetter(const NewsLetter& rhs){//拷贝构造函数
            for (list<NLComponent *>::iterator it=rhs.component.begin();it != rhs.component.end(); ++it )
                //期望有一个虚函数可以拷贝自己
                component.push_back();//new TextBlock? Graphic?
        }
    private:
	    list<NLComponent *> components;
}
//虚化构造器
virtual NLComponent *clone() const = 0;
//原型模式:添加clone
virtual TextBlock *clone() const{
    return new TextBlock(*this);
}
virtual Graphic  *clone() const{
    return new Graphic (*this);
}
NewsLetter::NewsLetter( const NewsLetter& rhs){
    for ( list<NLComponent *>::iterator it=rhs.component.begin();
		it != rhs.component.end(); ++it )
        component.push_back((*it)->clone());
}
//typeid(*it)==typeid(TextBlock)判断对象的类型

//Question
class BST {};
class BalancedBST: public BST {};
void printBSTArray(ostream& s, const BST array[], int numElements){
    for (int i=0; i < numElements; i++)
        s << array[i];
}
BalancedBST bBSTArray[10];
printBSTArray(cout, bBSTArray, 10);
//问题是?array[i]是指针算法的缩写，数组每次偏移地址是sizeof(BST)，而不是sizeof(BalancedBST)，会出现问题。
```

# 6. 读文件
```c++
ifstream infile("file_name");
if (!infile.is_open()){
    cout << "未成功打开文件" << endl;
}
int arr[26] = { 0 };
char c;
infile >> c;
while (!infile.eof()) {
    //do something
    infile >> c;
}
```

# 7. 泛型用一个方法输出double和int
1. 如果`(a - int(a)) > 1E-7`:则认为是double
2. 否则为int

# 8. 参考
1. <a href = "https://blog.csdn.net/a3192048/article/details/80303547">cin、cin.get()、cin.getline()、getline()的区别</a>