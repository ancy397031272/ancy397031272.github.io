---
layout:     post   				    # 使用的布局（不需要改）
title:      python两个 list 获取交集，并集，差集的方法				# 标题 
subtitle:   转载于：https://www.cnblogs.com/jlf0103/p/8882896.html  #副标题
date:       2020-04-15 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
  - Python
---

## python两个 list 获取交集，并集，差集的方法

1. 获取两个list 的交集：

```
#方法一:
a=[2,3,4,5]
b=[2,5,8]
tmp = [val for val in a if val in b]
print tmp
#[2, 5]

#方法二
print list(set(a).intersection(set(b)))#方法二比方法一快很多！
```

2. 获取两个list 的并集：

```
print list(set(a).union(set(b)))
```

3. 获取两个 list 的差集：

```
print list(set(b).difference(set(a))) # b中有而a中没有的      非常高效！
```