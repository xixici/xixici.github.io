---
title: Ubuntu下Matplotlib的安装与SDN仿真
date: 2016-08-10 22:00:23
tags: Matplotlib SDN
categories: 学习笔记
---
帮同学做`SDN(Software Defined Network)`软件定义网络方向的代码仿真,环境的安装与调试如下.

# 安装pip支持

## 下载get-pip 安装包
```
wget https://bootstrap.pypa.io/get-pip.py --no-check-certificate
```
## 安装pip 支持
```
sudo python get-pip.py 
```

# 安装Matplotlib库

- 安装scipy组件
```
sudo apt-get install python-scipy
```
- 安装numpy组件
```
sudo apt-get install python-numpy
```
- 安装 matplotlib
```
sudo apt-get install python-matplotlib
```

# 利用pip安装neworkx
```
sudo pip install networkx
```

# 安装R语言
```
sudo apt-get install r-base
```

<!--more-->

# 运行程序
```
./DO_EVERYTHING.sh 
```

代码报错,并未看到PLOT...郁闷...

# 代码地址
[sdnctrlsim-Github](https://github.com/cryptobanana/sdnctrlsim)

# 后续

报错问题最终解决.生成的PLOT,路径没找对.
