Union
---

1. 共享存储空间(三选一！)
```c++
union user{
  //从以下三个情况选择一种
    int ival;
    double dval;
    char cval;
}
```

<!-- TOC -->

- [1. 统一数据空间用两种操作方式进行操作](#1-统一数据空间用两种操作方式进行操作)
- [2. Union的另一种用法](#2-union的另一种用法)
- [3. 互斥赋值](#3-互斥赋值)
- [4. 结构和联合](#4-结构和联合)
- [5. 参考](#5-参考)

<!-- /TOC -->

# 1. 统一数据空间用两种操作方式进行操作
1. 常用于系统软件和嵌入式系统
2. 例子(将数组组合成矩阵)
```c++
double  _element[3][3];
int  i, j;
for (i=0;i<3;i++)
    for (j=0;j<3;j++)
         _element [i][j] = (i+1)*(j+1);

for ( i=0;i<3;i++){
  for ( j=0;j<3;j++)
    cout << _element [i][j] << "  ";
  cout << endl;
}
union  Matrix{
    struct
    {   double  _a11, _a12, _a13;
        double  _a21, _a22, _a23;
        double  _a31, _a32, _a33;
    };
    double _element[3][3];
};
//如果没有struct，那么布局会出现问题
Matrix m;
int  i, j;
for (i=0;i<3;i++)
    for (j=0;j<3;j++)
         m._element[i][j] = (i+1)*(j+1);
         //每个单元都有两个名称

for ( i=0;i<3;i++){
  for ( j=0;j<3;j++)
    cout << m._element[i][j] << "  ";
  cout << endl;
}
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/C++-数据结构/img/union/1.png)

# 2. Union的另一种用法
1. 例：定义数组, 存储100个图形(直线、矩形、圆)
```c++
struct Line{
  int x1, y1, x2, y2
};
struct Ellipse{
  int x, y, r; 
}；
struct Rectangle{
  int lef, top, rig, bot;
}
//第一种实现
Line figures_L[100];
Rectangle figures_R[100];
Ellipse firgures_E[100];
//过于浪费空间
//第二种实现
enum FIGURE_TYPE  {LINE, RECTANGLE, ELLIPSE};//使用标签来确认其类别
struct Line{
  FIGURE_TYPE t ;
  int x1, y1, x2, y2;
};
struct Ellipse{
  FIGURE_TYPE t; 
  int x, y, r; 
};
struct Rectangle{
  FIGURE_TYPE t;
  int left, top, rig, bot;
}
union FIGURE{
  FIGURE_TYPE t;//共享了第一块空间
	Line line;	
	Rectangle rect; 
	Ellipse ellipse;
};

FIGURE  figures[100];
void main()
{   input( figures, 100 );
    for (int i=0;i<100;i++)
         draw(figures[i]);
} 

//API：
void draw_line(int,int,int,int);
void draw_rect(int,int,int,int);
void draw_ellipse(int,int,int);
```

1. Union占据的空间:
  + 选中最大的空间进行共享
  + 注意最右边的t，这方便了我们的访问

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/C++-数据结构/img/union/2.png)
```c++
//多态性
void draw(FIGURE  figure){
  switch ( figure.t ){
    case LINE:
      draw_line(figure.line.x1, ……);
      break;
		case RECTANGLE:
      draw_rect(figure.rect.lef, ……);
      break;
		case ELLIPSE:
      draw_ellipse(figure.ellipse.x, ……);
      break;
	}
}
void input (Figure fig[],  int size){    
  int t;
  for (int k=0; k<size; k++){
    cin >> t;
    switch (t){
      case LINE:
        fig[k].type = LINE;
        cin >> fig[k].line.x1 >> fig[i].line.y1 >> fig[k].line.x2  >>  fig[i].line.y2;
        break;
      case RECTANGLE:   ……	
      case ELLIPSE:   …….
    }
  }
}
```

2. 如果要增加color和width
```c++
enum FIGURE_TYPE  {LINE, RECTANGLE, ELLIPSE};//使用标签来确认其类别
struct Line{
  FIGURE_TYPE t ;
  int color, int width;
  int x1, y1, x2, y2;
};
struct Ellipse{
  FIGURE_TYPE t;
  int color, int width; 
  int x, y, r; 
};
struct Rectangle{
  FIGURE_TYPE t;
  int color, int width;
  int left, top, rig, bot;
}
union FIGURE{
  FIGURE_TYPE t;//共享了第一块空间
  int color, int width;
	Line line;	
	Rectangle rect; 
	Ellipse ellipse;
};
```

![](https://spricoder.oss-cn-shanghai.aliyuncs.com/2020-C-plus-plus-advanced-programming/C++-数据结构/img/union/3.png)

3. C++不希望在运行时进行类型检查
  + 所有C++利用virtual func来进行实现

# 3. 互斥赋值
1. 在任何时刻，联合中只能有一个数据成员可以有值。当给联合中某个成员赋值之后，该联合中的其他成员就会变成为赋值状态

# 4. 结构和联合
1. 通过使用union完成和保证c++运行时的多态性

# 5. 参考
<a href = "https://blog.csdn.net/hou09tian/article/details/80816445">C++ 关于union的理解</a>