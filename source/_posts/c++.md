---
title: C++
date: 2017-02-14 11:48:58
categories: C++
tags: 
    - c++
---

# 简介
c++的诞生地是贝尔实验室，作者是比亚尼.斯特劳斯特录普博士。

## 应用场景

嵌入式，游戏编程，网络编程，系统编程

## 特点

快：运行速度快

省：节省内存资源

## c与c++关系

c是c++的一个子集，也就是说将c代码拷贝到c++的编译环境中编译时完全没问题的。

c++是从c的基础发展而来的

c语言是面向过程

c++支持面向过和面向对象

## HelloC++

```c++
#include <iostream> //包含c++标准输入输出库

using namespace std; //命名空间

int main()
{
    cout << "Hello c++" << endl; //输出,并换行
    return 0;
}
```

# 新特性

## 新增数据类型

| 语言   | 逻辑类型 | 真    | 假     |
| ---- | ---- | ---- | ----- |
| c    | 没提供  | 非0   | 0     |
| c++  | bool | true | false |

有什么好处，当我们使用c语言的时候，就这样使用

```c
void testCBool(){
    int flag=0;
    if (flag == 1) {
        //为真的时候执行
    } else {
        //为假执行
    }

}
```

而在c++中就这样使用

```c++
void testCppBool(){
    bool flag= true;
    if (flag) {
        //为真的时候执行
    } else {
        //为假执行
    }

}
```

## 初始化方法

### c语言

只有一种，叫复制初始化

int x=1024;

### c++

他提供了两种，一种是复制初始化(和c语言一样)，另一种是直接初始化。

int x(1024);

## 随用随定义

C语言：所以变量定义必须位于函数体的最前面

c++:所有变量随用随定义

```c++
void testCDefinVar(){
    int v1=3;
    int v2=4;

    v1=v1+2;
    v2=v2+v1;
}

void testCppDefinVar(){
    int v1=3;
    v1=v1+2;
    
    int v2=4;
    v2=v2+v1;
}
```

# 输入输出

在c++中scanf用cin代替，printf用cout代替

## cout

cout<<x<<endl;

cout<<"x+y="<<x+y<<endl;

cout<<x,y,z<<endl; //错误

## cin

cin>>x;

cin>>x>>y;

## 优势

不关注暂未符，不关心数据类型，所以不易出现问题。

## 练习

```c++
int main()
{
    //1.提示输入一个整数,并将该整数用8,10,16进制打印
    //2.提示输入一个布尔值(0,1),并以布尔的方式打印
    cout<<"请输入一个整数:"<<endl;
    int x=0;
    cin>>x;
    cout<<oct<<x<<endl;
    cout<<dec<<x<<endl;
    cout<<hex<<x<<endl;

    cout<<"请输入一个布尔值(0,1):"<<endl;
    bool y= false;
    cin>>y;

    cout<<boolalpha<<y<<endl;

    return 0;
}
```

# 命名空间

划片取名字。

## 为什么要有名称空间

防止命名冲突

## 练习：模拟c公司购买了a,b两家公司的软件

```c++
using namespace std; //命名空间

//a公司代码
namespace A
{
    int x=1;
    void fun(){
        cout<<"A"<<endl;
    }
}

namespace B
{
    int x=2;
    void fun(){
        cout<<"B"<<endl;
    }
    void fun2(){
        cout<<"2B"<<endl;
    }
}

using namespace B;

int main()
{
    //使用这两个公司的代码
    cout<<A::x<<endl;

    //因为上面使用了命名空间b,所以从这里找
    fun();
    fun2();

    return 0;
}
```

## 练习：最大值和最小值

```c++
#include <iostream> //包含c++标准输入输出库

using namespace std; //命名空间


namespace CompA{
    //定义一个函数,找出整型数组中的最大值,最小值
    int getMaxOrMin(int *arr,int count,bool isMax)
    {
        int temp=arr[0];

        for (int i = 1; i < count; ++i) {
            if (isMax) {
                if (temp < arr[i]) {
                    temp=arr[i];
                }
            } else {
                if (temp > arr[i]) {
                    temp=arr[i];
                }
            }
        }

        return temp;
    }
}



int main()
{

    int arr[]={1,4,2,8};
    bool  isMax= false;
    cin>>isMax;
    cout<<CompA::getMaxOrMin(arr,4,isMax)<<endl;
    return 0;
}
```

# c++引用(别名)

引用就是变量的别名。不能只有别名。

## 基本类型

```c++
#include <iostream> //包含c++标准输入输出库

using namespace std; //命名空间

int main()
{

    //定义别名,是在变量名前加&
    int a=10;

    int &b=a;

    b=20;
    cout<<a<<endl; //20

    a=30;
    cout<<b<<endl; //30

    return 0;
}
```

## 结构体

```c++
typedef struct {
    int x;
    int y;
}Point;

int main()
{

    Point p;

    Point &p1=p;

    p1.x=10;
    p1.y=20;

    cout<<p.x<<","<<p.y<<endl;

    return 0;
}
```

## 指针

```c++
int main()
{


    int a=3;
    int *p=&a;

    int *&q=p;

    *q=5; //由于q是p的别名,所以*q和*p都是访问的a

    cout<<a<<endl; //5
    return 0;
}
```

## 函数

使用别名交换两个变量的值，如果是在c中，只能使用指针

```c++
#include <iostream> //包含c++标准输入输出库

using namespace std; //命名空间

void swap(int &a,int &b); //函数原型声明

int main()
{

    int x=10;
    int y=20;
    cout<<x<<","<<y<<endl; //10,20

    swap(x,y);

    cout<<x<<","<<y<<endl; //20,10
    return 0;
}

void swap(int &a,int &b){
    int c=a;
    a=b;
    b=c;
}
```

# const

控制变量的值是否可以改变。

## 基本类型

```c++
const int x=3;//常量，不能改变x的值
```

## 指针

```c++
//功能等价
const int *p =NULL;
int const *p=NULL;

int * const p = NULL;

//等价
const int * const p=NULL;
int const * const p =NULL;
```

```c++
int x=3;
const int *p=&x;

int y=10;
p=&y; //正确，因为const修饰的是*p，也就是说不能改变*p的值
//*p=4; //错误
```

```c++
int x=3;
int * const p=&x;

int y=10;
//p=&y;//错误，因为const修饰的是p
```

```c++
const int x=3;
const int * const p=&x;
//p=&y; //错误，是因为int *后面的const修饰符
//*p=4;//错误，是int *前面的修饰符
```

## 引用

```c++
int x=3;
const int &y=x;
x=10;//正确
//y=30;//错误，因为const修饰的是y
```

示例：

```c++
const int x=3;
x=5; //错误

int x=3;
const int y=x;
y=5;//错误

int x=3;
const int *y=&x;
*y=5;

int x=3,z=4;
int * const y=&x;
y=&z;//错误

const int x=3;
const int &y=x;
y=5;//错误

const int x=3;
int *y=&x; //错误，因为x是不可以，但我们定义的y指针是可变的，编译器报错,这样改const int *y=&x;

//这样没问题，是因为用小权限接收大权限是可以的
int x=3;
const int *y=&x;
```

## 函数

```c++
void fun(const int &a, const int &b){
    a=10;
    b=20;
}
```

用const修饰了，里面就不能改变变量(常量)的值了

# 函数新特性

## 函数参数默认值

```c++
//声明的时候写默认值
void fun(int i,int j=5,int k=1);

//定义的时候不写,因为写了,有些编译器报错
void fun(int i,int j,int k){

}
```

示例：

```c++
void fun(int i=10,int j=20);

int main(){
    fun();
    fun(100);
    fun(200,300);

//    10,20
//    100,20
//    200,300
    
    return 0;
}

void fun(int i,int j){
    cout<<i<<","<<j<<endl;
}
```



## 函数重载

在相同作用域中，函数名相同，参数个数或类型不一样，叫重载。

```c++
//生成的函数名为getMax_int_int
int getMax(int x,int y){

    return 0;
}

//生成的函数名为getMax_double_double
int getMax(double x, double y){

    return 0.0;
}
```

## 内联函数

普通函数执行流程：

main函数-调用fun方法的过程：

先找到fun函数的入口地址，然后准备参数，跳转到改函数地址，开始执行，执行完了以后处理返回值，跳转到main函数的位置，继续执行main函数。



内联函数：

编译时将函数体代码和实参代替函数的调用语句。

实例：

```c++
inline int max(int a,int b){
    if (a > b) {
        return a;
    } else {
        return b;
    }
}

int main(){
    int x=10;
    int y=20;

    int m=max(x,y);

    cout<<m<<endl;

    return 0;
}
```

相当于

```c++
int main(){
    int x=10;
    int y=20;

    int m=0;

    //max函数的展开代码
    int a=x;
    int b=y;

    if (a > b) {
        m= a;
    } else {
        m= b;
    }

    cout<<m<<endl;

    return 0;
}
```

问：为什么所以函数不都使用成内联函数呢？

1.内联是编译器决定的，也就是说你全加上，有可能他没有编译为内联

2.逻辑简单，调用频繁的建议使用

3.如果内联函数写成了递归，就无法成为内联函数了

# 内存管理

内存的本质是：资源

谁掌控内存资源：操作系统

我们能做什么：申请/归还

## 申请和是否内存运算符

申请内存:new

释放内存：delete

```c++
//int *p=new int(10);
//还可以这样
int *p=new int;
if (NULL!=p) {
    *p=20;
    
    cout<<*p<<endl;
    
    delete p;
    p=NULL;
}
```

```c++
//块内存的申请和释放
int *p=new int[100];
if (NULL!=p) {
    p[0]=20;
    p[1]=10;

    cout<<p[0]<<","<<p[1]<<endl;

    delete []p;
    p=NULL;
}
```

## 实例：拷贝字符串

```c++
#include <string.h>
#include <iostream>
using namespace std;
int main(void)
{
    //在堆中申请100个char类型的内存
    char *str = new char[100];
    //拷贝Hello C++字符串到分配的堆中的内存中
    strcpy(str, "Hello C++");
    //打印字符串
    cout<<str<<endl;
    //释放内存
    delete []str;
    str=NULL;
	return 0;
}
```

# 模板

