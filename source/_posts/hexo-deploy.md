---
title: hexo-github部署指南
date: 2016-06-02 20:40:49
tags: hexo github
categories: 学习笔记
---
本博使用的是Hexo+github部署而成,并无花费,只需要一定的技术水平.

## 前期准备
### 申请github账号
github作为一个优秀的代码托管平台,如今的码农世界,第一要求不是你什么项目经验,工作经验,第一点就是你的github账号,对这个开源的代码世界有何贡献,是衡量一个成功代码者的重要标准.

[github官网](https://github.com/)
### 部署git环境
git是一种代码管理方式,是一种免费、开源的分布式版本控制系统.
<!-- more -->
[git下载地址](https://git-scm.com/download/)
### 部署Node.js环境
Node.js是一个Javascript运行环境(runtime).
#### Node.js优点
- RESTful API
- 单线程
Node.js可以在不新增额外线程的情况下，依然可以对任务进行并行处理 —— Node.js是单线程的。它通过事件轮询（event loop）来实现并行操作，对此，我们应该要充分利用这一点 —— 尽可能的避免阻塞操作，取而代之，多使用非阻塞操作。
- 非阻塞IO
- V8虚拟机
- 事件驱动
[node.js下载地址](http://nodejs.cn/) 

## 部署Hexo环境
### 初始化
使用git在任意非中文路径空文件夹,使用命令
```
npm install hexo-cli -g
```
### 部署hexo-deployer-git
```
npm install hexo-deployer-git --save
```
### 生成目录
```
hexo init
```
### 静态化
```
hexo generate
or
hexo g
```
### 部署
```
hexo deploy
or
hexo d
```
### 本地服务
```
hexo server
or 
hexo server -p 5000 #端口号
or
hexo s
```
### 完整部署步骤
```
npm install hexo-cli -g
npm install hexo-deployer-git --save
hexo init
hexo clean # 删除静态文件
hexo g
hexo d
```

## github仓库
建立与用户名一致的Respository,例如用户名为`xixici`,则建立`xixici.github.io`

## config.yml配置修改
修改Hexo站点主目录下config.yml文件中部署部分.如下:
```
deploy: 
  type: git
  repository: http://github.com/xixici/xixici.github.io.git
  branch: master
```
然后部署就需要上述命令
```
hexo g
hexo d
```

## 文章发表
```
hexo new post "markdown tips"
```
## 本人环境

```
$ hexo version # 命令语句
hexo: 3.2.0
hexo-cli: 1.0.1
os: Windows_NT 10.0.10586 win32 x64
http_parser: 2.5.2
node: 4.4.4
v8: 4.5.103.35
uv: 1.8.0
zlib: 1.2.8
ares: 1.10.1-DEV
icu: 56.1
modules: 46
openssl: 1.0.2h

```
## 参考
- [使用Hexo搭建个人博客(基于hexo3.0)
](http://opiece.me/2015/04/09/hexo-guide/)
- [http://baixin.io/2015/08/12/hexo/](http://baixin.io/2015/08/12/hexo/)
- [如何搭建一个独立博客——简明 Github Pages与 jekyll 教程](http://cnfeat.com/blog/2014/05/10/how-to-build-a-blog/)