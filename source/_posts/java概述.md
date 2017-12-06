---
title: java概述
description: <blockquote class="blockquote-center">本篇文章主要介绍了一些java语言的基本概述以及java环境变量的配置</blockquote>
date: 2014-10-07 16:37:30
tags: java基础,java,java概述
categories: java基础
keywords: java,java环境变量,java基础
---

<!-- more -->

## Java语言概述

Java是由sun公司推出的java面向对象程序设计语言和java平台的的总称。由James Gosling和同事们共同研发，于1995年正式推出。java最初称为Oak，1995年更名。其特点是：面向对象、通用性、高效性、安全性、跨平台。随着Java技术在web方面的不断成熟，已经成为Web应用程序的首选开发语言。

### java语言的发展

java自从1996年发布1.0版本起，经过近20年的发展，于2014年已发布了java 8版本。
### java语言的三个版本

java语言共有三个版本：
* javase（J2SE，Java2 Platform Standard Edition，标准版）：是在java基础阶段主要学习的内容，包含了构成java语言核心的类，比如：数据库连接、接口定义、输入/输出、网络编程等。
* javaee（J2EE，Java 2 Platform, Enterprise Edition，企业版）：用于服务端处理的企业版。该技术体系中包含的技术如Servlet Jsp等，主要针对于Web应用程序开发。
* javame（J2ME，Java 2 Platform Micro Edition，微型版）：用于手机等嵌入式设备的“微型版”。
其中，Javame目前使用较少，市场上的大多数为android系统和ios系统的手机，都有自己的开发工具来完成软件的开发。

## Java程序设计环境

### Java虚拟机(JVM)

* JVM是Java Virtual Machine（Java虚拟机）的缩写，JVM是一种用于计算设备的规范，它是一个虚构出来的计算机，是通过在实际的计算机上仿真模拟各种计算机功能来实现的。
* JVM是java的核心和基础，在java编译器和os平台之间的虚拟处理器，它是一种基于下层的操作系统和硬件平台并利用软件方法来实现的抽象计算机，可在上面执行java的字节码程序。
* JVM是java实现跨平台性的一个关键，JVM本身并不能跨平台，正是由于JVM在不同的操作系统上有着不同的版本，使得java程序可以“一次编译，反复运行”。

### Java开发环境的搭建

* JDK和JRE
    * JDK(Java development kit):java开发工具包，其中包含了JRE和java开发工具。安装了JDK之后就能运行Java程序。
    * JRE(Java runtime environment):java运行环境。其中包含了JVM和核心类库，如果只是单独的运行java程序，安装JRE即可。
* JDK的下载与安装
    * JDK开发工具箱的下载，可以到Oracle网站，地址是www.oracle.com/technetwork/javajavase/downloads，根据自己电脑的操作系统选择Windows、Linux、Mac OS X等相对应的版本。
* 环境变量的配置
在完成了JDK的安装之后，我们还需要进行环境变量的配置：即将jdk/bin目录添加到执行路径中，在bin目录下存放着一些可执行程序，如javac，java，javadoc等。
配置环境变量的详细过程：
    * 首先，右击【我的电脑】---【属性】-----【高级】---【环境变量】，如图：
    ![环境变量设置一](http://7xt7l1.com1.z0.glb.clouddn.com/%E8%AE%BE%E7%BD%AE%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F--1.jpg)

    * 将你jdk/bin目录加入进path中，以分号结束，但为了以后避免jdk重新安装时又要重新配置变量，我们可以在环境变量中新建一个名为%JAVA_HOME%的变量，变量值为jdk安装目录，再将%JAVA_HOME%/BIN加入到path中，如图：
    ![环境变量配置2](http://7xt7l1.com1.z0.glb.clouddn.com/%E8%AE%BE%E7%BD%AE%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F--2.jpg)![环境变量配置三](http://7xt7l1.com1.z0.glb.clouddn.com/%E8%AE%BE%E7%BD%AE%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F--3.jpg)

    * 测试环境变量是否配置成功，在DOS命令行下输入“javac”，输出帮助信息即为配置正确。如图：
    ![环境变量配置成功](http://7xt7l1.com1.z0.glb.clouddn.com/%E6%B5%8B%E8%AF%95%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E6%98%AF%E5%90%A6%E8%AE%BE%E7%BD%AE%E6%88%90%E5%8A%9F.jpg)

下面提供一下临时配置环境变量的方法：
当我们需要用别人的电脑进行开发，不能对别人电脑的环境变量进行随意更改时，我们可以使用临时配置的方式。
临时的配置方式需要用到DOS命令行中的set命令，例如set path=” D:\Program Files\Java\jdk1.6.0_18\bin”就可以把配置临时的path变量，但是当我们再重新开启一个命令提示符窗口，该path就失去了效果。classpath也是相同的道理。

### java程序编译运行方法

* 使用命令行方式
java程序的编译和运行可以通过dos命令行的方式：
	* 打开一个dos命令行窗口，可通过“win+R”的快捷键组合输入“cmd”的方式打开。
	* 进入到java文件保存的目录。
	* 执行javac文件名.java，对.java文件进行编译，生成.clss文件。
	* 执行java文件名，即可执行该java程序。

下面用一个小程序做一个示范：

```java
public class HelloWorld{
	public static void main(String []args){
		System.out.println("HelloWorld");
	}
}
```

编译运行结果如图所示：
![编译运行结果](http://7xt7l1.com1.z0.glb.clouddn.com/helloworld%E7%BC%96%E8%AF%91%E8%BF%90%E8%A1%8C%E7%BB%93%E6%9E%9C.jpg)
下面是一些dos命令行常用的命令：
> dir：列出当前文件夹目录
> md：创建文件夹
> rd：删除文件夹（必须保证文件夹是空的）
> cd：进入文件目录
> cd..：退回到上一级目录
> cd/：退回到根目录
> del：删除文件
> exit：退出dos命令行

* 使用集成开发工具

我们还可以通过使用java集成工具来进行java程序的开发，这里主要介绍的是如和使用Eclipse编译运行一个程序。Eclipse可以从网站http://eclipse.org上免费下载。使用eclipse的步骤如下：
> 启动eclipse，从菜单栏选择File—>New—>Java Project，打开新建的这个文件，在其中右键new—>class文件。
> 进行java文件的编写
> 编写完java文件之后，右键Run-->Run As-->Java Application即可。

## Java中的注释

* 注释的作用:
	* 1.注解，说明解释我们的程序，提高代码的阅读性
    * 2.调试程序。当程序出现错误时，通过注释可以方便的查找出错的地方。
* 注释的类型：单行注释、多行注释和文档注释三种。
    * 单行注释：//注释文字
    * 多行注释：/*注释文字（可多行）*/  ，多行注释中不能嵌套多行注释
	* 文档注释：/**注释内容*/，是Java特有的注释，通常书写在类、域、构造函数、方法、定义之前。注释内容可以被JDK中的工具javadoc.exe所解析，生成一套以网页文件形式体现的该程序分说明文档。
* 格式如图所示：
![java中的注释](http://7xt7l1.com1.z0.glb.clouddn.com/java%E4%B8%AD%E7%9A%84%E6%B3%A8%E9%87%8A.jpg)

