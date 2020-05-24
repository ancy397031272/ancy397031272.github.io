---
layout:     post   				    # 使用的布局（不需要改）
title:    pycharm中添加方法注释（Docstring format & Live Templates）				# 标题 
subtitle:  https://blog.csdn.net/dkjkls/article/details/88933950l #副标题
date:       2020-05-24 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
  - Python
---

# pycharm中添加方法注释（Docstring format & Live Templates）

优雅规范的注释有助于对代码理解，易于与人合作开发，提高效率。但若没有自动化的注释会让写注释耗时耗力。

注释中的要素包括：功能和用途简介、参数、返回值、创建人、创建时间、修改人、修改时间、版权声明、异常抛出。

本文介绍在 pycharm 中使用两种方式进行方法的注释：Docstring format 和 Live Templates。

## 1 Docstring format
### 1.1 Docstring format 添加方法注释
Docstring format 可通过下方路径进行设置，包括五种风格：Plain、Epytext、reStructuredText、Numpy、Google。

`File -> Settings -> Tools -> Python Integrated Tools -> Docstrings -> Docstring format`



使用方式为，在方法名下方输入三个双（单）引号，回车，自动生成。五种风格的样式如下：




```python
def docstrings_func_plain(parm_a, parm_b, parm_c):
    """
    Plain 风格
    """
def docstrings_func_epytext(parm_a, parm_b, parm_c):
    """
    Epytext 风格
@param parm_a: 参数a
@param parm_b: 参数b
@param parm_c: 参数c
@return: 结果a
"""
def docstrings_func_restructuredtext(parm_a, parm_b, parm_c):
    """
    reStructuredText 风格
    :param parm_a: 参数a
    :param parm_b: 参数b
    :param parm_c: 参数c
    :return: 结果a
    """
def docstrings_func_numpy(parm_a, parm_b, parm_c):
"""
NumPy 风格

Parameters
----------
parm_a : 参数a
parm_b : 参数b
parm_c : 参数a

Returns
-------
result_a : 结果a
"""
def docstrings_func_google(parm_a, parm_b, parm_c):
"""
Google 风格

Args:
    parm_a: 参数a
    parm_b: 参数b
    parm_c: 参数c

Returns:
    result_a  结果a
"""
```

### 1.2 Docstring format 添加参数类型注释
Python是动态语言，使用动态类型（Dynamic Typed），即在运行时确定数据类型，变量使用之前不需要类型声明；对于一些已经确定类型的参数，加上类型的注释，可以借助pyCharm的方法类型检查功能，在书写代码时就能够提前发现错误。
下面代码第一行是没加参数类型注释，第二行添加了参数类型注释，pyCharm就可根据方法对应的docstrings提前判断输入参数类型的问题，并给出正确类型提示。

pyCharm中开启插入类型占位符注释路径如下：

`File -> Settings -> Editor -> General -> Smart Keys -> Insert type placeholders in the documentation comment stub`


开启后再使用 Docstring format 添加方法注释，就会出现类型占位符。
对于reStructuredText风格，可将参数类型与参数描述同一行，也可分开书写。
格式化（可通过快捷键查看 Ctrl + Q）的Epytext注释如下：

添加了参数类型的各方法注释如下：

	def docstrings_func_epytext_type(parm_a, parm_b, parm_c):
	"""
	Epytext 风格 - 参数类型
	
	@param parm_a: 参数a
	@type parm_a: int
	@param parm_b: 参数b
	@type parm_b: str
	@param parm_c: 参数c
	@type parm_c: bool
	@return: result_a 结果a
	@rtype: int
	"""
	def docstrings_func_restructuredtext_type(parm_a, parm_b, parm_c):
	"""
	reStructuredText 风格 - 参数类型
	
	:param parm_a: 参数a
	:type parm_a: int
	:param parm_b: 参数b
	:type parm_b: str 
	:param parm_c: 参数c 
	:type parm_c: bool 
	:return: result_a 结果a
	:rtype: int
	"""
	def docstrings_func_restructuredtext_type_2(parm_a, parm_b, parm_c):
	"""
	reStructuredText 风格 - 参数类型 与参数描述同一行
	
	:param int parm_a: 参数a
	:param str parm_b: 参数b
	:param bool parm_c: 参数c
	:return: result_a 结果a
	:rtype: int
	"""
	def docstrings_func_numpy_type(parm_a, parm_b, parm_c):
	"""
	NumPy 风格 - 参数类型
	
	Parameters
	----------
	parm_a : int
	    参数a
	parm_b : str
	    参数b
	parm_c : bool
	    参数c
	
	Returns
	-------
	result_a : int
	    结果a
	"""
	def docstrings_func_google_type(parm_a, parm_b, parm_c):
	"""
	Google 风格 - 参数类型
	
	Args:
	    parm_a (int): 参数a
	    parm_b (str): 参数b
	    parm_c (bool): 参数c
	
	Returns:
	    result_a (int):  结果a
	"""

###  2 Live Templates
Docstring format 已经可以自动格式化输出docstrings，但无法加上创建人、创建时间、修改人、修改时间、版权声明；有些规范建义这些元素写在文件头部，而对于协同开发同一文件，觉得还是需要把这些元素加在各个方法里面，会更清晰明了。

可通过pyCharm的 Live Templates 自定义模板实现。
Live Templates中设置路径如下：

File -> Settings -> Editor -> Live Templates



添加方式如下：

进入 Live Templates 设置页面，点击右方加号，添加 Template Group，再添加 Live Template
在下方添加 Abbreviation（快捷键缩写），Desctiption （快捷键描述）

3. 在下方添加 Applicable（可应用的语言范围）

4. 在 Template text 中添加下方模板代码

"""


Parameters
----------

Returns
-------

:Author:  dkjkls
:Create:  $DATE$ $TIME$
:Blog:    https://blog.csdn.net/dkjkls
Copyright (c) 2019, dkjkls Group All Rights Reserved.
"""
5.在 Edit variables 中配置 DATE 和 TIME，使创建时间自动生成

6. 为了使用注释方便，还可添加 更新时间 和 当前时间


7. 在方法下方输入配置的 Abbreviation，使用 Tab 或 回车 都可自动生成注释，见下方代码

使用 Live Templates 添加方法注释有个问题，方法参数无法自动生成，需要从 Docstring format 方法注释复制。因暂未找到 Live Templates 中解析方法参数的pyCharm内置方法；如 IDEA 中解析方法参数的内置方法 methodName()，解析方法返回参数类型的内置方法 methodReturnType()，methodName() 结合 groovyScript(“def result=’’; def params=”${_1}".replaceAll(’[\\[|\\]|\\s]’, ‘’).split(’,’).toList(); for(i = 0; i < params.size(); i++) {result+=’ * @param ’ + params[i] + ((i < params.size() - 1) ? ‘\n’ : ‘’)}; return result", methodParameters())，可实现在 Live Templates 中解析方法参数并按格式输出。

不知是否是因为pyCharm支持了标准的 Docstring format 而没有设置该方法，找了很长时间都没找到解决方案，期待各大神不吝赐教。

注释代码如下：

	def docstrings_func_live_templates(parm_a, parm_b, parm_c):
	"""
	Live Templates 自定义
	
	Parameters
	----------
	
	Returns
	-------
	
	:Author:  dkjkls
	:Create:  2019/3/31 16:55
	:Blog:    https://blog.csdn.net/dkjkls
	Copyright (c) 2019, dkjkls Group All Rights Reserved.
	"""


	def docstrings_func_live_templates_parm_type(parm_a, parm_b, parm_c):
	"""
	Live Templates 自定义
	
	参数从docstrings_func_restructuredtext复制，暂未找到live_templates中解析方法参数的pyCharm内置方法
	
	IDEA 解析方法参数的内置方法 methodName(), 解析方法返回参数类型的内置方法 methodReturnType()
	
	methodName() 结合 groovyScript("def result=''; def params=; return result", methodParameters())，可实现在live_templates中解析方法参数并按格式输出
	
	Parameters
	----------
	:param int parm_a: 参数a
	:param str parm_b: 参数b
	:param bool parm_c: 参数c
	
	Returns
	-------
	:return: result_a 结果a
	:rtype: int
	
	:Author:  dkjkls
	:Create:  2019/3/31 16:55
	:Blog:    https://blog.csdn.net/dkjkls
	Copyright (c) 2019, dkjkls Group All Rights Reserved.
	"""

参考：
https://www.jetbrains.com/help/pycharm/using-docstrings-to-specify-types.html
https://www.jetbrains.com/help/pycharm/settings-smart-keys.html
