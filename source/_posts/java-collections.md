---
title: Java集合框架总结
date: 2016-10-31 14:17:01
categories: Java
tags: 
    - Collections
---

# 框架接口图

![](http://7qnc6h.com1.z0.glb.clouddn.com/java-collection-interface)

Java的集合框架分为两类Collection和Map

Collection是集合，也就是存储对象的value

Map是用来存储键值对的容器



List：有序集合，可以储存null值，值可以重复



Set:无序集合，可以存储null值，值不能重复

SortedSet:可以排序的set，不能存储null值，值不能重复。并提供了可以获取子Set的方法

NavigableSet:提供方便搜索的一些方法，比如：返回小于某个元素的元素



Queue：队列，可以存储null值，值可以重复。先进先出，对头删除元素，队尾添加元素

Deque:双端队列，也就是队头，对尾都可以删除元素



测试List

```java
ArrayList<String> strings = new ArrayList<>();
strings.add("a");
strings.add("b");
strings.add(null);
strings.add(null);
strings.add("aa");

strings.forEach(e-> System.out.println(e));
```

输出：

```shell
a
b
null
null
aa
```

发现List确实是有序集合，且可以存储null值，并且值可以重复



测试Set

```java
HashSet<String> strings = new HashSet<>();
strings.add("a");
strings.add("b");
strings.add(null);
strings.add(null);
strings.add("aa");

strings.forEach(e-> System.out.println(e));
```

输出：

```java
null
aa
a
b
```

发现Set无序的，能储存null元素，值不能重复



测试Queue:

```java
HashSet<String> strings = new HashSet<>();
strings.add("a");
strings.add("b");
strings.add(null);
strings.add(null);
strings.add("aa");

strings.forEach(e-> System.out.println(e));
```

输出：

```shell
a
b
null
null
aa
```

可以发现输出和输入顺序都一样，并且能存储null。



测试双端队列：

```java
LinkedList<String> strings = new LinkedList<>();
strings.add("a");
strings.add("b");
strings.add(null);
strings.add(null);
strings.add("aa");

strings.addFirst("first");
strings.addLast("last");

strings.forEach(e -> System.out.println(e));

System.out.println("------------");

System.out.println(strings.pollFirst());
System.out.println(strings.pollLast());
```

输出：

```shell
first
a
b
null
null
aa
last
------------
first
last
```

可以发现我们不仅可以在首尾添加元素，也能在首尾删除元素。



测试SortedSet:

```java
TreeSet<String> strings = new TreeSet<>();
strings.add("a");
strings.add("b");
strings.add("aa");
strings.add("aa");

strings.forEach(e-> System.out.println(e));
```

输出：

```java
a
aa
b
```

说明是有序的，并且不能存储null，元素也不能重复。在比较元素的时候还可以传入自定义比较器：

```java
TreeSet<String> strings = new TreeSet<>((o1, o2) -> {
    if (o1.length() < o2.length())
        return -1;
    else if (o1.length() > o2.length())
        return 1;
    else
        return 0;
});

strings.add("a");
strings.add("b");
strings.add("aa");
strings.add("ab");
```

输出：

```shell
a
aa
```

我们发现相同的元素不能存储进去。



测试SortedSet获取子集：

```java
TreeSet<String> strings = new TreeSet<>();
strings.add("a");
strings.add("b");
strings.add("aa");
strings.add("ab");

SortedSet<String> strings1 = strings.subSet("a", "ab");
strings1.forEach(e -> System.out.println(e));
```

输出：

```shell
a
aa
```

subSet方法就定义到了SortedSet中，作用是返回元素a到元素ab中间的元素，不包括ab元素的不可修改set。



测试NavigableSet:

```java
TreeSet<String> strings = new TreeSet<>();
strings.add("a");
strings.add("b");
strings.add("aa");
strings.add("ab");

strings.forEach(e-> System.out.println(e));
System.out.println("------------");
System.out.println(strings.lower("ab"));
System.out.println(strings.higher("ab"));
```

输出：

```shell
a
aa
ab
b
------------
aa
b
```

可以使用快速的搜索方法，比如使用lower找小于ab的元素，使用higher找大于ab的元素。

























