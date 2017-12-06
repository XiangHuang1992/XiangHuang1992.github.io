---
title: Ubuntu下jdk环境变量的配置
date: 2017年2月28日15:51:21
tags: [ubuntu,java环境变量,jdk]
categories: java
keywords: ubuntu,jdk,java环境变量
description: <blockquote class="blockquote-center">由于博主刚刚接触linux，记录一下ubuntu下jdk环境变量的配置过程。</blockquote>
---

<!-- more -->

## Linux下jdk环境变量的配置
PS:博主的系统版本是 ubuntu kylin 15.10。
### 下载、及安装
* 下载:http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
* 下载完成之后就是解压了：

> 1. 进入到文件目录下执行该指令`sudo tar zxvf ./jdk-8u65-linux-x64.tar.gz`
> 2. 安装完成之后就是配置环境变量啦
> 2.1 打开/etc/profile文件：` sudo gedit /etc/profile`
> 2.2 添加如下环境变量
```
#set java environment  
  
export JAVA_HOME=/usr/local/java/jdk版本 
  
export JRE_HOME=/usr/local/java/jdk版本/jre  
  
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib:$CLASSPATH  
  
export PATH=$JAVA_HOME/bin:$JRE_HOME/bin:$JAVA_HOME:$PATH 
```
> 2.3 使得修改生效：一种是使用重启的方式使得修改生效，另一种则是使用`source /etc/profile`也可以使修改生效。

> 3. 输入`java -version`测试是否配置成功。
> 3.1 出现以下代码表示配置成功：

```
lucas@lucas-ThinkPad-PC:~/java$ java -version
java version "1.8.0_65"
Java(TM) SE Runtime Environment (build 1.8.0_65-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.65-b01, mixed mode)
```

> 3.2 如出现如下代码：
```
程序 'java' 已包含在下列软件包中：
 * default-jre
 * gcj-4.6-jre-headless
 * gcj-4.7-jre-headless
 * openjdk-7-jre-headless
 * openjdk-6-jre-headless
请尝试：sudo apt-get install <选定的软件包>
```
则可以通过以下方式来解决：
* 在终端输入如下命令：
```
// 这里是输入你的jdk安装目录以及版本号，具体的根据自己的设置去配。
sudo update-alternatives --install /usr/bin/java java /home/lester/develop/jdk1.6.0_37/bin/java 300

sudo update-alternatives --install /usr/bin/javac javac /home/lester/develop/jdk1.6.0_37/bin/javac 300
```
在配置完以上信息之后，再去`java -version` 进行测试。就能看到成功配置的信息啦！～

好了，初次接触linux下的开发，确实会遇到许多的问题，博主会将这些常见的问题一一记录下来，以便自己查看，也为了让其他和我一样刚入门的新手一些参考。