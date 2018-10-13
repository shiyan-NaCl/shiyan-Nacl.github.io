---
layout: post
title:  "CSS学习"
date:   2018-10-12 20:44:05 +0800
categories: blog
---
CSS学习
========================================  

简述：
---------
Web实验三要求自行设计一个CSS样式，看了一晚上教程，写下一些笔记

1.CSS简介
--
层叠样式表(英文全称：Cascading Style Sheets)是一种用来表现HTML（标准通用标记语言的一个应用）或XML（标准通用标记语言的一个子集）等文件样式的计算机语言。CSS不仅可以静态地修饰网页，还可以配合各种脚本语言动态地对网页各元素进行格式化
2.CSS语法
--
![图片1][1]


  [1]: https://www.runoob.com/wp-content/uploads/2013/07/632877C9-2462-41D6-BD0E-F7317E4C42AC.jpg
  CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明:
  一个CSS实例
  p{color:red;text-align:center;font-size:20px}
  
  3.CSS有三种插入样式表的方式
--
  

 - **外部样式**
 每个页面使用 <link> 标签链接到样式表。
在使用外部样式表的情况下，你可以通过改变一个文件来改变整个站点的外观。
即CSS样式在链接的CSS文件中，更加方便，且可以将样式应用于多个界面

 头部连接
link rel="stylesheet" type="text/css" href="mystyle.css"

 - **内部样式**
 使用 style 标签直接在文档头部定义内部样式表



 实例

 head
 style
 hr {color:sienna;}
 p {margin-left:20px;}
 body {background-image:url("images/back40.gif");}
 style
 head

 - **内联样式（又称嵌入样式）**
直接在标签内使用style属性，Style 属性可以包含任何 CSS 属性。

 实例
《p style="color:sienna;margin-left:20px"》这是一个段落。《/p》

 - **样式优先级**
 样式表允许以多种方式规定样式信息。样式可以规定在单个的 HTML 元素中，在 HTML 页的头元素中，或在一个外部的 CSS 文件中。甚至可以在同一个 HTML 文档内部引用多个外部样式表。
但是各样式之间存在优先级


  **（内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式**
  
  待续。。。。。。

  