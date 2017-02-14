---
title: 数据结构-线性表
date: 2017-02-14 18:28:48
categories: DataStructure
tags: 
    - LineTable
---

# 简介

线性表：

顺序表(数组)，链表

链表：

静态链表，单链表，循环链表，双向链表

## 应用场景

常见的应用场景，比如通讯录，有增加，删除，搜索。

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











































