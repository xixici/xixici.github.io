---
title: markdown学习笔记
date: 2016-05-23 16:58:40
tags: markdown
categories: 学习笔记
mathjax: true
---

当你需要使用一种 **高格调**,又很 **Geek范** 的文字工具来记录自己,分享价值时,**Markdwon**就是你的首选.当你学习一项工具,并且使用它,或许你会花费很大的成本,但是如果你学会了,并使用,你会爱上他.*MarkDown*如是说.

------

## 工欲善其事必先利其器--MarkPad(WIN平台)
MarkPad 是款开源的 Markdown 编辑, Window 8 和谐友好的风格界面。

## Markdown实用语法	
 以下是常用用法,如 **加粗**, **斜体**, **链接**, **列表**, **公式**, **代码**, **表格**等等
 
### 加粗与斜体
``` 
**加粗的用法在这里**
*斜体的用法是这里*```
  **加粗的用法在这里**
 *斜体的用法是这里*
### 标题的用法
```
#标题1
##标题1
......
######标题1
```
`#`的数量的多少与大小有关,类似的还有`-`,自己试验用法吧.
### 链接的写法
```
[XIXICI 主页](http:\\xixici.com\)```

[XIXICI 主页](http:\\xixici.com\)
 	
### 阅读更多
```
<!--more-->```
<!--more-->
### 引用
```
>不能听命于自己者，就要受命于他人。
——尼采《查特拉斯如是说》```
>不能听命于自己者，就要受命于他人。
——尼采《查特拉斯如是说》

###  待办事宜
```
- [ ] 支持以 PDF 格式导出文稿
- [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
- [x] 新增 Todo 列表功能
- [x] 修复 LaTex 公式渲染问题
- [x] 新增 LaTex 公式编号功能
```

- [ ] 支持以 PDF 格式导出文稿
- [ ] 改进 Cmd 渲染算法，使用局部渲染技术提高渲染效率
- [x] 新增 Todo 列表功能
- [x] 修复 LaTex 公式渲染问题
- [x] 新增 LaTex 公式编号功能

### 质能守恒公式

```
$$E=mc^2$$```

$$E=mc^2$$

### 高亮代码

```python
@requires_authorization
class SomeClass:
    pass

if __name__ == '__main__':
    # A comment
    print 'hello world'
```
在整段代码两端加三个\`,  可以对整段代码加高亮.
仅仅对一句代码高亮可以在句子两端加一个\`即可.

### 绘制表格
```
| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | \$1600 |   5     |
| 手机        |   \$12   |   12   |
| 管线        |    \$1    |  234  |
```
| 项目        | 价格   |  数量  |
| --------   | -----:  | :----:  |
| 计算机     | \$1600 |   5     |
| 手机        |   \$12   |   12   |
| 管线        |    \$1    |  234  |

### 网易云音乐插入
```
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=32957377&auto=1&height=66"></iframe>```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=32957377&auto=1&height=66"></iframe>

自动播放将auto=1即可.

Geek的专注在本文表现的淋漓尽致.只用键盘就能写出来这么漂亮(`排版而已`)的文章.

## 参考
- [欢迎使用 Cmd Markdown 编辑阅读器](https://www.zybuluo.com/mdeditor)
- [MarkPad下载地址](http://code52.org/DownmarkerWPF/)
------
