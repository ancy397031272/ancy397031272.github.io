---
layout:     post   				    # 使用的布局（不需要改）
title:      Windows 和 Ubuntu双系统时间同步设置方法				# 标题 
# subtitle:   Hello World, Hello Blog #副标题
date:       2020-03-21 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Linux
---
## Windows 和 Ubuntu双系统时间同步设置方法

因Windows把系统硬件时间当作本地时间(localtime)，即操作系统中显示的时间跟BIOS中显示的时间是一样的。
Linux/Unix/Mac把硬件时间当作UTC，操作系统中显示的时间是硬件时间经过换算得来的，比如说北京时间是GMT+8，则系统中显示时间是硬件时间+8。
这样，当PC中同时有多系统共存时，就出现了时间不一致的现象。

###　解决方法：
(1)对于Ubuntu16.04以前的版本，通常都是修改`/etc/default/rcS`文件：
`sudo gedit /etc/default/rcS` 
将UTC=yes改为UTC=no 

(2)对于Ubuntu16.04，修改方法为在terminal中输入如下命令：
`timedatectl   % 查看时间`
`sudo timedatectl set-local-rtc 1  % 修改时间`
`timedatectl  % 查看时间是否修改成功`

