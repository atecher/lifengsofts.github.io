---
title: 详解Java集合框架
date: 2016-10-31 14:17:01
categories: Java
tags: 
    - Collections
---

# 简介

Java最初版本只实现了一些常用的数据结构，并提供了这些类或接口Vector,Stack,Hashtable,BitSet,Enumeration接口来实现这些结构。

其中Enumeration接口提供了让我们能枚举任意容器元素的抽象机制。

# 特点

## 将集合的接口与实现分离

这一点我们可以从常见的队列Queue的设计上看出来，队列的原则是尾部添加元素，在队列的头部删除元素，可以看到Java的实现是首先定义了一个接口，里面定义了一些Queue的常用操作方法，

```java
public interface Queue<E> extends Collection<E> {
	...
	boolean add(E e);
	boolean offer(E e);
	E remove();
	...
}
```

然后在根据不同的数据结构实现队列，通常情况下队列使用两种数据结构实现，循环数组和链表，如下图：

![](http://wenku.baidu.com/content/93a710a977232f60dccca1c2?m=3ff7f6828f73013b3217334265606453&type=pic&src=c990dd3eeba6f2e2656ba7c1d02091be.jpg)

这样在编程的时候只需要更换实现类就可以轻松的切换所使用的数据结构了。

# Collection

可以看到上面的Queue都继承Collection，其实集合类的都是继承了他，他提供了几个最基本的方法：

```java
public interface Collection<E> extends Iterable<E> {
	boolean add(E e);
	Iterator<E> iterator();
}
```

当然还有其他方法。

add：添加一个元素

iterator：返回一个实现了Iterator接口的对象。使用它可以很方便的访问集合中的元素。

# Iterator

Iterator接口包含的方法：

```java
public interface Iterator<E> {    
    boolean hasNext();
 
    E next();

    default void remove() {
        throw new UnsupportedOperationException("remove");
    }

    default void forEachRemaining(Consumer<? super E> action) {
        Objects.requireNonNull(action);
        while (hasNext())
            action.accept(next());
    }
}
```

便利元素的方式通过反复调用next方法即可访问每个元素，但是如果达到了集合末尾，将抛出NoSuchElementException，所以在调用next方法前要先调用hasNext方法检测。

```java
ArrayList<String> strings = new ArrayList<>();
strings.add("a");
strings.add("b");
strings.add("c");
strings.add("d");
strings.add("e");

Iterator<String> iterator = strings.iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

当然也可以通过foreach循环遍历：

```java
for (String s :
       strings ) {
    System.out.println(s);
}
```

编译器会把for each语法结构转为上面的迭代器的结构。这种方式可以遍历所有实现了Iterable接口的结构。

# Iterable

Iterable只包含一个iterator抽象方法

```java
public interface Iterable<T> {
    
    Iterator<T> iterator();
    ...
}
```

目的是让用户实现自定义的数据结构返回一个实现了Iterator接口的对象，我们看到ArrayList的实现如下：

```java
public Iterator<E> iterator() {
    return new Itr();
}
```

其中Itr是一个内部类，定义在ArrayList中，并实现了Iterator接口。

```java
private class Itr implements Iterator<E> {
    int cursor;       // index of next element to return
    int lastRet = -1; // index of last element returned; -1 if no such
    int expectedModCount = modCount;

    public boolean hasNext() {
        return cursor != size;
    }

    @SuppressWarnings("unchecked")
    public E next() {
        checkForComodification();
        int i = cursor;
        if (i >= size)
            throw new NoSuchElementException();
        Object[] elementData = ArrayList.this.elementData;
        if (i >= elementData.length)
            throw new ConcurrentModificationException();
        cursor = i + 1;
        return (E) elementData[lastRet = i];
    }

    public void remove() {
        if (lastRet < 0)
            throw new IllegalStateException();
        checkForComodification();

        try {
            ArrayList.this.remove(lastRet);
            cursor = lastRet;
            lastRet = -1;
            expectedModCount = modCount;
        } catch (IndexOutOfBoundsException ex) {
            throw new ConcurrentModificationException();
        }
    }

    @Override
    @SuppressWarnings("unchecked")
    public void forEachRemaining(Consumer<? super E> consumer) {
        Objects.requireNonNull(consumer);
        final int size = ArrayList.this.size;
        int i = cursor;
        if (i >= size) {
            return;
        }
        final Object[] elementData = ArrayList.this.elementData;
        if (i >= elementData.length) {
            throw new ConcurrentModificationException();
        }
        while (i != size && modCount == expectedModCount) {
            consumer.accept((E) elementData[i++]);
        }
        // update once at end of iteration to reduce heap write traffic
        cursor = i;
        lastRet = i - 1;
        checkForComodification();
    }

    final void checkForComodification() {
        if (modCount != expectedModCount)
            throw new ConcurrentModificationException();
    }
}
```

最重要的是Java SE8中不写循环而直接使用forEachRemaining方法就可以使用Lambda表达式处理每个元素：

```java
strings.iterator().forEachRemaining(e-> System.out.println(e));
```

同时也可是使用Iterable接口中的forEach方法来遍历：

```java
strings.forEach(e-> System.out.println(e));
```

需要注意的是元素的访问顺序取决于集合类型，如果是ArrayList迭代顺序将是和原来的顺序一样。如果是HashSet这类集合会按照某种随机次序出现，虽然能完全迭代完集合元素，但是顺序确实未知的。不过顺序问题对于计算总和或统计符合某个条件的元素没有多大影响。

我们注意到Iterator接口的方法和Enumeration接口的方法很像，其实Enumeration接口是Java1.0 API提供用来访问元素的，但是后来改用了Iterator接口，所以说我们还可以这样遍历元素：

```java
Vector<String> strings1 = new Vector<>();
strings1.add("a");
strings1.add("b");
strings1.add("c");
Enumeration<String> elements = strings1.elements();
while (elements.hasMoreElements()) {
    System.out.println(elements.nextElement());
}
```

## Iterator迭代器和其他语言区别

Java中的迭代器和其他语言中的迭代器有着本质的区别，在C++中给定一个位置不需要遍历就可以拿到该位置的元素，而在Java中不行。Java中查找元素的唯一方法是调用next方法，所以Java中的迭代器位于两个元素之间，当调用next方法后，迭代器越过一个元素，并返回刚刚越过的元素。

所以如果要通过Iterator删除一个元素，首先要调用next方法让他越过这个元素：

```java
Iterator<String> iterator = strings.iterator();
iterator.next();
iterator.remove();
```

如果要删除两个相邻的元素，不能直接调用两次remove方法，而是调用next方法：

```java
Iterator<String> iterator = strings.iterator();
iterator.next();
iterator.remove();
iterator.next();
iterator.remove();
```

# AbstractCollection

出现这抽象类的原因是，我们发现Collection接口中有很多个抽象方法，如果我们自己要实现一个接口，直接实现Collection接口需要些很多的方法，而AbstractCollection的功能就是帮我实现了一些通用的方法，如果我们要实现自己的集合就可以复用这些方法了。当然我们你觉得他实现的不好，完全可以覆盖他原有的方法。当然这个设计模式在Java8中好像有点过时了，因为完全可以把这些方法当默认方法添加到Collection接口中。

另外collection中一个removeIf可以很方便的删除一个集合中满足条件的元素：

```java
ArrayList<String> strings = new ArrayList<>();
strings.add("a123234324");
strings.add("b34");
strings.add("c");
strings.add("d4");
strings.add("e");

strings.removeIf(e->e.length()>2);

strings.forEach(e -> System.out.println(e));

strings.removeIf(new Predicate<String>() {
    @Override
    public boolean test(String s) {
        return s.length()==2;
    }
});

strings.forEach(e -> System.out.println(e));
```

# Java集合简介

可以看到有两个大家族接口Collection和Map。

Collection用了表示抽象的集合

map表示键值对的集合

## List

是有序集合，可以通过迭代器和整数索引来访问元素，List接口中定义了很多用于随机访问的方法：

```java
boolean add(E e);
boolean remove(Object o);
E get(int index);
void add(int index, E element);
E remove(int index);
E set(int index, E element);
...
```

其中定义了一个listIterator方法，用于返回ListIterator实例，其中定义了一些方法用于在迭代器增加一个元素或者替换元素：

```java
void add(E e);
void set(E e);
```

使用方法还是像遍历方法一样，set方法需要先调用next方法

```java
ArrayList<String> strings = new ArrayList<>();
strings.add("a123234324");
strings.add("b34");
strings.add("c");
strings.add("d4");
strings.add("e");

ListIterator<String> stringListIterator = strings.listIterator();

//相当于add(1,"b")
stringListIterator.next();
stringListIterator.add("b");


//相当于set(1,"s")
stringListIterator.next();
stringListIterator.next();
stringListIterator.set("s");

strings.forEach(e -> System.out.println(e));
```

虽然LinkedList也有listIterator方法，也就是说也能随机访问，但是因为他的实现结构是链表，所以随机访问性能没有ArrayList性能好。

```java
LinkedList<String> strings = new LinkedList<>();
strings.add("a123234324");
strings.add("b34");
strings.add("c");
strings.add("d4");
strings.add("e");

ListIterator<String> stringListIterator = strings.listIterator();
```

为了避免对链表进行随机访问，Java SE 1.4加入了一个标记接口RandomAccess，他没有任何方法，只是表示一个类是否支持随机访问：

```java
LinkedList<String> strings = new LinkedList<>();
if (strings instanceof RandomAccess) {
    System.out.println("链表支持随机访问");
} else {
    System.out.println("链表不支持随机访问");
}
```

## Set

和List接口差不多，不过他不允许存储重复元素，并且元素也是无需的，所以说适当的定义equals方法，同时如果两个相当的对象，返回的hashCode也要一样。

## SortedSet和SortedMap

## NavigableSet和NavigableMap

# 具体的集合



















































