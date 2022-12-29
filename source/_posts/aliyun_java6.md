---
title: Aliyun-java编程起步
date: 2022/11/1 21:33:23
tags: [Java]
categories: [aliyun-java]
---
内容介绍

1.   定义第一个程序代码

2.   类的基本定义

3.   Java的主方法定义

4.   屏幕打印的两种语法形式

 

几乎所有语言的第一个程序都是“Hello World”，因为最初C语言出现的第一个程序编写的就是"你好，世界”，如果要定义Java程序，要通过记事本来进行编写，所有Java程序的后缀都是*.java程序，建立一个目录保存所有程序源代码，建立一个“Hello.java"的源程序。

1.范例:定义第一个程序代码.

publicclassHello {
      publicstaticvoidmain(Stringargs[]){.
             System.out.println("Hello World !");                                     }
}  

 

Java程序是需要经过两次处理后才可以正常执行的: .

•         对源代码程序进行编译:javac Hello.java，会出现有一个 Hello.class.的字节码文件

–         利用JVM进行编译，编译出一套与平台无关的字节码文件(*.class );

•         在JVM上进行程序的解释执行: java Hello.

–         解释的就是字节码文件，字节码文件的后缀是不需要编写的;

 

 为了更加方便的理解java程序的主要结构，下面针对于第一个程序进行完整的解释。

2.在java程序开发之中最基础的单元是类，所有的程序都必须封装在类中执行，而类的基本定义语法如下：

 

[public] class类名称{}

 

 

在本程序之中定义的类名称为“Hello”，而类的定义有两种形式:。

•         “public class类名称{}” ：类名称必须与文件名称保持一致，一个*.java_文件里面只允许有一个public class定义;

•         “class类名称{}”:类名称可以与文件名称不一致，但是编译后的.class名称是class定义的类名称，解析的时候要求解析的是生成的.class文件名称，在一个*.java文件里面可以有多个class定义，并且编译之后会形成不同的*.class文件；

提示:关于以后源代码定义问题.

•         在以后进行项目开发的时候，很少会出现一个* .java源代码里面定义有多个class的情况，而对于以后的开发而言一个* .java文件里面就定义有一个public class类就够了。但是定义了多个文件会产生混乱，所以初期会在一个*.java文件中定义有多个类方便学习。

Java语言有着明确的命名要求，以后定义类名称的时候要求每一个单词的首字母必须大写，例如”HelloWorld“，才算标准。

 

3.主方法：主方法是所有的程序执行的起点，并且一定要定义在类之中

例：Java的主方法定义

[public]class类名称{
      publicstaticvoidmain(String[]args){
             程序的代码由此开始执行 
      }
}

java的主方法名称定义非常长，主方法所在的类都成为”主类“，所有的主类都将采用public class来定义。

 

4.屏幕打印（系统输出)可以直接在命令行方式下进行内容的显示，有两类语法形式:

1.输出之后追加换行:System.out.println(输出内容) ;

 

publiclass He1loworld {
      publicstaticvoidmain(string args []){
             system.out.println("Hello world ! ");
       system .out.println("Hello world ! ");
       system.out.println("He1lo world ! ");
      }
}

 

2.输出之后不追加换行:System.out.print(输出内容)、ln(line 换行)

publicclassHello {
      publicstaticvoidmain(Stringargs[]){
             System.out.print("He1lo");
             system.out.println(" wor1d ! ");
             System.out.println("Hello world ! ");
      }
}