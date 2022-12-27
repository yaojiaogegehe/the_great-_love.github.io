---
title: Html
date: 2022-11-01 16:46:08
tags:
---
hello,今天开启HTML教学。
1、HTML基础

HTML主题

<html>

<body>

中间填入你想要展示的内容

</body>

</html>

其中<html></html>之间文本描述网页

<body></body>之间文本是可见的页面内容

HTML标题是通过<h1>～<h6>来进行定义的

such as：

<h1>this is a heading</h1>

<h2>this is a heading</h2>

……

<h6>this is a heading</h6>

HTML段落是通过<p>标签进行定义

<p>this is a paragraph.</p >

HTML链接是通过<a>进行定义

<a href＝"https://baidu.com">

this is a link</ a>

这就是一个常见的HTML链接，你可以在href属性后面加上你想转往的网址。

注意，https因为有加密协议不能转，这个问题后续学习后解决

HTML图像是通过<img>标签进行定义

< img src＝"文件名.jpg" width＝"104" height＝"142">

其中图像名称和尺寸是以属性的形式提供的

HTML元素

HTML元素语法

HTML元素以开始标签起始，以结束标签终止

元素内容是开始标签与结束标签间的内容

某些HTML元素具有空内容

大多数HTML元素可拥有属性

嵌套的HTML元素

such as:

<html>

<body>

<p>hello world</p >

</body>

</html>


以上就是一个完整的嵌套HTML文档

空的HTML元素

就是<br>，在HTML中可以起到换行的作用


HTML标签是对大小写不敏感的，但以后的发展趋势是向着小写进发的

HTML属性

居中对齐

<h1>定义标题的开始

<h1 aligh＝"center">是一种居中对齐方式对齐，只对于标题

such as：

<h1 aligh＝"center">this is heading</h1>

背景颜色

<body>是定义HTML文档的主体，想要改变背景颜色就要在这个上面进行修改

such as：

<body bgcolor＝"yellow">

</body>

关于属性值都应该加上引号

HTML标题

通过<h1>～<h6>进行定义，<h1>最大，<h6>最小

表标签定义水平线

<hr/>标签在HTML页面创建水平线

such as：

<p>this is a paragraph</p >

<hr/>

<p>this is a paragraph</p >

注释

类似于Python里的#符，格式如下

<!--你想输入的内容-->

such as：

<p>hello world</p >

<!--看不见这段话-->

想研究网页的HTML代码，只需要鼠标右键点击选择查看页面源代码即可

HTML样式

背景颜色

style属性代替了老版本的bgcolor

<body style＝"background-color:yellow">

<p>hello world</p >

</body>

除此之外style还能对页面中的句子进行特别的diy，比如我们想把上面的hello world定制成字体为times，颜色是红，字高（像素高）为50，则我们可以这样修改：

<body style＝"background-color:yellow">

<p style＝"font-size:50px;color:red;font-family:times">hello world</p >

</body>

这样就行了，除此之外还有text-align属性规定了元素中文本的水平对齐方式!

HTML格式化

对于在HTML页面给别人展示代码我们不可能通过<br/>不断换行，这样效率低下，所以我们可以使用<pre>，这个是定义预格式文本定义

such as：

<pre>

这是预格式文本

它可以  保留

空格  和

换行

</pre>

对于如何实现缩写或首字母缩写，可以使用<abbr title＝"你缩写的全称">命令

such as：

<abbr title＝"nimasile">nmsl</abbr>

HTML css

很多时候我们对网页页面的设计需要借助样式表来对页面内容进行格式化其中样式表分为外部样式表和内部样式表

外部样式表

你下载的第三方样式，可以通过更改一个文件来改变整个站点的外观，这个建可以被应用到很多页面

such as：

<head>

<link rel＝"stylesheet" type＝"text/css" href＝"mystyle.css">

</head>

<body>

……

</body>

内部样式表

单个文件需要特别样式时，可以使用

<head>

<style type＝"text/css">

h1｛font-size:50px;color:red｝

p｛color:blue｝

</style>

</head>

<body>

<h1>使用h1样式的句子</h>

<p>使用p样式的句子</p >

</body>