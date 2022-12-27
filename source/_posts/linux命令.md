---
title: linux命令
date: 2022-11-15 17:49:01
tags:
---

Centos查看版本号的命令：cat /etc/redhat-release
退出vim编辑模式，先按esc键，再按alt+shift+：键，最后输入wq，然后回车。

进程是在 CPU 及内存中运行的程序代码，而每个进程可以创建一个或多个进程
1、查看进程列表：
第一种：top(3秒刷新一次)
    <img src="/images/top.png" width="80%" height="45%"/>
    Tasks（系统任务）信息：total，总进程数；running，正在运行的进程数；sleeping，休眠的进程数；stopped，中止的进程数；zombie，僵死无响应的进程数。CPU信息：us，用户占用；sy，内核占用；ni，优先级调度占用；id，空闲CPU；wa，I/O等待占用；hi，硬件中断占用；si，软件中断占用；st，虚拟化占用。了解空闲的CPU百分比，主要看%id部分。Mem（内存）信息：total，总内存空间；used，已用内存；free，空闲内存；buffers，缓存区域。Swap（交换空间）信息：total，总交换空间；used，已用交换空间；free，空闲交换空间；cached，缓存空间。
第二种：pstree -aup(以树状图的方式展现进程之间的派生关系，显示效果比较直观。)
    -a：显示每个程序的完整指令，包含路径，参数或是常驻服务的标示；
    -c：不使用精简标示法；
    -G：使用VT100终端机的列绘图字符；
    -h：列出树状图时，特别标明现在执行的程序；
    -H<程序识别码>：此参数的效果和指定”-h”参数类似，但特别标明指定的程序；
    -l：采用长列格式显示树状图；
    -n：用程序识别码排序。预设是以程序名称来排序；
    -p：显示程序识别码；
    -u：显示用户名称；
第三种：ps aux(普通)

2、查看进程号：
    ps aux中的PID就是该进程的进程号

3、查看某个服务的进程号
    ps -ef|grep PID

4、杀死某特定进程：
    kill -l PID
    -l选项告诉kill命令用好像启动进程的用户已注销的方式结束进程。当使用该选项时，kill命令也试图杀死所留下的子进程。但这个命令也不是总能成功--或许仍然需要先手工杀死子进程，然后再杀死父进程。

<img src="/images/linux初级命令.jpg" width="80%" height="45%"/>
<img src="/images/linux帮助.jpg" width="80%" height="45%"/>
<img src="/images/linux文件查看.jpg" width="80%" height="45%"/>
<img src="/images/linux重定向.jpg" width="80%" height="45%"/>