---
title: Coding笔记系列2--初涉前端略有趣
date: 2016-06-22 22:24:51
tags: Coding
categories: 学习笔记
---

`Coding`笔记第二篇.这几天不想看paper,也不想写paper.可能这几天天气太热,心情浮躁,想换换心情.

## HTML5 and CSS

这部分很简单,只要记住命令是自封闭还是配对封闭.也不清楚这么说对不对,一直看英文的.总结几点自己感觉值得记忆的地方:

- `a`标签对应链接href,`p`标签文字记录标签.
- `img`标签对已链接src.
- `.class`css中对应class需要前加`.`
- `#id`css中对应id需要加`#`
- `h1`css中对应标签直接规定

<!--more-->

## Bootstrap

Bootstrap作为最通用的前端框架,用起来简直无脑.

- 自带css `btn` 以及 `btn-default` `btn-primary` ...
- `well` 之前没注意这个样式,超好用
- `ul`无序`ol`有序数字
- `input`中单选`radio`多选`checkbox`

## jQuery

jQ在这里学习太早了吧,所幸还是很简单.

直接给出涉及到的用法
```
<script>
  $(document).ready(function() {
    $("#target1").css("color", "red");						 	
    // css样式 
    $("#target1").prop("disabled", true);						
    // disabled
    $("#target4").remove();										
    // 移除样式
    $("#target2").appendTo("#right-well");						
    // 添加
    $("#target5").clone().appendTo("#left-well");				
    // 克隆下添加
    $("#target1").parent().css("background-color", "red");		
    // 父类
    $("#right-well").children().css("color", "orange");			
    // 子类
    $("#left-well").children().css("color", "green");			
    $(".target:nth-child(2)").addClass("animated bounce");		
    // 层数
    $(".target:even").addClass("animated shake");				
    // 奇偶even odd
    $("body").addClass("animated hinge")						
    // body操作
  });
</script>```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="http://music.163.com/outchain/player?type=2&id=149297&auto=1&height=66"></iframe>