---
title: Java笔记
date: 2023-04-19 10:45
tags: [笔记]
---

## String 类特点分析

### String 类对象两种实例化的方式比较

```java
String A = "abc"
String B = "abc"
```

直接赋值会直接将对象保存到对象池中（堆）
这是指向的同一块堆空间

字符串池
在存储时会去查找是否有相同的
池中没有数据，保存新数据
池中有数据

构造方法实例化

```java
String str = new String("abc")
```

字符串是一个匿名对象
Strint('abc')会让匿名对象开辟一个堆内存
new 会重新开辟一个堆内存空间
直接赋值要比实例开辟更节省空间

#### 区别：

    * 直接赋值： 只会产生一个实例化对象，并且可以自动保存到对象池之中，以实现该字符串实例到重用
    * 构造方法： 会参数两个实例化对象，并且不会自动入池无法对象重用

### String 对象（常量）池

对象池的主要目的是实现数据的共享处理。
_ 静态常量池：指的是程序（_.class）在家在的时候会自动将此成勋之中保存的字符串、普通常量、类和方法的信息等待，全部进行分配
_ 运行时常量池：当一个程序（_.class)加载之后可能有一常量，这个时候提供的常量池

```Java
// 静态案例
String strA = "abc";
String strB = "www."+"abc"+".cn";
strA == strB   结果True
//运行案例
String info = "abc"
String strA = "abc";
String strB = "www."+info+".cn";
strA == strB   结果False
```

程序在加载时并不确定 info 内容是什么，因为在进行字符串连接的时候 info 采用的是一个变量，变量的内容是可以修改的，所以它不认为最终的 strB 的结果就是一个所需要的结果

### 字符串内容不可修改

字符串常量并没有产生任何改变，改变的只是一个 String 类对象的引用，并且这种改变将有可能带来大量的垃圾

### 主方法组成分析

public:描述的是一种访问权限，主方法是一切的开始点，开始点一定是公共的
static:程序的执行是通过类名称完成的，所以表示此方法是由类直接调用
void:主方法是一切的起点，起点一旦开始就没有返回的可能了
main:是一个系统定义好的方法名称
String args[]:字符串的数组，可以实现程序启动参数的接收

### JavaDoc 文档介绍

````
https://docs.oracle.com/javase/8/docs/api/java/lang/String.html```
类的完整定义
类的相关说明
成员属性的摘要
构造方法摘要
方法摘要
详细说明

最后部分就是堆方法和成员的详细解释

### 字符串与字符数组
p81

### 字符串与字节

### 字符串比较
equals()
注意会区分大小写
equalsIgnoreCase()
不区分大小写比较

## p84 字符串查找
从一个完整的字符串中查找子字符串的存在，方法如下
|方法|功能|
|---|---|
|public public boolean contains(String s)|判断字符串是否存在|
|public int indexOf(String str)|从头查找制定字符串的位置|
|public int indexOf(String str,int fromIndex)|从指定位置查找字符串的位置|
|public int lastIndexOf(String str)|由后向前查找字符串的位置|
|public inst lastIndexOf(String str,int fromIndex)|从指定位置由后向前查找指定字符串的位置|
|public boolean startsWith(String prefix)|判断是否以指定的字符串开头|
|public boolean startWith(String prefix,int toffset)|判断是否以指定的字符串结尾|
|public booean endsWith(String suffix)|判断是否以指定的字符串结尾|


## p85字符串替换
指定内容进行一个指定字符串的替换显示
|方法|功能|
|---|---|
|public String replaceAll(String regx,String replacement)|全部替换|
|public String replaceFirst(String regex,String replacement)|替换首个|

## p86字符串的拆分
在字符串处理时还提供 了一种字符串拆分处理，字符串的才分操作主要是可以更具表达式实现字符串的拆分
并且才分完成的数据以字符串数组的形式返回
|方法|功能|
|---|---|
|public String[] split(String regex)|按照指定的字符串全部拆分|
|public String[] split(String regex,int limit)|按照指定的字符串拆分为指定的个数,后面不拆了|

如果遇到拆不开的情况，这个时候最简单的理解就是使用"\\"双斜杠转义

## p87字符串截取
从一个完整的字符串之中截取出子字符串，对于截取操纵有两个方法
|方法|功能|
|---|---|
|public String substring(int beginIndex)|从指定索引截取到结尾|
|pubic String substring(int beginIndex,int endIndex)|截取指定索引范围中的子字符串|
有时候开始或结束索引往往是通过indexOf()方法计算得来的，非常常用


## p88格式化字符串
|方法|功能|
|---|---|
|public static String format(String format,Object...args)|根据指定结构进行文本格式化|
```java
String name = "张三";
int age = 18;
double score = 98.2323;
String str = String.format("姓名:%s、年龄：%d、成绩：%5.2f",name,age,score)
````

## p89 其他方法

| 方法                             | 功能               |
| -------------------------------- | ------------------ |
| public String concat(String str) | 字符串的连接       |
| public String intern()           | 字符串入池         |
| public boolean isEmpty()         | 判断是否为空字符串 |
| public int length()              | 判断字符串的长度   |
| public String trim()             | 去除左右的空格信息 |
| public String toUpperCase()      | 转大写             |
| public String toLowerCase()      | 转小写             |

trim 不会消除空格的长度，但会去除左右空格显示
在 String 类里面提供有大小写转换，但是这种转换的特征是可以避免非字符串的转换

## p90 继承问题的引出

可以扩充已有类的功能
所谓的良好的代码是指结构性合理，适合维护，可重用性很高，适合于维护
所谓继承就是在已有的代码上进行扩充

## 91 类继承定义

```java
class 子类 extends 父类{}
```

## 106 Object 类

不存在继承关系,是所有类的父类，考研接收所有子类
所有引用类型可以用 Object 类接收
