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

## 常对象成员和常成员函数

这样声明

```c++
const Coordinate m_pCoorA;

//也可以这样
Coordinate const m_pCoorA;
```

改进上面的例子，将Line其中的一个成员改为常成员，并添加一些常成员函数。

Coordinate.hpp

```c++
#ifndef Coordinate_hpp
#define Coordinate_hpp

class  Coordinate{
    
    
public:
    Coordinate(int x,int y);
    ~Coordinate();
    int getX() const; //因为该类，有可能在其他类声明了常成员，所以要定义常成员函数，不然无法编译，也就是说在该函数中不能改变常成员的值
    int getY() const;
private:
    int m_iX;
    int m_iY;
};

#endif /* Coordinate_hpp */
```

Coordinate.cpp

```c++
#include <iostream>

#include "Coordinate.hpp"

using namespace std;

Coordinate::Coordinate(int x,int y){
    m_iX=x;
    m_iY=y;
    cout<<"Coordinate(int x,int y)"<<endl;
}

Coordinate::~Coordinate(){
    cout<<"~Coordinate"<<endl;
}

int Coordinate::getX() const{
    return m_iX;
}

int Coordinate::getY() const{
    return m_iY;
}
```

Line.hpp

```c++
#ifndef Line_hpp
#define Line_hpp

#include "Coordinate.hpp"

class Line {
    
    
public:
    Line(int x1,int y1,int x2,int y2);
    ~Line();
    
    //这两个函数重载
    void printInfo();
    void printInfo() const;
private:
    const Coordinate m_pCoorA;
    Coordinate m_pCoorB;
};

#endif /* Line_hpp */
```

Line.cpp

```c+
#include <iostream>

#include "Line.hpp"

using namespace std;

Line::Line(int x1,int y1,int x2,int y2):m_pCoorA(x1,y1),m_pCoorB(x2,y2){
    cout<<"Line()"<<endl;
}

Line::~Line(){
    
    cout<<"~Line()"<<endl;
}

void Line::printInfo(){
    cout<<"printinfo()"<<endl;
    cout<<m_pCoorA.getX()<<","<<m_pCoorA.getY()<<endl;
    cout<<m_pCoorB.getX()<<","<<m_pCoorB.getY()<<endl;
}

void Line::printInfo() const{
    cout<<"printinfo() const"<<endl;
    cout<<m_pCoorA.getX()<<","<<m_pCoorA.getY()<<endl;
    cout<<m_pCoorB.getX()<<","<<m_pCoorB.getY()<<endl;
}
```

测试

```c++
//这样就调用到了const函数
const Line line(1,2,3,4);
line.printInfo();
```

## 对象常指针和对象常引用

```c++
Line line(1,2,3,4);

const Line &l1=line; //常对象引用
const Line *l2=&line; //常对象指针
```

综合案例

```c++
#include <iostream>
using namespace std;
class Coordinate
{
    
public:
	Coordinate(int x, int y)
	{
		// 设置X,Y的坐标
		m_iX=x;
        m_iY=y;
	}
    // 实现常成员函数
	void printInfo() const
	{
	    cout<<"("<<m_iX<<","<<m_iY<<")"<<endl;
	}
public:
	int m_iX;
	int m_iY;
};


int main(void)
{
	const Coordinate coor(3, 5);

	// 创建常指针p
	const Coordinate *p=&coor;
    // 创建常引用c
    const Coordinate &c=coor;
	
	coor.printInfo();
	p->printInfo();
	c.printInfo();  
	
	return 0;
}
```

输出：

```shell
(3,5)
(3,5)
(3,5)
```



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

类

定义类

    class Point {

    public:
        int x;
        int y;
        void printX(){
            cout<<x<<endl;
        }
        void printY(){
            cout<<y<<endl;
        }
    };

实例化对象

在栈上创建对象:

    //通过栈的方式实例化对象
    Point point;
    point.x=10;
    point.y=20;
    
    point.printX();
    point.printY();

在堆上创建对象：

    Point *point=new Point();
    if (NULL==point) {
        //实例化对象失败
        return 0;
    }
    
    point->x=100;
    point->y=200;
    point->printX();
    point->printY();

字符串

初始化方式

    string s1;
    string s2("abc");
    string s3(s2);
    string s4(3,'c');
    
    cout<<s1<<endl;
    cout<<s2<<endl;
    cout<<s3<<endl;
    cout<<s4<<endl;

常用函数

  方法名    	作用                  
  s.empty	字符串为空，返回true，否则false
  s.size 	字符的个数               
  s[n]   	返回s中n位置的字符          
  s1+s2  	连接字符串               
  s1=s2  	将s1的内容替换为s2的副本      
  v1==v2 	内容相等，返回true         
  v1!=v2 	内容不相等，返回true        

    string s1="hello";
    string s2("world");
    string s3=s1+s2;
    string s4="hello" +s2;
    string s5="hello"+s2+"world";
    
    //    string s6="hello"+"world"; //这种方式错误，只有一端是一个变量才可以，而java中则可以

实例：读取用户姓名

    cout<<"请输入用户名："<<endl;
    string name;
    getline(cin, name);
    
    cout<<name<<endl;
    
    if (name.empty()) {
        cout<<"输入的姓名不能为空"<<endl;
        return 0;
    }
    
    cout<<"Hello "+name<<endl;
    cout<<"你的名字长度："<<name.size()<<endl;
    cout<<"你的名字首字母是："<<name[0]<<endl;
    
    if ("admin"==name) {
        cout<<"你是一个管理员"<<endl;
    }

封装

他的好处是保护数据不被恶意篡改。下面模拟一个用户的实例化，然后打印用户信息：

    #include <iostream>
    #include <string>
    
    using namespace std;
    
    class Student {


    public:
        void setName(string _name){
            m_strName=_name;
        }
        string getName(){
            return m_strName;
        }
        void setGender(string _gender){
            m_strGender=_gender;
        }
        string getGender(){
            return m_strGender;
        }
        int getScore(){
            return m_iScore;
        }
        
        void initScore(){
            m_iScore=0;
        }
        
        void study(int _score){
            m_iScore+=_score;
        }
        
    private:
        string m_strName;
        string m_strGender;
        int m_iScore;
    };
    
    int main(){
        Student stu;
        
        stu.initScore();
        stu.setName("张三");
        stu.setGender("男");
        stu.study(5);
        stu.study(3);
        
        cout<<stu.getName()<<" "<<stu.getGender()<<" " <<stu.getScore()<<endl;


        return 0;
    }

类外定义

一般情况下，我们将类的声明定义在一个文件：

Student.hpp

    #ifndef Student_hpp
    #define Student_hpp
    
    #include <stdio.h>
    #include <string>
    
    using namespace std;
    
    //定义类
    class Student {


    public:
        void setName(string _name);
        string getName();
        void setGender(string _gender);
        string getGender();
        void setAge(int _age);
        int getAge();
        void teach();
    private:
        string m_strName;
        string m_strGedner;
        int m_iAge;
    };
    
    #endif /* Student_hpp */

然后在另一个文件实现：

Student.cpp

    #include <iostream>

    #include "Student.hpp"

​    
​    
    //实现类
    void Student::setName(string _name){
        m_strName=_name;
    }
    string Student::getName(){
        return m_strName;
    }
    void Student::setGender(string _gender){
        m_strGedner=_gender;
    }
    string Student::getGender(){
        return m_strGedner;
    }
    void Student::setAge(int _age){
        m_iAge=_age;
    }
    int Student::getAge(){
        return m_iAge;
    }
    void Student::teach(){
        cout<<"现在上课了..."<<endl;
    }

内存分区

栈区：int x=0；int *p=NULL;

堆区：int *p=new int[20];

全局区：存储全局变量以静态变量

常量区：string str="hello";

代码区：存储逻辑代码的二进制

构造函数

Teacher.hpp

在头文件里面定义构造函数

    #ifndef Teacher_hpp
    #define Teacher_hpp
    
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    class Teacher {


    public:
        //构造函数
        Teacher();
        Teacher(string name,int age=20);
        
        //成员函数
        void setName(string _name);
        string getName();
        void setAge(int _age);
        int getAge();
    private:
        string m_strName;
        int m_iAge;
    
    };
    
    #endif /* Teacher_hpp */

在实现文件里面实现构造函数：

    #include "Teacher.hpp"

​    
    Teacher::Teacher(){
        m_strName="jack";
        m_iAge=30;
        cout<<"Teacher()"<<endl;
    }
    Teacher::Teacher(string name,int age){
        m_strName=name;
        m_iAge=age;
        cout<<"Teacher(string name,int age)"<<endl;
    }
    
    void Teacher::setName(string _name){
        m_strName=_name;
    }
    string Teacher::getName(){
        return m_strName;
    }
    void Teacher::setAge(int _age){
        m_iAge=_age;
    }
    int Teacher::getAge(){
        return m_iAge;
    }

然后在实现文件里面就可以使用：

    #include "Teacher.hpp"

    int main(){

        Teacher t1;

        Teacher t2("zhangsan",10);

        Teacher t3("lisi");

        cout<<t1.getName()<<" "<<t1.getAge()<<endl;
        cout<<t2.getName()<<" "<<t2.getAge()<<endl;
        cout<<t3.getName()<<" "<<t3.getAge()<<endl;
        
        return 0;
    }

构造函数初始化列表

常量必须用初始化列表初始化。

Teacher.hpp

    #ifndef Teacher_hpp
    #define Teacher_hpp
    
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    class Teacher {


    public:
        //构造函数
        Teacher(string name="jack",int age=20,int max=100);
        
        //成员函数
        void setName(string _name);
        string getName();
        void setAge(int _age);
        int getAge();
    private:
        string m_strName;
        int m_iAge;
        const int m_iMax; //表示这个老师能带多少个学生，是一个常量只能初始化一次
    };
    
    #endif /* Teacher_hpp */

Teacher.cpp

    #include "Teacher.hpp"

​    
    Teacher::Teacher(string name,int age,int max):m_strName(name),m_iAge(age),m_iMax(max){
        //这里使用初始化列表
        cout<<"Teacher(string name,int age)"<<endl;
    }
    
    void Teacher::setName(string _name){
        m_strName=_name;
    }
    string Teacher::getName(){
        return m_strName;
    }
    void Teacher::setAge(int _age){
        m_iAge=_age;
    }
    int Teacher::getAge(){
        return m_iAge;
    }

main.cpp

    Teacher t1;

    Teacher t2("zhangsan",10);

    Teacher t3("zhangsan",150);

​    
    cout<<t1.getName()<<" "<<t1.getAge()<<endl;
    cout<<t2.getName()<<" "<<t2.getAge()<<endl;
    cout<<t3.getName()<<" "<<t3.getAge()<<endl;

拷贝构造函数

如果没有定义，则系统默认生成一个。当采用直接初始化(赋值)或复制初始化时系统将自动调用，还有就是参数传递也会调用。

Teacher.hpp

    #ifndef Teacher_hpp
    #define Teacher_hpp
    
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    class Teacher {


    public:
        //构造函数
        Teacher(string name="jack",int age=20);
        //拷贝构造函数
        Teacher(const Teacher & tea);
        
        //成员函数
        void setName(string _name);
        string getName();
        void setAge(int _age);
        int getAge();
    private:
        string m_strName;
        int m_iAge;
       
    };
    
    #endif /* Teacher_hpp */

Teacher.cpp

    #include "Teacher.hpp"

​    
    Teacher::Teacher(string name,int age):m_strName(name),m_iAge(age){
        //这里使用初始化列表
        cout<<"Teacher(string name,int age)"<<endl;
    }
    
    Teacher::Teacher(const Teacher & tea){
        cout<<"Teacher(const Teacher & tea)"<<endl;
    }
    
    void Teacher::setName(string _name){
        m_strName=_name;
    }
    string Teacher::getName(){
        return m_strName;
    }
    void Teacher::setAge(int _age){
        m_iAge=_age;
    }
    int Teacher::getAge(){
        return m_iAge;
    }

main.cpp

    Teacher t1;

​    
    Teacher t2=t1;//会调用拷贝构造函数
    Teacher t3(t1);//会调用拷贝构造函数
    
    test(t1);

test是一个函数

    void test(Teacher t){
        t.setName("a");
        cout<<t.getName()<<endl;
    }

析构函数

1.没有定义则系统自动生成。

2.对象销毁时自动调用，目的是归还资源。

3.析构函数，没有返回值，没有参数，不能重载。

Teacher.hpp

    #ifndef Teacher_hpp
    #define Teacher_hpp
    
    #include <iostream>
    #include <string>
    
    using namespace std;
    
    class Teacher {


    public:
        //构造函数
        Teacher(string name="jack",int age=20);
        //拷贝构造函数
        Teacher(const Teacher & tea);
        
        //析构函数
        ~Teacher();
        
        //成员函数
        void setName(string _name);
        string getName();
        void setAge(int _age);
        int getAge();
    private:
        string m_strName;
        int m_iAge;
       
    };
    
    #endif /* Teacher_hpp */

然后实现析构函数

    #include "Teacher.hpp"

​    
    Teacher::Teacher(string name,int age):m_strName(name),m_iAge(age){
        //这里使用初始化列表
        cout<<"Teacher(string name,int age)"<<endl;
    }
    
    Teacher::Teacher(const Teacher & tea){
        cout<<"Teacher(const Teacher & tea)"<<endl;
    }
    
    Teacher::~Teacher(){
        cout<<"~Teacher()"<<endl;
    }
    
    void Teacher::setName(string _name){
        m_strName=_name;
    }
    string Teacher::getName(){
        return m_strName;
    }
    void Teacher::setAge(int _age){
        m_iAge=_age;
    }
    int Teacher::getAge(){
        return m_iAge;
    }

最后测试是否调用了析构函数

main.cpp

    Teacher t1; //这样方式声明的，会自动调用析构函数
    Teacher t2(t1); //这样方式声明的，会自动调用析构函数
    
    Teacher *t3 = new Teacher();
    delete t3; //在堆上创建的对象，必须手动调用


# 类

## 定义类

```c++
class Point {
    
public:
    int x;
    int y;
    void printX(){
        cout<<x<<endl;
    }
    void printY(){
        cout<<y<<endl;
    }
};
```

## 实例化对象

在栈上创建对象:

```c++
//通过栈的方式实例化对象
Point point;
point.x=10;
point.y=20;

point.printX();
point.printY();
```

在堆上创建对象：

```c++
Point *point=new Point();
if (NULL==point) {
    //实例化对象失败
    return 0;
}

point->x=100;
point->y=200;
point->printX();
point->printY();
```

# 字符串

## 初始化方式

```c++
string s1;
string s2("abc");
string s3(s2);
string s4(3,'c');

cout<<s1<<endl;
cout<<s2<<endl;
cout<<s3<<endl;
cout<<s4<<endl;
```

## 常用函数

| 方法名     | 作用                   |
| ------- | -------------------- |
| s.empty | 字符串为空，返回true，否则false |
| s.size  | 字符的个数                |
| s[n]    | 返回s中n位置的字符           |
| s1+s2   | 连接字符串                |
| s1=s2   | 将s1的内容替换为s2的副本       |
| v1==v2  | 内容相等，返回true          |
| v1!=v2  | 内容不相等，返回true         |

```c++
string s1="hello";
string s2("world");
string s3=s1+s2;
string s4="hello" +s2;
string s5="hello"+s2+"world";

//    string s6="hello"+"world"; //这种方式错误，只有一端是一个变量才可以，而java中则可以
```

## 实例：读取用户姓名

```c++
cout<<"请输入用户名："<<endl;
string name;
getline(cin, name);

cout<<name<<endl;

if (name.empty()) {
    cout<<"输入的姓名不能为空"<<endl;
    return 0;
}

cout<<"Hello "+name<<endl;
cout<<"你的名字长度："<<name.size()<<endl;
cout<<"你的名字首字母是："<<name[0]<<endl;

if ("admin"==name) {
    cout<<"你是一个管理员"<<endl;
}
```

# 封装

他的好处是保护数据不被恶意篡改。下面模拟一个用户的实例化，然后打印用户信息：

```c++
#include <iostream>
#include <string>

using namespace std;

class Student {
    
    
public:
    void setName(string _name){
        m_strName=_name;
    }
    string getName(){
        return m_strName;
    }
    void setGender(string _gender){
        m_strGender=_gender;
    }
    string getGender(){
        return m_strGender;
    }
    int getScore(){
        return m_iScore;
    }
    
    void initScore(){
        m_iScore=0;
    }
    
    void study(int _score){
        m_iScore+=_score;
    }
    
private:
    string m_strName;
    string m_strGender;
    int m_iScore;
};

int main(){
    Student stu;
    
    stu.initScore();
    stu.setName("张三");
    stu.setGender("男");
    stu.study(5);
    stu.study(3);
    
    cout<<stu.getName()<<" "<<stu.getGender()<<" " <<stu.getScore()<<endl;
    
    
    return 0;
}
```

# 类外定义

一般情况下，我们将类的声明定义在一个文件：

Student.hpp

```c++
#ifndef Student_hpp
#define Student_hpp

#include <stdio.h>
#include <string>

using namespace std;

//定义类
class Student {
    
    
public:
    void setName(string _name);
    string getName();
    void setGender(string _gender);
    string getGender();
    void setAge(int _age);
    int getAge();
    void teach();
private:
    string m_strName;
    string m_strGedner;
    int m_iAge;
};

#endif /* Student_hpp */
```

然后在另一个文件实现：

Student.cpp

```c++
#include <iostream>

#include "Student.hpp"



//实现类
void Student::setName(string _name){
    m_strName=_name;
}
string Student::getName(){
    return m_strName;
}
void Student::setGender(string _gender){
    m_strGedner=_gender;
}
string Student::getGender(){
    return m_strGedner;
}
void Student::setAge(int _age){
    m_iAge=_age;
}
int Student::getAge(){
    return m_iAge;
}
void Student::teach(){
    cout<<"现在上课了..."<<endl;
}
```

# 内存分区

栈区：int x=0；int *p=NULL;

堆区：int *p=new int[20];

全局区：存储全局变量以静态变量

常量区：string str="hello";

代码区：存储逻辑代码的二进制

# 构造函数

Teacher.hpp

在头文件里面定义构造函数

```c++
#ifndef Teacher_hpp
#define Teacher_hpp

#include <iostream>
#include <string>

using namespace std;

class Teacher {
    
    
public:
    //构造函数
    Teacher();
    Teacher(string name,int age=20);
    
    //成员函数
    void setName(string _name);
    string getName();
    void setAge(int _age);
    int getAge();
private:
    string m_strName;
    int m_iAge;

};

#endif /* Teacher_hpp */
```

在实现文件里面实现构造函数：

```c++
#include "Teacher.hpp"


Teacher::Teacher(){
    m_strName="jack";
    m_iAge=30;
    cout<<"Teacher()"<<endl;
}
Teacher::Teacher(string name,int age){
    m_strName=name;
    m_iAge=age;
    cout<<"Teacher(string name,int age)"<<endl;
}

void Teacher::setName(string _name){
    m_strName=_name;
}
string Teacher::getName(){
    return m_strName;
}
void Teacher::setAge(int _age){
    m_iAge=_age;
}
int Teacher::getAge(){
    return m_iAge;
}
```

然后在实现文件里面就可以使用：

```c++
#include "Teacher.hpp"

int main(){
    
    Teacher t1;
    
    Teacher t2("zhangsan",10);
    
    Teacher t3("lisi");
    
    cout<<t1.getName()<<" "<<t1.getAge()<<endl;
    cout<<t2.getName()<<" "<<t2.getAge()<<endl;
    cout<<t3.getName()<<" "<<t3.getAge()<<endl;
    
    return 0;
}
```

## 构造函数初始化列表

常量必须用初始化列表初始化。

Teacher.hpp

```c++
#ifndef Teacher_hpp
#define Teacher_hpp

#include <iostream>
#include <string>

using namespace std;

class Teacher {
    
    
public:
    //构造函数
    Teacher(string name="jack",int age=20,int max=100);
    
    //成员函数
    void setName(string _name);
    string getName();
    void setAge(int _age);
    int getAge();
private:
    string m_strName;
    int m_iAge;
    const int m_iMax; //表示这个老师能带多少个学生，是一个常量只能初始化一次
};

#endif /* Teacher_hpp */
```

Teacher.cpp

```c++
#include "Teacher.hpp"


Teacher::Teacher(string name,int age,int max):m_strName(name),m_iAge(age),m_iMax(max){
    //这里使用初始化列表
    cout<<"Teacher(string name,int age)"<<endl;
}

void Teacher::setName(string _name){
    m_strName=_name;
}
string Teacher::getName(){
    return m_strName;
}
void Teacher::setAge(int _age){
    m_iAge=_age;
}
int Teacher::getAge(){
    return m_iAge;
}
```

main.cpp

```c++
Teacher t1;

Teacher t2("zhangsan",10);

Teacher t3("zhangsan",150);


cout<<t1.getName()<<" "<<t1.getAge()<<endl;
cout<<t2.getName()<<" "<<t2.getAge()<<endl;
cout<<t3.getName()<<" "<<t3.getAge()<<endl;
```

## 拷贝构造函数

如果没有定义，则系统默认生成一个。当采用直接初始化(赋值)或复制初始化时系统将自动调用，还有就是参数传递也会调用。

Teacher.hpp

```c++
#ifndef Teacher_hpp
#define Teacher_hpp

#include <iostream>
#include <string>

using namespace std;

class Teacher {
    
    
public:
    //构造函数
    Teacher(string name="jack",int age=20);
    //拷贝构造函数
    Teacher(const Teacher & tea);
    
    //成员函数
    void setName(string _name);
    string getName();
    void setAge(int _age);
    int getAge();
private:
    string m_strName;
    int m_iAge;
   
};

#endif /* Teacher_hpp */
```

Teacher.cpp

```c++
#include "Teacher.hpp"


Teacher::Teacher(string name,int age):m_strName(name),m_iAge(age){
    //这里使用初始化列表
    cout<<"Teacher(string name,int age)"<<endl;
}

Teacher::Teacher(const Teacher & tea){
    cout<<"Teacher(const Teacher & tea)"<<endl;
}

void Teacher::setName(string _name){
    m_strName=_name;
}
string Teacher::getName(){
    return m_strName;
}
void Teacher::setAge(int _age){
    m_iAge=_age;
}
int Teacher::getAge(){
    return m_iAge;
}
```

main.cpp

```c++
Teacher t1;


Teacher t2=t1;//会调用拷贝构造函数
Teacher t3(t1);//会调用拷贝构造函数

test(t1);
```

test是一个函数

```c++
void test(Teacher t){
    t.setName("a");
    cout<<t.getName()<<endl;
}
```

### 浅拷贝

定义一个Array类，数据成员为m_iCount，成员函数包括数据封装函数，构造函数，拷贝构造函数和析构函数。

Array.hpp

```c++
#ifndef Array_hpp
#define Array_hpp

class Array {
    
    
public:
    Array();
    Array(const Array &arr);
    ~Array();
    
    void setCount(int count);
    int getCount();
private:
    int m_iCount;
};

#endif /* Array_hpp */
```

Array.cpp

```c++
#include <iostream>

#include "Array.hpp"

using namespace std;

Array::Array(){
    cout<<"Array"<<endl;
}

Array::Array(const Array &arr){
    //浅拷贝
    m_iCount=arr.m_iCount;
    cout<<"Array &"<<endl;
}

Array::~Array(){
    cout<<"~Array"<<endl;
}

void Array::setCount(int count){
    m_iCount=count;
}

int Array::getCount(){
    return m_iCount;
}
```

测试

```c++
Array arr1;
arr1.setCount(5);

Array arr2(arr1);

cout<<arr2.getCount()<<endl; //5,可以看到拷贝成功
```

### 深拷贝

我们在上一节的例子增加一个指针成员变量，实现深拷贝。

Array.hpp

```c++
#ifndef Array_hpp
#define Array_hpp

class Array {
    
    
public:
    Array(int count);
    Array(const Array &arr);
    ~Array();
    
    void setCount(int count);
    int getCount();
    
    void printAddr();
    
    void printArr();
private:
    int m_iCount;
    int *m_pAdd; //增加了指针
};

#endif /* Array_hpp */
```

Array.cpp

```c++
#include <iostream>

#include "Array.hpp"

using namespace std;

Array::Array(int count){
    m_iCount=count;
    m_pAdd=new int(m_iCount);
    
    //赋默认值
    for (int i=0; i<m_iCount; i++) {
        m_pAdd[i]=i+1;
    }
    
    cout<<"Array"<<endl;
}

Array::Array(const Array &arr){
    //深拷贝
    m_iCount=arr.m_iCount;
    
    m_pAdd=new int[m_iCount];
    
    for (int i=0; i<m_iCount; i++) {
        m_pAdd[i]=arr.m_pAdd[i];
    }
    
    cout<<"Array &"<<endl;
}

Array::~Array(){
    delete [] m_pAdd;
    m_pAdd=NULL;
    cout<<"~Array"<<endl;
}

void Array::setCount(int count){
    m_iCount=count;
}

int Array::getCount(){
    return m_iCount;
}

void Array::printAddr(){
    cout<<m_pAdd<<endl;
}

void Array::printArr(){
    for (int i=0; i<m_iCount; i++) {
        cout<<m_pAdd[i]<<endl;
    }
}
```

测试是否拷贝成功

```c++
Array arr1(5);

Array arr2(arr1);

arr1.printArr();
arr2.printArr();
```

他们打印的值相同，但地址就不一样了。

# 析构函数

1.没有定义则系统自动生成。

2.对象销毁时自动调用，目的是归还资源。

3.析构函数，没有返回值，没有参数，不能重载。

Teacher.hpp

```c++
#ifndef Teacher_hpp
#define Teacher_hpp

#include <iostream>
#include <string>

using namespace std;

class Teacher {
    
    
public:
    //构造函数
    Teacher(string name="jack",int age=20);
    //拷贝构造函数
    Teacher(const Teacher & tea);
    
    //析构函数
    ~Teacher();
    
    //成员函数
    void setName(string _name);
    string getName();
    void setAge(int _age);
    int getAge();
private:
    string m_strName;
    int m_iAge;
   
};

#endif /* Teacher_hpp */
```

然后实现析构函数

```c++
#include "Teacher.hpp"


Teacher::Teacher(string name,int age):m_strName(name),m_iAge(age){
    //这里使用初始化列表
    cout<<"Teacher(string name,int age)"<<endl;
}

Teacher::Teacher(const Teacher & tea){
    cout<<"Teacher(const Teacher & tea)"<<endl;
}

Teacher::~Teacher(){
    cout<<"~Teacher()"<<endl;
}

void Teacher::setName(string _name){
    m_strName=_name;
}
string Teacher::getName(){
    return m_strName;
}
void Teacher::setAge(int _age){
    m_iAge=_age;
}
int Teacher::getAge(){
    return m_iAge;
}
```

最后测试是否调用了析构函数

main.cpp

```c++
Teacher t1; //这样方式声明的，会自动调用析构函数
Teacher t2(t1); //这样方式声明的，会自动调用析构函数

Teacher *t3 = new Teacher();
delete t3; //在堆上创建的对象，必须手动调用
```

# 对象数组

首先定义一个对象Point用来表示一个二维坐标。

Point.hpp

```c++
#ifndef Point_hpp
#define Point_hpp

#include <iostream>

using namespace std;

class Point {
    
    
public:
    Point();
    ~Point();
    
    int m_iX;
    int m_iY;
};

#endif /* Point_hpp */
```

Point.cpp

```c++
#include "Point.hpp"

Point::Point(){
    cout<<"Point()"<<endl;
}

Point::~Point(){
    cout<<"~Point()"<<endl;
}
```

然后创建这个对象的对象数组。

```c++
#include <iostream>
#include <string>
#include "Point.hpp"

using namespace std;

int main(){
    
    //在栈上创建对象
    Point t[3];
    
    t[0].m_iX=10;
    t[0].m_iY=20;
    
    //在堆上创建对象
    Point *p=new Point[3];
    p->m_iX=7;
    p[0].m_iY=10;
    
    p++;//p+=1;p+=1;
    
    //1
    p->m_iX=11;
    p[0].m_iY=20;
    
    //2
    p[1].m_iX=20;
    p++;
    p->m_iY=30;
    
    //遍历
    for (int i=0; i<3; i++) {
        cout<<t[i].m_iX<<" "<<t[i].m_iY<<endl;
    }
    
    
    //现在指针是指向最后一个元素，所以只能倒序遍历
    for (int j=0; j<3; j++) {
        cout<<p->m_iX<<" "<<p->m_iY<<endl;
        p--;
    }
    
    p++; //重要，因为p现在指向到了，数组前面的元素
    
    delete []p;
    p=NULL;
    
    return 0;
}
```

# 对象成员

一个对象的成员是对象。下面模拟一个Line类，有两个Point，point对象有两个成员x,y。

Point.hpp

```c+
#ifndef Point_hpp
#define Point_hpp

#include <iostream>

using namespace std;

class Point {
    
    
public:
    Point();
    ~Point();
    
    void setX(int _x);
    int getX();
    
    void setY(int _y);
    int getY();
private:
    int m_iX;
    int m_iY;
};



#endif /* Point_hpp */
```

Point.cpp

```c++
#include "Point.hpp"

Point::Point(){
    cout<<"Point()"<<endl;
}

Point::~Point(){
    cout<<"~Point()"<<endl;
}

void Point::setX(int _x){
    m_iX=_x;
}

int Point::getX(){
    return m_iX;
}

void Point::setY(int _y){
    m_iY=_y;
}

int Point::getY(){
    return m_iY;
}
```

我们现在测试他们的构造函数调用顺序：

```c++
Line *line=new Line();

delete line;
```

输出如下：

```shell
Point()
Point()
Line()
~Line()
~Point()
~Point()
```

结论：先初始化内部对象成员，然后在初始化外部类。销毁先外部类，然后销毁内部成员对象。

那成员之间他们的初始化顺序和销毁顺序是什么呢：

我给Point,Line都加上了构造参数

Point.cpp

```c++
Point::Point(int x,int y):m_iX(x),m_iY(y){
    cout<<"Point()"<<m_iX<<","<<m_iY<<endl;
}

Point::~Point(){
    cout<<"~Point()"<<m_iX<<","<<m_iY<<endl;
}
```

Line.cpp

```c
Line::Line(int x1,int y1,int x2,int y2):m_pointA(x1,y1),m_pointB(x2,y2){
    cout<<"Line()"<<endl;
}
Line::~Line(){
    cout<<"~Line()"<<endl;
}
```

然后穿入值：

```c++
Line *line=new Line(1,2,3,4);

delete line;
```

输出：

```shell
Point()1,2
Point()3,4
Line()
~Line()
~Point()3,4
~Point()1,2
```

可以看见小初始化最上面的对象成员，销毁则相反。

# 对象指针

首先定义一个坐标类，然后实例化两个对象，然后分别计算坐标之和，最后使用指针操作。

Coordinate.hpp

```c++
#ifndef Coordinate_hpp
#define Coordinate_hpp

class Coordinate {
    
    
public:
    Coordinate();
    ~Coordinate();
public:
    int m_iX;
    int m_iY;
};

#endif /* Coordinate_hpp */
```

Coordinate.cpp

```c++
#include <iostream>

#include "Coordinate.hpp"

using namespace std;

Coordinate::Coordinate(){
    cout<<"Coordinate()"<<endl;
}

Coordinate::~Coordinate(){
    cout<<"~Coordinate()"<<endl;
}
```

测试

```c++
//    Coordinate *p1=NULL;
//    p1=new Coordinate;
//    
//    Coordinate *p2=new Coordinate();
//    
//    p1->m_iX=10;
//    p1->m_iY=20;
//    
//    (*p2).m_iX=30;
//    (*p2).m_iY=40;
//    
//    //计算这两个点坐标之和
//    cout<<p1->m_iX+(*p2).m_iX<<endl; //40
//    cout<<p1->m_iY+(*p2).m_iY<<endl; //60
//    
//    delete p1;
//    p1=NULL;
//    
//    delete p2;
//    p2=NULL;

//对象指针
Coordinate p1;

Coordinate *p2=&p1;

p2->m_iX=10;
p2->m_iY=20;

cout<<p1.m_iX<<endl; //10
cout<<p1.m_iY<<endl; //20，可以看到我们通过指针的方式操作了p1
```

## 成员对象指针

改进上面的项目，将Line里面的点换成指针。

Coordinate.hpp

```c++
#ifndef Coordinate_hpp
#define Coordinate_hpp

class  Coordinate{
    
    
public:
    Coordinate(int x,int y);
    ~Coordinate();
    int getX();
    int getY();
private:
    int m_iX;
    int m_iY;
};

#endif /* Coordinate_hpp */
```

Coordinate.cpp

```c++
#include <iostream>

#include "Coordinate.hpp"

using namespace std;

Coordinate::Coordinate(int x,int y){
    m_iX=x;
    m_iY=y;
    cout<<"Coordinate(int x,int y)"<<endl;
}

Coordinate::~Coordinate(){
    cout<<"~Coordinate"<<endl;
}

int Coordinate::getX(){
    return m_iX;
}

int Coordinate::getY(){
    return m_iY;
}
```

Line.hpp

```c++
#ifndef Line_hpp
#define Line_hpp

#include "Coordinate.hpp"

class Line {
    
    
public:
    Line(int x1,int y1,int x2,int y2);
    ~Line();
    void printInfo();
private:
    Coordinate *m_pCoorA;
    Coordinate *m_pCoorB;
};

#endif /* Line_hpp */
```

Line.cpp

```c++
#include <iostream>

#include "Line.hpp"

using namespace std;

Line::Line(int x1,int y1,int x2,int y2){
    //先实例化两个点
    m_pCoorA=new Coordinate(x1,y1);
    m_pCoorB=new Coordinate(x2,y2);
    cout<<"Line()"<<endl;
}

Line::~Line(){
    delete m_pCoorA;
    m_pCoorA=NULL;
    
    delete m_pCoorB;
    m_pCoorB=NULL;
    cout<<"~Line()"<<endl;
}

void Line::printInfo(){
    cout<<"printinfo()"<<endl;
    cout<<m_pCoorA->getX()<<","<<m_pCoorA->getY()<<endl;
    cout<<m_pCoorB->getX()<<","<<m_pCoorB->getY()<<endl;
}
```

测试

```c++
Line *p=new Line(1,2,3,4);
p->printInfo();

delete p;
p=NULL;

cout<<sizeof(p)<<endl;
cout<<sizeof(Line)<<endl;

//    Coordinate(int x,int y)
//    Coordinate(int x,int y)
//    Line()
//    printinfo()
//    1,2
//    3,4
//    ~Coordinate
//    ~Coordinate
//    ~Line()
//    8 //64位，一个指针8位，
//    16 //line里面有两个指针
```

# this指针

this指针指向当前对象的地址，值和&当前对象的值一样。

Array.hpp

```c++
#ifndef Array_hpp
#define Array_hpp

class Array {
    
    
public:
    Array(int len);
    ~Array();
    
    void setLen(int len);
    int getLen();
    
    Array* printInfo();
private:
    int len;
    
};

#endif /* Array_hpp */
```

Array.cpp

```c++
#include <iostream>

#include "Array.hpp"

using namespace std;

Array::Array(int len){
    this->len=len;
}

Array::~Array(){
    
}

void Array::setLen(int len){
    this->len=len;
}

int Array::getLen(){
    return len;
}

//如果这里return的Array对象，那么他是一个临时对象，不会更改原对象的值
//如果return是Array&,新对象的改变会影响到原对象
//如果return是指针，也会改变原对象
Array* Array::printInfo(){
//    cout<<"len="<<len<<endl;
    cout<<this<<endl;
    return this; //他要求返回一个对象，this是一个指针，*this就是一个对象
}
```

测试

```c
Array arr(10);

//    arr.printInfo().setLen(5);
arr.printInfo()->setLen(5);

//    cout<<arr.getLen()<<endl;
cout<<&arr<<endl;
```

# 继承

## 什么是继承

学生继承人类的一些共性。

定义一个Person类，然后让Worker共有继承Person类。

## 继承中构造函数和析构函数调用顺序

在继承中：

创建对象时先调用父类的构造函数，在调用子类的构造函数。

销毁对象时先调用子类的析构函数，然后在调用父类的析构函数。

输出如下：

```shell
Person()
Worker()
~Worker()
~Person()
```

其中Worker继承Person

## 继承方式

### 共有继承

class A:public B

| 父类成员访问属性  | 子类成员访问属性        |
| --------- | --------------- |
| private   | 无法访问(也可以说没继承下来) |
| protected | protected       |
| public    | public          |

### 保护继承

class A:protected B

| 父类成员访问属性  | 子类成员访问属性        |
| :-------- | --------------- |
| private   | 无法访问(也可以说没继承下来) |
| protected | protected       |
| public    | protected       |

### 私有继承

class A:private B

| 父类成员访问属性  | 子类成员访问属性        |
| :-------- | --------------- |
| private   | 无法访问(也可以说没继承下来) |
| protected | private         |
| public    | private         |

私有继承也属于一个Has a关系，因为他只能访问父类的共有属性。

## 隐藏

父子关系，成员同名，隐藏。

```c++
//Soldier里有一个play,他的父类也有一个play方法
Soldier s;

//调用Soldier里的play方法
s.play();
s.work();

//调用Person里面的play方法
s.Person::play();
```

## 多重集成

注意他不是多继承，比如：士兵继承人，步兵继承士兵，他们之间的关系是多重继承。

## 多继承

比如:农民集成工人类，还继承农民类，简称农民工类，他们之间的关系就是多继承。

Worker.hpp

```c++
#ifndef Worker_hpp
#define Worker_hpp

#include <string>

using namespace std;

class Worker {
    
    
public:
    Worker(string code="001");
    virtual ~Worker();
    void carry();  //射击
protected:
    string m_strCode;
};

#endif /* Worker_hpp */
```

Worker.cpp

```c++
#include <iostream>

#include "Worker.hpp"

using namespace std;

Worker::Worker(string code){
    m_strCode=code;
    cout<<"Worker()"<<endl;
}

Worker::~Worker(){
    cout<<"~Worker()"<<endl;
}

void Worker::carry(){
    cout<<m_strCode<<endl;
    cout<<"Worker-carry()"<<endl;
}
```

Farmer.hpp

```c++
#ifndef Farmer_hpp
#define Farmer_hpp

#include <string>

using namespace std;

class Farmer {
    
    
public:
    Farmer(string name="jack");
    virtual ~Farmer();
    void sow();
protected:
    string m_strName;
};

#endif /* Farmer_hpp */
```

Farmer.cpp

```c++
#include <iostream>

#include "Farmer.hpp"

using namespace std;

Farmer::Farmer(string name){
    m_strName=name;
    cout<<"Farmer()"<<endl;
}

Farmer::~Farmer(){
    cout<<"~Farmer()"<<endl;
}


void Farmer::sow(){
    cout<<"sow()"<<endl;
}
```

MigrantWorker.hpp

```c++
#ifndef MigrantWorker_hpp
#define MigrantWorker_hpp

#include <string>

#include "Worker.hpp"
#include "Farmer.hpp"

using namespace std;

//这里在前面，先调用构造函数
class MigrantWorker:public Worker,public Farmer {
    
    
public:
    MigrantWorker(string name,string code);
    ~MigrantWorker();
};

#endif /* MigrantWorker_hpp */
```

MigrantWorker.cpp

```c++
#include <iostream>

#include "MigrantWorker.hpp"

using namespace std;

MigrantWorker::MigrantWorker(string name,string code):Farmer(name),Worker(code){
    cout<<"MigrantWorker"<<endl;
}

MigrantWorker::~MigrantWorker(){
    cout<<"~MigrantWorker()"<<endl;
}
```

最后测试

```c++
MigrantWorker *p = new MigrantWorker("Merry","100");

p->carry();
p->sow();

delete p;
p=NULL;
```

输出：

```shell
Worker()
Farmer()
MigrantWorker
100
Worker-carry()
sow()
~MigrantWorker()
~Farmer()
~Worker()
```

## 虚继承

是为了解决菱形继承问题。简单来讲就是，工人继承人，农民继承人，农民工继承工人，农民就会出现两份人的信息，如果让工人虚继承人，农民虚继承人，农民工在继承他们两个，就只会出现一份人的信息。就这问题，如果按照常规写法，会报错，Person重定义。解决方法有多种

### 宏定义

```c++
#ifndef Person_hpp //解决宏定义
#define Person_hpp //解决宏定义

#include <string>

using namespace std;

class Person {
    
    
public:
    Person(string color="blue");
    virtual ~Person();
    
    void printColor();
protected:
    string m_strColor;
};

#endif //解决宏定义
```

在菱形继承中，会导致里面有多份数据。可以这样验证：

```shell
Person()
Worker()
Person()
Farmer()
MigrantWorker
Worker red //重复数据
Person-printColor()
Farmer red //重复数据
Person-printColor()
~MigrantWorker()
~Farmer()
~Person()
~Worker()
~Person()
```

解决方法是工人，农民从人类那里虚拟继承。

```c++
class Worker:virtual public Person
  
class Farmer:virtual public Person
```

这样打印结果就是：

```shell
Person()
Worker()
Farmer()
MigrantWorker
b
Person-printColor()
b
Person-printColor()
~MigrantWorker()
~Farmer()
~Worker()
~Person()
```

但是这样的结果就是，Person类无法接收到子类传递的参数。下面是完整测试代码：

Person.hpp

```c++
#ifndef Person_hpp
#define Person_hpp

#include <string>

using namespace std;

class Person {
    
    
public:
    Person(string color="b");
    virtual ~Person();
    
    void printColor();
protected:
    string m_strColor;
};

#endif /* Person_hpp */
```

Person.cpp

```c++
#include <iostream>

#include "Person.hpp"

using namespace std;

Person::Person(string code){
    m_strColor=code;
    cout<<"Person()"<<endl;
}

Person::~Person(){
    cout<<"~Person()"<<endl;
}

void Person::printColor(){
    cout<<m_strColor<<endl;
    cout<<"Person-printColor()"<<endl;
}
```

Worker.hpp

```c++
#ifndef Worker_hpp
#define Worker_hpp

#include <string>

#include "Person.hpp"

using namespace std;

class Worker:virtual public Person {
    
    
public:
    Worker(string code="001",string color="blue");
    virtual ~Worker();
    void carry();  //射击
protected:
    string m_strCode;
};

#endif /* Worker_hpp */
```

Worker.cpp

```c++
#include <iostream>

#include "Worker.hpp"

using namespace std;

Worker::Worker(string code,string color):Person("Worker "+color){
    m_strCode=code;
    cout<<"Worker()"<<endl;
}

Worker::~Worker(){
    cout<<"~Worker()"<<endl;
}

void Worker::carry(){
    cout<<m_strCode<<endl;
    cout<<"Worker-carry()"<<endl;
}
```

Farmer.hpp

```c++
#ifndef Farmer_hpp
#define Farmer_hpp

#include <string>

#include "Person.hpp"

using namespace std;

class Farmer:virtual public Person {
    
    
public:
    Farmer(string name="jack",string color="blue");
    virtual ~Farmer();
    void sow();
protected:
    string m_strName;
};

#endif /* Farmer_hpp */
```

Farmer.cpp

```c++
#include <iostream>

#include "Farmer.hpp"



using namespace std;

Farmer::Farmer(string name,string color):Person("Farmer "+color){
    m_strName=name;
    cout<<"Farmer()"<<endl;
}

Farmer::~Farmer(){
    cout<<"~Farmer()"<<endl;
}


void Farmer::sow(){
    cout<<"sow()"<<endl;
}
```

MigrantWorker.hpp

```c++
#ifndef MigrantWorker_hpp
#define MigrantWorker_hpp

#include <string>

#include "Worker.hpp"
#include "Farmer.hpp"

using namespace std;

//这里在前面，先调用构造函数
class MigrantWorker:public Worker,public Farmer {
    
    
public:
    MigrantWorker(string name,string code,string color);
    ~MigrantWorker();
};

#endif /* MigrantWorker_hpp */
```

MigrantWorker.cpp

```c++
#include <iostream>

#include "MigrantWorker.hpp"

using namespace std;

MigrantWorker::MigrantWorker(string name,string code,string color):Farmer(name,color),Worker(code,color){
    cout<<"MigrantWorker"<<endl;
}

MigrantWorker::~MigrantWorker(){
    cout<<"~MigrantWorker()"<<endl;
}
```

# 多态

## 静态多态(早绑定)

例子是，一个类有多个函数重载，在调用的时候传不同的参数，在编译时就确定了要调用那个函数。

## 动态多态(晚绑定)

比如：我们定义一个形状类定义一个计算面积的函数，在定义圆继承形状类中也定义一个计算面积函数并实现，在定义一个矩形并也实现计算面积的函数。

然后也用形状类型的指针，引用这两个对象，然后调用计算面积的方法。他们会调用不同对象类的面积方法。

Shape.hpp

```c++
#ifndef Shape_hpp
#define Shape_hpp



class Shape {
    
    
public:
    Shape();
    ~Shape();
    virtual double calcArea(); //要实现多态，需要加virtual，子类方法默认也就加上了，但最好手动也加上，这样一看就明白，
};

#endif /* Shape_hpp */
```

Shape.cpp

```c++
#include "Shape.hpp"

#include <iostream>

using namespace std;

Shape::Shape(){
    cout<<"Shape()"<<endl;
}

Shape::~Shape(){
    cout<<"~Shape"<<endl;
}

double Shape::calcArea(){
    cout<<"Shape-calcAre()"<<endl;
    return 0;
}
```

Circle.hpp

```c++
#ifndef Circle_hpp
#define Circle_hpp

#include "Shape.hpp"

class Circle:public Shape {
    
    
public:
    Circle(double r);
    ~Circle();
    double calcArea();
protected:
    double m_dR; //圆的半径
};

#endif /* Circle_hpp */
```

Circle.cpp

```c++
#include <iostream>

#include "Circle.hpp"

using namespace std;

Circle::Circle(double r){
    cout<<"Circle"<<endl;
}

Circle::~Circle(){
    cout<<"~Circle"<<endl;
}
double Circle::calcArea(){
    cout<<"Circle-calcArea"<<endl;
    return 3.14*m_dR*m_dR;
}
```

Rect.hpp

```c++
#ifndef Rect_hpp
#define Rect_hpp

#include "Shape.hpp"

class Rect:public Shape {
    
    
public:
    Rect(double width,double height);
    ~Rect();
    double calcArea();
    
protected:
    double m_dWidth;
    double m_dHeight;
};

#endif /* Rect_hpp */
```

Rect.cpp

```c++
#include <iostream>

#include "Rect.hpp"

using namespace std;

Rect::Rect(double width,double height){
    m_dWidth=width;
    m_dHeight=height;
    cout<<"Rect"<<endl;
}

Rect::~Rect(){
    cout<<"~Rect"<<endl;
}

double Rect::calcArea(){
    cout<<"Rect-calcArea"<<endl;
    return m_dHeight*m_dWidth;
}
```

测试

```c++
Shape *shape1=new Rect(2,5);
Shape *shape2=new Circle(3);

shape1->calcArea();
shape2->calcArea();

delete shape1;
delete shape2;

shape1=NULL;
shape2=NULL;
```

输出：

```shell
Shape()
Rect
Shape()
Circle
Rect-calcArea
Circle-calcArea
~Shape //可以看见析构函数还有问题，因为只调用了父类析构函数
~Shape
```

## virtual使用限制

修饰的函数不能使全局函数，不能修饰静态成员函数，不能修饰构造函数，导致编译错误。

不能修饰内联函数，如果修饰了inline将被忽略。

## 虚析构函数

他就是解决上面例子中析构函数问题的。一般建议父类都声明虚构析构函数，因为你不知道未来的子类是否会使用析构函数释放资源。

```c++
virtual ~Shape(); 
```

## 抽象类

含有纯虚函数的类叫抽象类。不能实例化对象，编译错误

```c++
virtual double test()=0; //声明一个纯虚函数
```

这里我们设计这样一个示例，一个人类，一个工人类，一个清洁工类

Person.hpp

```c++
#ifndef Person_hpp
#define Person_hpp

#include <string>

using namespace std;

class Person {
    
    
public:
    Person(string name);
    virtual void work()=0; //纯虚函数
    virtual ~Person(){};
private:
    string m_strName;
};

#endif /* Person_hpp */
```

Person.cpp

```c++
#include "Person.hpp"

Person::Person(string name){
    m_strName=name;
}
```

Worker.hpp

```c++
#ifndef Worker_hpp
#define Worker_hpp

#include "Person.hpp"

class Worker:public Person {
    
    
public:
    Worker(string name,int age);
//    virtual void work();
private:
    int m_iAge;
};

#endif /* Worker_hpp */
```

Worker.cpp

```c++
#include <iostream>

#include "Worker.hpp"

using namespace std;

Worker::Worker(string name,int age):Person(name){
    m_iAge=age;
}

//void Worker::work(){
//    cout<<"Work-work()"<<endl;
//}
```

Dustman.hpp

```c++
#ifndef Dustman_hpp
#define Dustman_hpp

#include "Worker.hpp"

class Dustman:public Worker {
    
    
public:
    Dustman(string name,int age);
    virtual void work();
};

#endif /* Dustman_hpp */
```

Dustman.cpp

```c++
#include <iostream>

#include "Dustman.hpp"

using namespace std;

Dustman::Dustman(string name,int age):Worker(name,age){
    
}

void Dustman::work(){
    cout<<"Dustman-扫地"<<endl;
}
```

测试

```c++
Dustman dustman("a",20); //测试是否可以被实例化
```

## 接口类

仅含有纯虚函数的类称为接口类。下面定义一个可飞的接口，然后实现一个飞机，战斗机类。

Flyable.hpp

```c++
#ifndef Flyable_h
#define Flyable_h

class Flyable {
    
    
public:
    virtual void takeoff()=0;
    virtual void land()=0;
};

#endif /* Flyable_h */
```

由于它是接口类，所以没有cpp文件。

Plane.hpp

```c++
#ifndef Plane_hpp
#define Plane_hpp

#include <string>

#include "Flyable.hpp"

using namespace std;

class Plane :public Flyable {
    
    
public:
    Plane(string code);
    virtual void takeoff();
    virtual void land();
    void printCode();
private:
    string m_strCode;
};

#endif /* Plane_hpp */
```

Plane.cpp

```c++
#include <iostream>

#include "Plane.hpp"

using namespace std;

Plane::Plane(string code){
    m_strCode=code;
}

void Plane::takeoff(){
    cout<<"Plane-takeoff()"<<endl;
}

void Plane::land(){
    cout<<"Plane-land()"<<endl;
}

void Plane::printCode(){
    cout<<m_strCode<<endl;
}
```

FighterPlane.hpp

```c++
#ifndef FighterPlane_hpp
#define FighterPlane_hpp

#include <string>

#include "Plane.hpp"

using namespace std;

class FighterPlane:public Plane {
    
    
public:
    FighterPlane(string code);
    virtual void takeoff();
    virtual void land();
};

#endif /* FighterPlane_hpp */
```

FighterPlane.cpp

```c++
#include <iostream>

#include "FighterPlane.hpp"


using namespace std;

FighterPlane::FighterPlane(string code):Plane(code){
    
}

void FighterPlane::takeoff(){
    cout<<"FighterPlane-takeoff()"<<endl;
}

void FighterPlane::land(){
    cout<<"FighterPlane-land()"<<endl;
}
```

测试

```c++
#include <iostream>

#include "Flyable.hpp"
#include "Plane.hpp"
#include "FighterPlane.hpp"

void flyMatch(Flyable *f1,Flyable *f2){
    f1->takeoff();
    f1->land();
    f2->takeoff();
    f2->land();
}

int main(int argc, const char * argv[]) {

    //传入父类
//    Plane p1("1");
//    Plane p2("2");
//    
//    flyMatch(&p1, &p2);
    
    //传入子类
    FighterPlane p1("1");
    FighterPlane p2("2");
    
    p1.printCode();
    p2.printCode();
    
    flyMatch(&p1, &p2);
    
    return 0;
}
```

# 模板

