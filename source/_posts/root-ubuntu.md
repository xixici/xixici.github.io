---
title: Ubuntu开启root账户登录后的两条笔记
date: 2016-08-13 19:53:36
tags: Ubuntu
categories: 学习笔记
---


----------


做Hadoop集群时,以root账户登录获取到最高权限.可以避免很多不必要的麻烦.但有两点需要略作修改的bug之处.笔者Ubuntu 14.04 LTS


----------


# ROOT账户登录时界面报错

登录系统时出现
```
Error found when loading /root/.profile
stdin: is not a tty 
```
此时需要更改
```
/root/.profile
```
编辑并修改一样代码如下:
```
gedit /root/.profile # 打开
tty -s && mesg n     # 修改mesg n 的所在行代码
```
然后`重启`系统即可.

----------


# ROOT账户启动Chromium浏览器报错
以ROOT用户启动Chromium时,会报错**不能以根用户身份运行google chrome 浏览器**此时,我最初的解决办法就是以隐身方式打开浏览器.后来找到下面的解决办法,将chromium用户数据文件夹.
<!--more-->
进入下面路径
```
/usr/share/applications/
```

在chromium快捷图标上右键，点击**属性**，在命令属性后添加
```
-user-data-dir
```
即可.


----------


