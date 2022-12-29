---
title: Aliyun-CLASSPATH环境属性
date: 2022/11/1 21:33:23
tags: [Java]
categories: [aliyun-java]
---


目录：

1.CLASSPATH的概念

2.CLASSPATH的环境属性

3.添加“.”环境变量

4.PATH和CLASSPATH的区别

 

1CLASSPATH的概念

CLASSPATH如果要完整的进行解释需要好多知识，所以本次只是对CLASSPATH的概念做一个先期的介绍。

假设在d:\mldnjava目录下提供一个Hello.classde 字节码文件：

image.png


 

 

假设当前用户所在的目录为“d:\mldnjava”，这样的情况下直接使用java命令进行Hello.class字节码文件解释：

image.png


 

如果说现在脱离了这个目录，将当前目录修改了“C:\”(C盘目录下并没有Hello.class字节码文件)，如果再次执行程序并解释，这个时候会出现以下错误提示信息：

因为从1.6版本之后，都是多国语言版它会根据你当前的语言系统环境显示中文或英文。1.8版本只能看见前面一部分，1.9版本才可以看见后面一部分。

 

image.png


 

2.CLASSPATH的环境属性

 

出现ClassNotFoundException原因?

当前目录中没有字节码，那么现在的需求就是：可以在不用的目录中都执行

d:\mldnjava\Hello.class文件。所以在这样一个处理要求下只能够依靠CLASSPATH环境属性来完成。

范例：定义CLASSPATH环境属性。

 

image.png


 

SET CLASSPATH=d:\mldnjava

执行代码程序

 

image.png


 

3.添加“.”环境变量

 

当设置了CLASSPATH之后，在java程序解释的时候会自动的通过CLASSPATH所设置的路径进行类的加载，所以可以得出一个结论：JVM解释程序的时候需要得到CLASSPATH的支持。但是有一个问题，发现默认情况下所有解释的类都是从当前所在的目录中加载的，所以可以得出一个结论CLASSPATH的默认设置韦当前所在目录加载类文件。很明显如果到出去设置CLASSPATH就会造成整个操作系统的混乱，那么从正常的角度来讲，对于CLASSPATH来说还是应该采用默认设置方式，所以如果这个时候要想只通过当前目录加载，则可以将CLASSPATH设置为“.”。

范例：从当前所在路径加载类SET CLASSPATH=.

 

image.png

 

如果你安装了一些与Java开发程序软件的时候，它有可能会自动的修改默认的CLASSPATH，这个“.”配置会消失。这种情况下就必修利用命令自己重新设置回来。需要注意的是，现在的CLASSPATH是在一个命令行下的配置，如果该命令行关闭了，那么相关的属性配置也将消失，所以做好将其配置为全局属性，则可以直接在系统中追加有一个属性信息。

 

image.png


 

4.PATH和CLASSPTH区别

 

面试题：请问PATH和CLASSPTH区别？

 PATH:是操作系统提供的路径配置，定义所有可执行程序的路径；

 CLASSPATH:是由JRE提供的，用于定义Java程序解释时类加载路径，默认设置的韦当前所在目录加载，可以“SET=CLASSPATH=路径”的命令形式来进行定义；

 |-关系：JVM →CLASSPATH的定义的路径→加载字节码文件。