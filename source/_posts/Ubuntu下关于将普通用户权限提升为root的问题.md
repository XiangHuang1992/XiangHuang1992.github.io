---
title: Ubuntu下关于将普通用户权限提升为root的问题
date: 2017年2月28日15:51:21
tags: [ubuntu,root权限]
categories: 问题搜集整理
keywords: ubuntu,root权限
description: <blockquote class="blockquote-center">由于博主刚刚接触linux，所以喜欢吓琢磨。现在记录一下在将普通用户提升为root用户时出现的问题 </blockquote>
---

<!-- more -->

### 问题的由来
* 博主一个好奇就想把自己的那个用户提升为root级别的，所以进行了如下操作。
```
su
vi etc/passwd
然后将自己创建的那个用户（博主的用户名为lucas），对应的值
lucas:x:1000:0:lucas,,,:/home/lucas:/bin/bash
中的1000修改成了和root用户一样的0.

好吧，这下lucas确实成了root用户了，但是问题就来了，你下次登录的适合界面上只剩下客人会话了。其它会话都没了。
```

### 解决措施

```
在用户登录界面，按下 `ctrl+alt+f7`进入命令行界面。
按照如下操作进行：
输入用户名：lucas（博主的）
输入密码：xxxxxx
然后使用vi命令打开我们修改过的文件：/etc/passwd
将0修改成原来的数值。这样我们的登录界面又会出现用户登录啦！
好吧。。至此，问题解决。 
```

PS：博主的Linux系统的Ubuntu kylin 15.10 的版本。具体的原因是ubuntu从12.04开始，添加了额外的root保护，不允许直接开启root账户，强制使账户改为root账户会被屏蔽。所以以后不能再继续作死了。老老实实的用sudo吧。%>_<%。

记录时间：2015年12月10日19:05:05。下班吃饭。