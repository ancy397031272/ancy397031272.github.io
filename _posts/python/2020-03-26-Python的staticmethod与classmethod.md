---
layout:     post   				    # 使用的布局（不需要改）
title:      python的staticmethod与classmethod 				# 标题 
# subtitle:   Hello World, Hello Blog #副标题
date:       2020-03-26 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Python
---
# Python的staticmethod与classmethod

## 1.Python staticmethod修饰符

python staticmethod 返回函数的静态方法。

该方法不强制要求传递参数，如下声明一个静态方法：

```
class C(object):
    @staticmethod
    def f(arg1, arg2, ...):
        ...
```

以上实例声明了静态方法 **f**，从而可以实现实例化使用 **C().f()**，当然也可以不实例化调用该方法 **C.f()**。

#### 函数语法

```
staticmethod(function)
```

参数说明：

- 无

### 实例

```
# -*- coding: UTF-8 -*-


class C(object):
    @staticmethod
    def f():
        print('runoob')


C.f()  # 静态方法无需实例化
cobj = C()
cobj.f()  # 也可以实例化后调用
```

以上实例输出结果为：

```
runoob
runoob
```

## 2.Python classmethod 修饰符

#### 描述

**classmethod** 修饰符对应的函数不需要实例化，不需要 self 参数，但第一个参数需要是表示自身类的 cls 参数，可以来调用类的属性，类的方法，实例化对象等。

#### 语法

classmethod 语法：

```
classmethod
```

#### 参数

- 无。

#### 返回值

返回函数的类方法。

#### 实例

以下实例展示了 classmethod 的使用方法：
class A(object):
    bar = 1

    def func1(self):
        print('foo')
    
    @classmethod
    def func2(cls):
        print('func2')
        print(cls.bar)
        cls().func1()  # 调用 foo 方法
    A.func2()  # 不需要实例化

输出结果为：

```
func2
1
foo
```

