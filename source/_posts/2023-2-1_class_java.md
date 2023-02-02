---
title: Java面向对象编程
date: 2023/2/1 12:31:32
tags: [技术分享]
---
## Java面向对象编程

## 面向对象简介

面向对象过程指的是面对于一个问题的解决方案，更多的情况下是不会做出重用的设计形式为模块化设计，并且可以进行重用配置
面向对象三大特征：
    封装性：内部的操作对外部而言不可见；当内部操作都不可直接使用的时候才是最安全的；
    继承性：在已有结构的基础上继续进行功能的扩充；
    多态性：是在继承性的基础上扩充而来的概念，指的是类型的转换处理。
面向对象开发的三个步骤：
    OOA：面向对象分析；
    OOD：面向对象设计；
    OOP：面向对象编程；

## 类与对象简介

面向对象中最重要的两部分："类"和“对象”
1）类：“创建对象的标准”
类是对某一类事务的共性的抽象概念，而对象描述的是一个具体的产物（类只是一个设计的模板，而对象才是将类可以使用的实例，比如：创造一辆汽车所有部件及图纸信息是一个类，而对象是将他们拼接好以后行程的实例的成品）；

类有两部分组成：
    1、成员属性（Field）有些时候为了简化称其为属性
        举例：一个人具有：年龄，名字，身高，性别，头发，眼睛，耳朵，鼻子，胳膊，腿儿组成的这是一个人的属性
    2、操作方法（Method）定义对象具有的处理行为；
        举例：成员属性定义的一个人，这个人可以做哪些事情，比如：唱歌，跳舞，游泳，运动等等

## 类与对象定义

在Java中类是一个独立的结构体，所以需要使用class来进行定义，而在类之中主要由属性和方法所组成，那么属性就是一个个具体的变量，方法就是可以重复执行的代码

定义一个类

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄："+age);
    }
}

public class JavaDemo{
    public static void main (String args []){

    }
}
```

现在有了类之后，如果想使用类就必须要用使用对象来完成，如果要产生对象，那必须使用如下语法格式来完成
    声明并实例化对象： 类名称 对象名称 = new 类名称();
    分布步骤：
        - 声明对象：类名称 对象名称 = null;
        -实例化对象：对象名称 = new 类名称;
当获取类实例化对象之后，那么就需要需要通过对象进行类中的操作调用，此时有两种调用方式
    调用类中的属性：实例化对象.成员属性
    调用类中的放啊放：实例化对象.方法名称()

范例：
实际开发时，主类和其他类要分开

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄："+age);
    }
}

public class JavaDemo{
    public static void main (String args []){
        Person per = new Person();//声明并实例化对象
        per.name = "张三" ；
        per.age = 18 ;
        per.tell();
    }
}
```

如果此时的程序你并没有进行对象属性内容的设置，则该内容为其对应数据类型的默认值
String是引用数据类型所以默认值为null，int是基本数据类型所以默认值为0
boolean默认值是false

## 对象内存分析

代码引用传递
Java之中类属于引用数据类型，引用数据类型最大的困难之处在于要进行内存的管理，同时在进行操作的时候也会发生有内存关系的变化，所以本次针对于之前的程序的内存关系进行一些简单分析
案例：以下面程序为主进行分析

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = new Person();//声明并实例化对象
//        per.name = "张三" ;
//        per.age = 18 ;
        per.tell();
    }
}
```
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_1.png)
-- -
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_2.png)
-- -
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_3.png)
-- -
![] (https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_4.png)
如果要进行内存分析，那么首先给出两块最为常用的内存空间：
    ‒ 堆内存：保存的是对象的具体信息，在程序中堆内存的空间开辟是通过new完成的
    ‒ 栈内存：保存的是一块堆内存的地址，即：通过地址找到堆内存，而后找到对象内容，但是为了分析简化起见可以简单的理解为：对象名称保存在栈内存中

清楚了以上的对应关系后，那么下面就针对于之前的程序进行分析

在之前进行分析的时候可以发现对象的实例化有两种语法，一种是之前使用的声明并实例化对象，另一种就是分步完成，所以下面针对分步的那内存操作进行分析

范例：

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = null;//声明对象
per = new Person() ; // 实例化对象
        per.name = "张三" ;
        per.age = 18 ;
        per.tell();
    }
}
```

下面通过内存分析来进行操作
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_5.png)
需要特别引起注意的是，所有的对象在调用类中的属性和方法时候，必须要实例化完成后才可以执行
范例：错误代码

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = null;//声明对象
        per.name = "张三" ;
        per.age = 18 ;
        per.tell();
    }
}
```

代码之中只是声明了对象，但是并没有为对象进行实例化，所以此时无法调用。而此时程序中出现的NullPointerException（空指针异常），就是在没有在堆内存开辟后时所产生的问题，并且只有引用数据类型存在此问题
Java之中类属于引用数据类型，引用数据类型最大的困难之处在于要进行内存的管理，同时在进行操作的时候也会发生有内存关系的变化，所以本次针对于之前的程序的内存关系进行一些简单分析
案例：以下面程序为主进行分析

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = new Person();//声明并实例化对象
//        per.name = "张三" ;
//        per.age = 18 ;
        per.tell();
    }
}
```

如果要进行内存分析，那么首先给出两块最为常用的内存空间：
‒ 堆内存：保存的是对象的具体信息，在程序中堆内存的空间开辟是通过new完成的
‒ 栈内存：保存的是一块堆内存的地址，即：通过地址找到堆内存，而后找到对象内容，但是为了分析简化起见可以简单的理解为：对象名称保存在栈内存中

清楚了以上的对应关系后，那么下面就针对于之前的程序进行分析

在之前进行分析的时候可以发现对象的实例化有两种语法，一种是之前使用的声明并实例化对象，另一种就是分步完成，所以下面针对分步的那内存操作进行分析

范例：

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = null;//声明对象
per = new Person() ; // 实例化对象
        per.name = "张三" ;
        per.age = 18 ;
        per.tell();
    }
}
```

下面通过内存分析来进行操作

需要特别引起注意的是，所有的对象在调用类中的属性和方法时候，必须要实例化完成后才可以执行
范例：错误代码

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = null;//声明对象
        per.name = "张三" ;
        per.age = 18 ;
        per.tell();
    }
}
```

代码之中只是声明了对象，但是并没有为对象进行实例化，所以此时无法调用。而此时程序中出现的NullPointerException（空指针异常），就是在没有在堆内存开辟后时所产生的问题，并且只有引用数据类型存在此问题

## 引用传递分析

类本身属于引用数据类型，既然是引用数据类型，就会牵扯到内存的引用传递，所谓的引用传递的本质：同一块堆内存空间可以被不同的栈内存指向，也可以更换指向

范例：定义一个引用传递

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
//        Person per = new Person();//声明并实例化对象
        Person per1 = new Person() ;
        per1.name = "张三" ;
        per1.age = 18 ;
Person per2 = per1;// 引用传递
per2.age = 80 ;
        per1.tell();
    }
}
```

这个时候的引用传递是直接在主方法之中定义的，也可以通过方法实现引用传递处理
范例：利用方法实现引用传递处理

``` java
class Person {  // 定义一个类
    String name ;  // 人员的姓名
    int age ;
    public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age );
    }
}

public class JavaDemo1{
    public static void main (String[] args){
        Person per = new Person() ;
        per.name = "张三" ;
        per.age = 18 ;
        changeInfo(per); // 等价于Person temp = per 
        per.tell();
    }
    public static void changeInfo(Person temp){
        temp.age = 80 ;
    }
}
```
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_6.png)
与之前的差别最大的地方在于，此时的程序是将Person类的实例化对象（内存地址，数值），传递到了changge（）方法之中，由于传递的是一个Person类型，那么change（）方法接收的也是Person类型

引用传递可以发生在方法上，这个时候一定要观察方法的参数类型，同时也要观察方法的执行过程

## 引用与垃圾产生分析

引用传递与垃圾产生分析
经过了一系列的分析之后已经确认，所有的引用传递的本质就是一场堆内存的调戏游戏。
但是对于引用传递如果处理不当，
那么也会造成垃圾的产生，那么本次将针对于垃圾产生原因进行简单分析。.范例:定义一个要分析的程序.、
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_7.png)
此时已经明确发生了引用传递，并且也成功的完成了引用传递的处理操作，但是下面来观察一下其.内存的分配处理流程。

一个栈内存只能够保存有一个堆内存的地址数据，如果发生更改，则之前的地址数据将彻底消失。
![](https://blog-alan.oss-cn-hangzhou.aliyuncs.com/java_aliyun/class_8.png)
所谓的垃圾空间指的就是没有任何栈内存所指向的堆内存空间，所有的垃圾将被GC ( Garbage Collector、垃圾收集器)|
不定期]进行回收并且释放无用内存空间，但是如果垃圾过多，一定将影响到GC的处理性能，从而降低整体的程序性能，那么在实际的.开发之中，对于垃圾的产生应该越少.越好。

## 成员属性封装

在类中的组成就是属性和方法，一般而言方法都是对外提供服务的，所以是不会进行封装处理，而对于属性由于其需要较高的安全性，所以往往需要对其进行保护，这个时候就需要采用封装性对属性进行保护
在默认的情况下，对于类中的属性是可以通过利用其他类利用对象进行调用的

范例：属性不封装情况下的问题

``` java
class Person {  // 定义一个类     String name ;  // 人员的姓名     int age ;    
     public void tell (){
        System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{  //主类
    public static void main (String[] args){         
        Person per = new Person();//声明并实例化对象         
per.name = "张三" ;  //在类外部修改属性
        per.age = 18 ;     //在类外部修改属性
        per.tell();     
    }
}
```

此时在person类中提供的name和age两个属性并没有进行封装处理，这样外部就能进行调用了，但是有可能所设置的数据是错误的数据。如果要想解决这样的问题就可以利用private关键字对属性进行封装处理。

范例：对属性进行封装

``` java
class Person {  // 定义一个类     
private String name ;  // 人员的姓名          private  int age ;    
        public void tell (){
           System.out.println("姓名："+name+"，年龄：" + age  );
    }
}

public class JavaDemo1{  //主类
    public static void main (String[] args){         
        Person per = new Person();//声明并实例化对象         
per.name = "张三" ;  //在类外部修改属性
        per.age = 18 ;     //在类外部修改属性
        per.tell();     
    }
}
```

而属性一旦封装之后外部将不能够直接访问，即：外部不可见，但是对类的内部是可见的，那么如果要想让外部的程序可以访问封装的属性，，则在Java开发标准中提供有如下要求
‒ 【setter，getter】设置或取得属性可以使用setXxx（），getXxx（）方法，以private string name为例

```
‒ 设置属性的方法：public void setName（String n）；
‒ 获取属性方法：public String getName();
```

范例：实现封装

``` java
class Person {  // 定义一个类     
private String name ;  // 人员的姓名          private  int age ;    
        public void tell (){
           System.out.println("姓名："+name+"，年龄：" + age  );
public void setName（String n）{
name = n ;
}
public void setAge(int a){
if(a >= 0){
age = a ;
}
}
public String getName(){
return name ;
}
public String getAge(){
return age ;
}
    }
}

public class JavaDemo1{  //主类
    public static void main (String[] args){         
        Person per = new Person();//声明并实例化对象         
per.setName("张三") ;  //在类外部修改属性
        per.age(-18) ;     //在类外部修改属性
        per.tell();     
    }
}
```
在以后进行任何类定义的时候一定要记住，类中所有属性都必须使用private封装。（98%），并且属性要进行访问必须要提供有setter，getter方法。

## 构造方法与匿名对象

现在程序在使用类的时候一般都按照类如下的步骤进行：
	``● 声明并实例化对象，这个时候实例化对象中的属性并没有任何的数据存在，都是其数据类型的默认值
	``● 需要通过一系列的setter方法为类中的属性设置内容
等于说现在要想真正获得一个可以正常使用的实例化对象，必须通过两个步骤才可以实现。
8个属性就要有8个setter
专门提供有构造方法：通过构造方法实现对象中的属性初始化处理。只有在关键字new的时候构造方法。定义：
	``● 方法名称必须与类名称保持一致；
	``● 构造方法不允许设置任何的返回值类型，即没有返回值定义；
	``● 构造方法是在使用关键字new实例化对象的时候自动调用的
Person per = new Person("张三",18);
对象实例化格式对比

 主要是定义对象所属类型，类型决定了你可以调用的方法；
 实例化对象的名称，所有的操作通过对象来进行访问；
 开辟一块新的堆内存空间；
调用有参构造、 调用无参构造
在Java程序里面考虑到程序结构的完整性，所有的类都会提供构造方法，也就是说你的类中没有任何的构造方法，那么系统自动创建什么都不做的构造方法，这个无参构造方法在程序编译的时候自动创建的。
如果有一个构造方法的时候，这个默认的构造方法将不会被自动创建。
一个类至少存在一个构造方法，永恒存在。
既然构造方法本身是一个方法，那么方法就是具有重载的特点，而构造方法重载的时候只需要考虑类型和参数个数。
范例：构造方法重载
在进行多个构造方法定义的时候，强烈建议大家有一些定义的顺序，例如：可以按照参数的个数降序或升序排列。
经过分析可以发现，构造方法的确是可以进行数据的设置，而对于setter也可以进行数据的设置，这个时候要清楚，构造方法是在对象实例化的时候为属性设置初始化内容，而setter除了拥有设置数据的功能之外，还具有修改数据的功能。
经过分析之后可以发现，利用构造方法可以传递属性数据，于是现在进一步分析对象的产生格式：
	``● 定义对象的名称：类名称 对象名称 = null；
	``● 实例化对象：对象名称 = new 类名称()
如果这个时候只是通过实例化对象来进行类的操作也是可以的，而这种形式的对象由于没有名字，我们叫他匿名对象。
此时依然通过了对象进行了类中tell()方法的调用。但是由于此对象没有任何的引用，所以该对象使用一次之后就将成为垃圾，而所有的垃圾将被GC进行回收与释放。
