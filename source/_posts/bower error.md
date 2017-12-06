---
title: Bower:Additional error details:Name must be lowercase, can contain digits, dots, dashes, "@" or spaces
date: 2016年9月16日 23:16:22
tags: [Bower,web]
categories: 错误收集
keywords: bower,Bower
description: <blockquote class="blockquote-center">Bower:Additional error details:Name must be lowercase, can contain digits, dots, dashes, "@" or spaces</blockquote>
---

在运行`bower install`安装第三方JS的时候，遇到以下错误提示：

<!-- more -->

```java
E:\nginx-1.10.2\html\parkhero2.0\master>bower install
bower                         EINVALID Failed to read E:\nginx-1.10.2\html\parkhero2.0\master\bower.json

Additional error details:
Name must be lowercase, can contain digits, dots, dashes, "@" or spaces
```
看到这个错误有点懵比，因为一直是可以正常运行的，突然遇到这个错误，然后去检查了一下`bower.json`文件，发现错误的原因是：
```json
  "name": "Park", // 错误就在这里，上面提示了name必须小写，可以包含数字、点、破折号、@和空格
  "version": "2.0.0",
```
好吧，至此问题就解决了。
```
  "name": "park", // 改成小写
  "version": "2.0.0",
```
修改完之后运行`bower install`,正常运行了。这是个小错误，记录一下。