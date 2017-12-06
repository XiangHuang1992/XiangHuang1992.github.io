---
title: windows下的cmd神器:Cmder介绍及其设置
date: 2017年2月22日11:46:30
tags: [cmder,cmd.linux,shell]
keywords: cmder,cmd工具,shell,windows,命令行工具
categories: 常用工具
description: <blockquote class="blockquote-center">**Cmder**是windows系统环境下的命令行工具。对于使用过linux系统的人来说，windows下的cmd工具简直让我无法忍受，不过`Cmder`这款工具对于由于某些原因不得不在windows下进行工作的人来说，确实是一个福音。</blockquote>
---


![Cmder主界面](http://7xt7l1.com1.z0.glb.clouddn.com/%E8%BD%AF%E4%BB%B6%E4%B8%BB%E7%95%8C%E9%9D%A2.jpg)

<!-- more -->

## Cmder的安装
cmder官网： [http://cmder.net/](http://cmder.net/ "官网")
Github：[https://github.com/cmderdev/cmder](https://github.com/cmderdev/cmder "github地址")
1. 官网安装
![Cmder官网截图](http://7xt7l1.com1.z0.glb.clouddn.com/cmder%E5%AE%98%E7%BD%91.jpg)
![cmder官网截图download](http://7xt7l1.com1.z0.glb.clouddn.com/cmder%E5%AE%98%E7%BD%91%E6%88%AA%E5%9B%BEdownload.jpg)
在官网上,我们可以看到`Download`模块，分为min版和full版，两者的区别在于：full版集成了`msysgit`工具，是`Git for Windows`的标准配置，除了git本身这个命令之外，里面还有大量的linux命令，比如 grep, curl(没有 wget)； 像vim, grep, tar, unzip, ssh, ls, bash, perl 对于爱折腾的Coder更是痛点需求。

	* 将下载的压缩包解压到你想放置的目录。
	* 点击Cmder.exe即可运行。

## Cmder配置及相关设置

### 乱码和文字重叠
当我们使用`ls`命令查看文件目录时，发现，中文被显示成了一些奇怪的乱码，将以下几行代码配置在`cmder/config/user-aliases`下即可解决问题:
```
l=ls --show-control-chars
la=ls -aF --show-control-chars
ll=ls -alF --show-control-chars
ls=ls --show-control-chars -F
```

如果进行了以上配置还存在乱码问题时，还能尝试进行如下配置：
![cmder乱码设置](http://7xt7l1.com1.z0.glb.clouddn.com/cmder%E7%9A%84win+alt+p%E7%95%8C%E9%9D%A2.jpg)

### 启动Cmder
前文已经说过，Cmder无需安装，解压即可运行。`Cmder`点击`Cmder.exe`即可运行，显然，这样打开是非常不方便的，所以，我们可以进行如下配置：

1. 将cmder添加入环境变量
将`cmder.exe`所在的目录添加至系统环境变量。添加完之后，使用`win+r`输入`cmder`即可运行`Cmder`。
右键点击`我的电脑--->属性`,然后如下图所示进行配置即可：
![cmder环境变量设置](http://7xt7l1.com1.z0.glb.clouddn.com/%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E8%AE%BE%E7%BD%AE.jpg)

2. 添加cmser至右键菜单
能不能将cmder添加到右键，让我们可以在任意文件目录下打开`cmder`呢？如果能这样使用那么简直是不能太赞了！！答案是完全可以的，因为在上一步骤我们已经将`cmder`加入了环境变量，所以我们只需要进行如下配置即可：
```
// 以系统管理员权限打开cmd窗口，输入以下代码，回车即可。
Cmder.exe /REGISTER ALL
```
![cmder here](http://7xt7l1.com1.z0.glb.clouddn.com/cmder%20here.jpg)

### 默认开启设置
作为强大的存在，必然支持私人定制。输入`win + alt + p` 或者 在底部右击点击 `settings`, 进入设置页面；可以根据自己的所需进行各种配置(字体，皮肤等等等等)。

目前游走在前端，Gulp已离不开，`Cmder+PowerShell`这个组合无疑是运行`gulp`的利器。如下图所示，可以设置`PowerShell`作为默认开启的选项；也可以更改默认开启是所在目录。
![cmder powershell](http://7xt7l1.com1.z0.glb.clouddn.com/cmder%20powershell.jpg)

## Cmder常用功能介绍
Cmder功能非常强大，也有许多功能：
1. Cmder常用快捷键
	* `Tab`：自动路径补全
	* `ctrl+T`:建立新页签
	* `ctrl+W`：关闭页签
	* `ctrl+tab`：切换页签
	* `alt_f4`:关闭所有页签
	* `alt+shift+1`:开启cmd.exe
	* `alt+shift+2`:开启powershell.exe
	* `alt+shift+3`:开启powershell.exe（系统管理员权限）
	* `ctrl+1`:快速切换到第一个页签
	* `ctrl+n`:快速切换到第n个页签
	* `alt+enter`:切换到全屏状态
	* `ctrl+r`:历史命令搜索

2. 可在视窗内搜寻画面上曾经出现过的任意字
3. 新增页签按钮，可透过滑鼠新增页签
4. 切换页签按钮，可透过滑鼠切换页签
5. 锁定视窗，让视窗无法再输入
6. 切换视窗是否提供卷轴功能，启动时可查询之前显示过的内容
7. 按下滑鼠左键可开启系统菜单，滑鼠右键可开启工具选项视窗，`win+alt+p`开启工具选项视窗。

## cmder元件组成
`Cmder`集成了多套软体，其中最重要的是`msysgit`、`ConEmu`、`Clink`。
- msysgit除了提供git for windows相关工具之外，还提供了多套Unix/linux环境下常用的指令工具，例如：less、ls、tar、grep等。
- ConEmu体验不如cmder
- Clink将GNU Readline 函式库整合进原生的Windows 命令提示字元视窗，提供命令列模式下强大的编辑与输入能力，这也是用了cmder 之后会这么像在Linux 环境下使用的感觉。

### Chocolatey软件包管理系统
在 Linux 下，大家喜欢用`apt-get(mac下用brew)`来安装应用程序，如今在 windows 下，大家可以使用`Chocolatey`来快速下载搭建一个开发环境。`Chocolatey`的哲学就是完全用命令行来安装应用程序， 它更像一个包管理工具（背后使用`Nuget`）
另外需要说明的是，`Chocolatey`只是把官方下载路径封装到了`Chocolatey`中，所以下载源都是其官方路径，所以下载的一定是合法的，但是如果原软件是需要 Licence 注册的话，那么`Chocolatey`下载安装好的软件还是需要你去购买注册。不过`Chocolatey`一般还是会选用免费 Licence 可用的软件。

安装chocolatey , 运行如下命令即可：
```
@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```
安装软件命令`choco install softwareName`, 短写是`cinst softwareName`
可安装的应用程序，可以参见其 Package列表
以下是window下开发常用的开发环境应用:
```
choco install autohotkey.portable    #安装 AutoHotkey (Portable)
choco install nodejs.install  #安装 node
choco install git.install     #安装 git
choco install ruby            #安装 ruby
choco install python          #安装 python
choco install jdk8            #安装 JDK8
choco install googlechrome    #安装 Chrome
choco install google-chrome-x64 #Google Chrome (64-bit only)
choco install firefox         #安装 firefox
choco install notepadplusplus.install #安装 notepad++
choco install Atom                    #安装 Atom
choco install SublimeText3            #安装 SublimeText3
```

### 其他功能
- `Cmder`还增加了`alias`功能;他让你用短短的指令执行一些常见但指令超长又难以记忆的语法;比如 `ls` `cls`等等；在其控制台输入`alias`可以查看。
- 主控台文字自动放大缩小功能，你只要按下Ctrl+滑鼠滚轮就可以办到;果你用支援两点触控的笔电，也可以在触控板上用两指放大的手势调整文字大小。还有：up，向上翻历史命令;
- Cmder有极为简单的复制粘贴操作。Ctr+V直接粘贴;用鼠标选中你想拷贝的内容，自动就复制到剪切板；天神，这悉数的美感;点赞!
- 自定义aliases:打开Cmder目录下的config文件夹，里面的aliases文件就是我们可以配置的别名文件，只需将里面ls命令的别名按下列方式修改就可以在ls命令下显示中文。