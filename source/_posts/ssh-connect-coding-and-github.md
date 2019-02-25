---
title: 配置 SSH 公钥访问 Github 和 Coding 仓库
date: 2019-02-22 11:07:20
tags: github
categories: 学习笔记
---

### 生成公钥

打开命令行终端输入`ssh-keygen -t rsa -C <your_email@example.com>`( 你的邮箱)，连续点击 Enter 键即可。

```
sh-keygen -t rsa -C <your_email@example.com>
# Creates a new ssh key, using the provided email as a label
# Generating public/private rsa key pair.
Enter file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]  // 推荐使用默认地址
Enter passphrase (empty for no passphrase):   //此处点击 Enter 键即可，也可以填写密码，填写密码后每次使用 SSH 方式推送代码时都会要求输入密码，由于这个 Key 也不是用于军事目的，所以也无需设置密码。
```

<!--more-->

成功之后显示如下信息：

```
Your identification has been saved in /Users/you/.ssh/id_rsa.
# Your public key has been saved in /Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

### Coding.net添加公钥

Coding 提供账户 SSH 公钥和项目 SSH 公钥设置。本质上账户公钥和部署公钥是一样的，只是关联的方式不同。同一个 SSH 公钥文件，如果和 Coding 账户关联，便称为账户 SSH 公钥，配置后拥有账户下所有项目的读写权限；如果和具体的某一个项目关联，则称为部署公钥，配置后默认拥有该项目的只读权限。

#### 添加账户公钥

1. 在终端输入`open ~/.ssh`，用文本编辑器打开「id_rsa.pub」文件（此处是生成公钥的默认名称，如果生成公钥时采用了其他名称，打开相对应的文件即可），复制全部内容
2. 登录 Coding.net，进入「账户 -> SSH 公钥」页面，点击「新增公钥」
3. 将第一步中复制的内容填写到「公钥内容」一栏，公钥名称可随意填写
4. 设定公钥有效期，可选择具体日期或设置永久有效

#### 添加部署公钥

1. 在终端输入`open ~/.ssh`，用文本编辑器打开「id_deploy.pub」文件（此处部署公钥名称为「id_deploy.pub」，用户在生成部署公钥的时候完全可以自定义名称），复制全部内容
2. 登录 Coding.net，进入目标项目，点击「设置 -> 部署公钥 -> 新建部署公钥」
3. 将第一步中复制的内容填写到「公钥内容」一栏，公钥名称自定义
4. 点击「添加」，然后输入账户密码即可成功添加部署公钥

## Github.com添加公钥

类似上面

[https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account]: https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account	"GitHub帮助文档"
[https://coding.net/help/doc/git/ssh-key.html]: https://coding.net/help/doc/git/ssh-key.html	"Coding帮助文档"

# 最终测试-重要

添加完成之后, 切记要测试连接如下:

```
ssh -T git@git.coding.net 

ssh -T git@github.com 
```

## 参考
- [https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account)
- [https://coding.net/help/doc/git/ssh-key.html](https://coding.net/help/doc/git/ssh-key.html)