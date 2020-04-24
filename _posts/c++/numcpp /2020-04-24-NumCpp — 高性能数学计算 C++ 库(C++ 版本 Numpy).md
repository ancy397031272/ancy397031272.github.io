---
layout:     post   				    # 使用的布局（不需要改）
title:     NumCpp — 高性能数学计算 C++ 库(C++ 版本 Numpy) 				# 标题 
subtitle:   https://www.jianshu.com/p/5a2834599a52 #副标题
date:       2020-04-23 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
   - C++
---

## NumCpp — 高性能数学计算 C++ 库(C++ 版本 Numpy)

NumCpp 是一个高性能的数学计算 C++ 库，它提供了一个简单的 Numpy/Matlab 类似的接口。

**NumCpp中**的主要数据结构是`NdArray`。它本质上是一个 2D 数组类，一维数组实现为1xN数组。还有一个`DataCube`类作为便利容器提供，用于存储2D数组`NdArray`，但它通过简单容器的用途有限。

| **NumPy的**                              | **NumCpp**                                   |
| ---------------------------------------- | -------------------------------------------- |
| `a = np.array([[1, 2], [3, 4], [5, 6]])` | `nc::NdArray a = { {1, 2}, {3, 4}, {5, 6} }` |
| `a.reshape([2, 3])`                      | `a.reshape(2, 3)`                            |
| `a.astype(np.double)`                    | `a.astype()`                                 |

NumCpp 提供了许多初始化函数，它们返回`NdArray`。

| **NumPy的**             | **NumCpp**                |
| ----------------------- | ------------------------- |
| `np.linspace(1, 10, 5)` | `nc::linspace(1, 10, 5)`  |
| `np.arange(3, 7)`       | `nc::arrange(3, 7)`       |
| `np.eye(4)`             | `nc::eye(4)`              |
| `np.zeros([3, 4])`      | `nc::zeros(3, 4)`         |
|                         | `nc::NdArray(3, 4) a = 0` |
| `np.ones([3, 4])`       | `nc::ones(3, 4)`          |
|                         | `nc::NdArray(3, 4) a = 1` |
| `np.nans([3, 4])`       | `nc::nans(3, 4)`          |
|                         |                           |

```
nc::NdArray(3, 4) a = nc::constants::nan
```

|
 | `np.empty([3, 4])` | `nc::empty(3, 4)` |
 |   | `nc::NdArray(3, 4) a;` |