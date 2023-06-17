---
title: 韩顺平
date: 2023-05-16 14:24
tags: [笔记]

---

## 

## 269-270 IDEA快捷键

* command+删除键 删除一行
* command+d 快速复制
* command+r 快速运行
* command+n 快速生成构造方法
* option+/ 自动补全
* command+H 查看一个类的层级关系
* command+B 快速定位函数
* option+enter 快速导入类
*  Command + Option + L 快速格式化代码
* 变量名后输入.var快熟生成变量名

## 271 模版快捷键

* main 快速生成住方法
* sout快速生成打印
* fori 快速生成循环

在file->settings->editor->live templates->查看有哪些模版快捷键可以注解增加模版

## 272 包

**三大作用**

* 区分相同名字的类
* 当类很多时，可以很好的管理类
* 控制访问范围



**包的基本语法**

``` java
package com.hspedu;
```

说明：

1.package 关键字，表示打包

2.com.hspedu 表示包名

## 273 包原理

**包的本质**

实际上就是创建不同的文件夹来保存文件

## 274 包的快速入门

如果在一个类中引用不同包中的相同类，需要用包名区分

Dog dog = new Doc();

com.abc.Dog dog = new com.abc.Doc();

## 275 包的命名

**命名规则**

只能包含数字、字母、下划线、小圆点、但不能用数字开头、不能时关键字或保留字

**命名规范**

一般是小写字母+小圆点一般是

```
com.公司名.项目名.业务模块名
比如 com.hspedu.oa.model
		com.hspedu.oa.controller;
		com.sina.crm.user
		com.sina.crm.order
		com.sina.crm.utils
```

## 276 常用的类

**常用的包**

```
java.lang.* lang包是基本包，默认引入，不需要再引入
java.util.*	util包，系统提供的工具包，工具类，使用Scanner
java.net.*	网络包，网络开发
java.awt.*	是左java的界面开发GUOI
```

## 包的使用细节

**如何引入包**

```
com.hspedu.pkg:Import01.java
```

```
语法: import 包;
```

比如：import java.utils.Scanner;

需要那个类就导入那个类，不建议使用*

**注意事项与细节**

* package的作用是声明当前类所在的包，需要放在类的最上面，一个类中最多只有一句package

* import指定位置放在package的下面，在类定义前面，可以有多句且没有顺序的要求

## 277 访问修饰符

* 公开级别：public修饰，对外公开
* 受保护级别:protected修饰，对字类和统一报中的类公开
* 默认级别：没有修饰符，想同一包的类公开
* 私有级别：private修饰，只有类本身可以访问，不对外公开

| 访问级别 | 访问控制修饰符 | 同类 | 同包 | 子类 | 不同包 |
| -------- | -------------- | ---- | ---- | ---- | ------ |
| 公开     | public         | o    | o    | o    | o      |
| 受保护   | protected      | o    | o    | o    | x      |
| 默认     | 无             | o    | o    | x    | x      |
| 私有     | private        | o    | x    | x    | x      |

**使用注意事项**

* 修饰符可以用来修饰类中的属性，成员方法以及类
* 只有默认的和public才能修饰类，并且遵循上述访问权限的特点
* 业务没有学习基础，因此关于在子类中的访问权限，我门讲完子类后，在回头讲解
* 成员方法的访问规则和属性完全一样

 ## 281 封装

就是吧抽象出来的数据【属性】和对数据的操作【方法】封装在一起，数据被保护在内部，程序其他部分只有通过被授权的操作【方法】，才能对数据进行操作

**封装的理解和好处**

1、因此实现细节 方法<--调用

2、可以对数据进行验证，保证安全合理

## 282封装实现步骤

1、将属性进行私有化 private 【不能直接修改属性】

2、提供一个公共的public set方法 对与属性**判断**并赋值

3、提供一个公共的public get方法 用于获取属性值

## 283 封装快速入门

如果要使用快捷键运行commant+r需要先配置主类

## 284 封装构造器

我们可以将set方法写在构造器中，这样仍然可以验证

``` java
public Person(String name,int age ,double salary){
  this.setName(name);
  this.setAge(age);
  this.setSalary(salary);
}
```

## 284 封装的课堂练习

## 398 抽象类

父类方法不确定性

当父类当某些方法，需要声明，但是又不确定如何实现时，可以将其声明位抽象方法，那么这个类就是抽象类

所谓抽象方法就是指没有实现的方法（没有方法体）

``` java
public abstract void eat();
```

* 当一个类中存在抽象方法时，需要将该类声明位abstract 类
* 一般来说，抽象类会被继承由其子类实现该方法

## 399 抽象类细节1

* 用abstract关键字来修饰一个类时，这个类就交抽象类

``` java
访问修饰符 abstract 类名{}
```

* 用abstract 关键字来修饰一个方法时，这个方法就是抽象方法

``` java
访问修饰符 abstract 返回类型 方法名(参数列表);
```

* 抽象类的价值更多作用在于设计，时设计者设计好后，让子类继承并实现抽象类()
* 抽象类，时考官比较爱好的知识点，在框架和设计模式使用较多



1、抽象类不能被实例化

2、抽象类不一定要包含abstract方法，也就是说，抽象类可以没有abstract方法，还可以有实现的方法

3、一旦包含了abstract方法，则这个类必须声明位abstract

4、abstract只能修饰类和方法，不能修饰属性和其他的

5、抽象类可以有任意成员[抽象类本质还是类]，比如：非抽象方法，构造器、静态属性等等

6、抽象方法不能有主体，即不能实现

7、如果一个类继承了抽象类，则它必须实现抽象类的所有方法，除非它直接也声明为abstract类

8、抽象方法不能使用private,final和static来修饰，因为这些关键字都是和重写想违背的

## 401 模版设计模式

**案例**

需求

1、有多个类，完成不同的任务job

2、要求统计得到各自完成任务的时间

3、编程实现TestTemplate.java

感情的自然流露

1、先用最容易想到的方法->代码实现

2、分析问题、提出使用模版设计模式

**最佳实践**

设计一个抽象类(Template)，能完成如下功能；

1、变写方法caleTime(),可以计算某段代码的耗时实践

2、编写一个抽象方法code()

3、编写一个子类sub,继承抽象类Template,并实现code方法

4、编写一个测试类TestTemplate，看看是否好用

``` java
abstract vlass Template{
  public abstract void job();
  public void caleTimes(){
    long strat = System.currentTimeMillis();
    job();
    long end = System.currentTimeMillis();
    System.out.println("耗时:"+(end-start));
  }
}
```

## 402-403 接口

接口就是给出一些没有实现的方法，封装到一起，到某个类要使用的时候，在根据具体情况吧方法写出来

语法：

``` java
interface 接口名{
  // 属性
  // 方法（1、抽象。2、默认。3、静态)
}

****

class 类名 inplements 接口{
  自己的属性;
  自己的方法;
  必须实现的接口的抽象方法
}
```

现在jdk7.0前，接口里的所有方法都没有方法体

jdk8后接口类可以有静态方法，默认方法，也就是说接口中可以有方法的具体实现

``` java
interface MyInterface01{
  default public void myMethod(){
    // code
  }
  public static void t2(){
    // code
  }
}
class A implements MyInterface01{}
```

**在接口中，抽象方法可以省略abstract关键字**

一个类使用接口，需要实现接口类所有的抽象方法

## 404-407接口的细节

* 接口不能被实例化
* 几口中所有的方法时public方法，接口中抽象方法可以不用abstract修饰
* 一个普通类实现接口，就必须将该接口的所有方法都实现
* 抽象类实现接口，可以不用实现接口的方法
* 一个类可以同时实现多个接口
* 接口中的属性，只能是final的，而且是public static final修饰符
* 接口中属性的访问形式：接口名.属性名
* 接口不能继承其他的类，但是可以继承多个别的接口
* 接口的修饰符 只能是public 和默认，这点和类的修饰符是一样的

``` java
interface ID extends A,B{}
```

## 409 接口VS继承

当子类继承了父类，就自动的拥有父类的功能

如果子类需要扩展功能，可以通过实现接口的方式扩展

可以理解实现接口是对java单继承机制的一种补充

**接口和继承解决的问题不同**

继承的价值主要在于：解决代码的复用性和可维护性

接口的价值主要在于：设计，设计各种范围（方法），让其他类群实现这些方法。即更加灵活

**接口比继承更加灵活**

接口比继承更加灵活，继承是满足is-a的关系，二接口只需慢煮like0a的关系

接口在一定程度上实现代码解藕

## 接口的多态性

* 多态参数（前面案例体现）InterfacePolyParameter.java

* 多态数组InterfacePolyArr.java

* 接口存在多态传递

  







## 499-568



## 499集合介绍

集合的理解和好处

数组有写不足的地方

1. 长度开始时必须指定，而且一旦指定不能更改
2. 保存的必须为同一类的元素
3. 使用数组进行增加元素的示意代码比较麻烦

集合

1. 可以动态保存任意多个对象，比较方便
2. 提供了一系列方便的操作对象的方法：add、remove、set、get等
3. 使用集合添加，删除新元素的示意代码-简洁了

## 集合体系

集合主要是两组（单列集合，双列集合）

Collection接口由两个重要的子接口List与Set，他们的实现子类都是单列集合

Map接口的实现子类是双列集合，存放的是K-V

## Collection

* Collection接口实现类的特点

``` java
public interface Collection<E> extends iterable<E>
```



1. collection的实现子类可以存放多个元素，每个元素可以是Object
2. 有些Collection的实现类，可以存放重复的元素，有些不可以
3. 有些Collection的实现类，有些是有序的（list)，有些不是有序（set）
4. Collection接口没有直接的实现子类，是通过它的子接口set和list来实现的

Collection接口常用方法，以实现子类ArrayList来演示


| 方法名      | 功能                   |
| ----------- | ---------------------- |
| add         | 添加单个元素           |
| remove      | 删除指定元素           |
| contains    | 查找元素是否存在       |
| size        | 获取元素个数           |
| isEmpty     | 判断是否为空           |
| clear       | 清空                   |
| addAll      | 添加多个元素           |
| containsAll | 查找多个元素是否都存在 |
| removeAll   | 删除多个元素           |

## Collection接口遍历元素方式

1. 使用Iterator（迭代器）
2. Iterator对象称为迭代器，主要用于便利Collection集合中的元素
3. 所有实现了Collection接口的集合类都有一个iterator()方法，用以返回一个实现了Iterator接口的对象，即返回一个迭代器
4. Itertor仅用于遍历集合，Iterator本身并不存放对象

``` java
Iterator iterator = coll.iterator();// 得到一个集合的迭代器
//hasNext():判断是否还有下一个元素
while(iterator.hasNext()){
  //next()作用：1.下移，2.将下移以后的集合位置上的元素返回，返回下一个元素，类型是Object类型
  System.out.println(iterator.next());
}
```

提示：在调用iterator.next()方法之前必须要调用iterator.hasNext()进行检测。若不掉用，且下一条记录无效，直接掉用it.next()会跑出NoSuchElementException异常

快速生成while循环 **itit**

command+j可以把快捷键提示出来

当退出while循环后，这是iterator迭代器指向了最后

如果希望再次遍历，需要重置我们的迭代器（重新得到一个迭代器对象）

## Collection，增强for遍历

增强for循环，可以代替iterator迭代器，特点；增强for就是简化版的iterator

本质一样，只能用于遍历集合或数组

增强for底层就是iterator迭代器

基本语法

``` java
for(元素类型 元素名:集合名或数组名){
  访问元素
}
```

## 505 List

1. list集合类中元素有序（即添加顺序和取出顺序一致）、且可重复
2. list集合汇总的每个元素都有其对应的顺序索引，即支持索引
3. list容器中的元素都对应一个整数型的序号记载其在容器中的位置，可以根据序号存取容器中的元素
4. JDK API中list接口的实现类有 ArrayList、LinkedList、Vector

| 方法名                                    | 功能                                           |
| ----------------------------------------- | ---------------------------------------------- |
| void add(int index,Object ele)            | 在index位置插入ele元素                         |
| boolean addAll(int index,Collection eles) | 从index位置开始将eles中的元素添加进去          |
| Object get(int index)                     | 获取指定index位置的元素                        |
| Int indexOf(Object obj)                   | 返回obj在集合中首次出现的位置                  |
| int lastIndex(Object obj)                 | 返回obj在当前集合中末次出现的位置              |
| Object remove(int index )                 | 移除指定index位置的元素，并返回此元素          |
| Object set(int index,Object ele)          | 设置置顶index位置的元素为ele相当于是替换       |
| List subList(int fromIndex,int toIndex)   | 返回从fromIndex到toIndex位置的子集合，前闭后开 |

## 507 ArrayList，LinkedList，Vector三种遍历方式

1. Iterator
2. 增强for
3. 普通for+get
