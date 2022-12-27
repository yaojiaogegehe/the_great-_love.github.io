---
title: sqlmap
date: 2022-12-01 19:08:00
tags:
---
以下是sqlmap经典的一些用法：
<img src="/images/sqlmap1.jpg" width="50%" height="45%"/>
以pikachu平台布尔盲注为例，进行讲解：
首先在输入框（这个输入框必须得确定存在SQL漏洞，不然怎么用sqlmap呢？）输入111，然后复制跳转后的网址(url)。打开sqlmap输入命令：
python sqlmap.py -u "这里输入你复制的URL"
随后会报错，出现以下报错提醒：
<img src="/images/错误1.jpg" width="130%" height="120%"/>
这里我们网上查询错误原因后得到如下结果：
<img src="/images/解决1.jpg" width="130%" height="120%"/>
所以我们知道原因是先前输入的命令缺少cookie值，我们返回先前的网页，使用F12到console使用javascript:(document.cookie)
成功得到cookie值：
<img src="/images/解决2.jpg" width="130%" height="120%"/>
随后在sqlmap上再次输入命令：
python sqlmap.py -u "这里输入你复制的URL" --cookie="这里输入先前复制下来的cookie"--batch
即可得到其构造好的payload
如果想要得到其数据库名称，则可以使用下面的命令：
python sqlmap.py -u "URL" --current-db
然后在出现选项后选择Y，之后就出现了当前数据库的名称,就是下图中current database的内容，我们可以知道当前名称是pikachu：
<img src="/images/sqlmap2.jpg" width="130%" height="120%"/>
如果想要获取数据库内表的名称，命令是：
python sqlmap.py -u "URL" -D 数据库名称--tables
得到如下内容：
<img src="/images/sqlmap3.jpg" width="130%" height="120%"/>
同理，想要拿到表里的列名，输入以下命令：
python sqlmap.py -u "URL" -D 数据库名称 -T 数据库中你想查询表的名称 --columns
<img src="/images/sqlmap4.jpg" width="130%" height="120%"/>
最后，我们发现上面的命令只显示列名，我们想要获取列表中的内容，则要使用以下的命令：
python sqlmap.py -u "URL" -D 数据库名称 -T 数据库中你想查询表的名称 -C 表中你想查询的列名 --dump
之后你发现出现如下信息：
<img src="/images/sqlmap5.jpg" width="130%" height="120%"/>
图中信息大致意思是已经找到列中的内容，但其中有加密内容，所以询问你是否将其保存为临时文件让你出去使用别的工具进行破解，但sqlmap本身就包含破解的字典，所以我们这里输入n，之后就会出现提示，询问你是否使用sqlmap自带的字典，我们选择y
<img src="/images/sqlmap6.jpg" width="130%" height="120%"/>
出现上图的三个选项，1是使用sqlmap自带字典进行爆破，2是你自己编写一个字典进行爆破，3是导入你本地字典进行爆破。我们选择1.随后出现下面提示：
do you want to use common password suffixes? (slow!) [y/N]
这个大致意思是询问你是否要用基于后缀的方式进行爆破，如果用了速度会变慢但更精确，这里我们选择n
之后就爆破出了我们想要的内容啦！
<img src="/images/sqlmap7.jpg" width="130%" height="120%"/>