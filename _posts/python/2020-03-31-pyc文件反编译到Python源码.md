---
layout:     post   				    # 使用的布局（不需要改）
title:      pyc文件反编译到Python源码				# 标题 
subtitle:   转载于：https://blog.csdn.net/Focus_on_linux/article/details/52530022  #副标题
date:       2020-03-31 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
  - Python
---


##  pyc文件反编译到Python源码

使用**uncompyle**
项目地址：https://github.com/wibiti/uncompyle2

注： 按照官方文档的说法应该是只支持python 2.7，其他版本我也没有测试

## 安装
最方便的就是使用pip安装
`pip install uncompyle`

## 使用方法
我使用pip在mac os上安装好后的可执行文件名叫uncompyle6，很奇葩有没有
`uncompyle6 --help 查看帮助`
`uncompyle6 models.pyc > models.py 将models.pyc反编译成py文件`
`uncompile -o . *.pyc 将当前文件夹中所有的pyc文件反编译成后缀名为.pyc_dis的源文件`

## 总结
反编译后的效果可以说很理想，如果你的代码格式符合PEP8规范的要求，那就基本和源来的文件一样，不过各种注释就没有了（不能要求太高是不是）
最后改的代码还没有运行（没有生成pyc）的，就真的丢了，不过不多，再写一遍吧！
问题是解决了，不过最后要反思一下，使用find + rm 删除文件的时候一定要小心，按确认之前一定要再三检查

参考 http://stackoverflow.com/questions/48211/free-python-decompiler-that-is-not-an-online-service/7474393#
