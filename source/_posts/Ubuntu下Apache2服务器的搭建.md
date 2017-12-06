---
title: Ubuntu下Apache2服务器的搭建
date: 2017年2月28日15:43:45
tags: [Apache2,服务器,ubuntu,linux]
categories: 实用工具
keywords: Apache2,ubuntu,ubuntu下搭建Apache2服务器
description: <blockquote class="blockquote-center">刚接触服务器端的开发，今天上班头要求在unbuntu下先搭建一个服务器，于是乎，博主又开始摸索了。嗯～进入正题，楼主选择的是Apache服务器。楼主的系统版本是：Ubuntu Kylin 15.10.</blockquote>
---

<!-- more -->

## Apache服务器的下载与安装

博主选择的是使用apt-get开发包打包的方式安装的。下面是安装步骤：

*  安装apache，在命令行终端中输入以下命令：
```
$ sudo apt-get install apache2
```
* 如果网络连接正常的话，应该是会顺利安装好的，在安装完成之后，需要重启apache服务，在命令行终端中输入如下命令：
```
$ sudo /etc/init.d/apache2 restart
``` 

>  如果重启之后出现如下提示，则表示服务器已经启动成功了。
```
lucas@lucas-ThinkPad-PC:~$ sudo /etc/init.d/apache2 restart
[ ok ] Restarting apache2 (via systemctl): apache2.service.
```
> 可能出现的问题1： NameVirtualHost * :80 has no VirtualHost.
> > 出现上述问题的原因：定义了多个NameVirtualHost，我们只需要将/etc/apahce2/ports.conf 中的NameVirtualHost * :80注释掉即可。

> 可能出现的问题2： Could not reliably determine the server's fully qualified domain name, using 127.0.1.1 for ServerName 
> 1. 原因：根据提示，无法可靠的确定服务器的有效域名，使用127.0.1.1作为服务器域名。因此在下面的测试中，应该使用127.0.1.1，而不是127.0.0.1。
> 2. 解决方法：终端输入`vim /etc/apache2/httpd.conf `，在文件中添加ServerName localhost:80 ，再次restart apache2,就可以使用127.0.0.1来访问web服务器了。

## Apache服务器的测试
既然已经安装好了，name我们当然应该测试一下了。

在浏览器中输入`http://localhost`或者`http://127.0.0.1`，如果看到了It works，那么就说明服务器成功安装了。Apache的默认安装，会在`var/www/`的目录，这个就是我们的web目录了，所有需要能够浏览器访问的web文件都要放在这个目录里。

下面是楼主的测试结果：
![apahce服务器测试结果](http://7xt7l1.com1.z0.glb.clouddn.com/apache2%20%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%90%AD%E5%BB%BA%E6%88%90%E5%8A%9F%E6%B5%8B%E8%AF%95%E5%9B%BE%E7%89%87.jpg)

PS:好了。至此Ubuntu下Apache服务器的安装就已经完成，下面的文章中，我将继续Apache服务器配置文件的详解。