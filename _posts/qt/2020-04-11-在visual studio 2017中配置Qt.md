---
layout:     post
title:      在visual studio 2017中配置Qt
subtitle:   转载于：https://www.cnblogs.com/nyx159/p/7583533.html
date:       2020-04-11
author:     ancy
header-img: img/post-bg-re-vs-ng2.jpgt
catalog: true
tags:
    - Qt
---

# [在VISUAL STUDIO 2017中配置QT](https://www.cnblogs.com/nyx159/p/7583533.html)

# 简述

这两天因为软件工程课要用vs2017写一个C++的GUI界面，就打算学习Qt，但是vs2017配置起Qt来不像vs2013，15那么简单，而且现在网上对于vs2017配置Qt的教程很少，也不详细，我配的时候也找了很多的教程，走了不少坑，最后在陈彦吉学长的帮助下成功在vs2017上配置好了Qt，现在写一个完整的教程以方便他人

# 安装vs2017

首先你要拥有一个能写C++的vs2017（废话……），这个怎么安装vs2017就不用介绍了，不过一定要选择了visual c++

# 下载Qt

进入Qt官方下载页，这里有很多的Qt版本，因为我只在windows10上配置过，别的系统的我不清楚这个方式是否适用，找到适合自己的版本，我下载的是：qt-opensource-windows-x86-msvc2015_64-5.6.3[http://download.qt.io/archive/qt/5.6/5.6.3/]
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231306071-1407627205.png)

# 安装Qt

打开下载的exe, 直接next
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231349993-2127814486.png)

先Skip，不影响最后成功
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231420525-460972883.png)

![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231441993-575028730.png)

选择好路径后下一步
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231512337-698130781.png)

勾选Qt5.6.3，之后下一步，
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231535321-1132642289.png)

开始安装，我安装过了，下面的页面就没有了，不过直接点完成就可以了。

# 配置vs2017

安装完Qt，后打开vs2017，选择（工具 -> 扩展和更新…），这里你们现在应该还没有Qt VS Tools，这个在做完这步之后会出现。
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231610478-1625999008.png)

选择：联机，搜索关键字“Qt”，就会出现相关插件：
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231707165-432388963.png)

安装第一个，安装完后在打开你的vs2017，菜单栏就会出现Qt VS Tools，这时选择Qt->Options：
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231739056-1166438837.png)

点击Add，

![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231803743-1554767178.png)

选择之前安装Qt的路径，不用填名字，他会自动识别
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231835118-906702851.png)

两个Ok。

# 测试一下

新建个Qt项目，选择Qt GUI Application
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231901009-1211970375.png)

不用改，直接一路next，完成项目
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923231958946-259751784.png)

![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232004009-1466266041.png)

![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232009306-732996284.png)

# 最后一步，很重要！

这时一个Qt工程就建好了，但这里还需要改个东西，我第一次安装就是卡在这步了，后来学长帮我找到了贴吧那个教程我改了才成功。
就是将平台改为windows10，点击项目，选择最后的QtGuiApplication1属性
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232048228-851663880.png)

这里windows SDk版本是8.1，你需要将它改为10
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232110056-636778658.png)

![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232125790-1095622956.png)

点击确定
这时就终于配好了。
运行一下它给的样例。
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232159665-1551237626.png)
界面也能出来。
![img](https://images2017.cnblogs.com/blog/1073870/201709/1073870-20170923232213681-400016654.png)

至此，Qt在vs2017上的配置就成功了，大家就可以愉快地学习使用了。