---
layout:     post   				    # 使用的布局（不需要改）
title:      Python实用模块fire 				# 标题 
subtitle:   转载于：https://xugaoxiang.com/2019/12/03/python-module-fire/
date:       2020-03-28				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Python
---

# Python实用模块fire

#### 软硬件环境

- ubuntu 18.04 64bit
- anaconda3 with [python](https://xugaoxiang.com/tag/python/) 3.7.1
- fire

### fire

`fire`与[python实用模块推荐(1)_click_pathlib](https://blog.xugaoxiang.com/python/python-module-recommend.html)中介绍过`click`模块功能类似，但是`fire`使用起来更加的方便简单(基本上不用写代码及文档注释)，功能更加强大。

安装`fire`

```bash
pip install fire
import fire

def hello(name):
  return 'Hello {name}!'.format(name=name)

if __name__ == '__main__':
  fire.Fire()
```

如上面的示例所示，只需要`fire.Fire()`就完成了命令行参数的构建，运行方法是

```bash
python example.py hello world
```

其中`example.py`是文件名，`hello`是方法名，`world`是传递给`hello`方法的参数；另外你可以明确的给方法构建，如下调用`fire.Fire(hello)`，那么运行的时候就可以省略掉`hello`方法了，`python example.py world`

`fire.Fire()`的参数可以是方法，对象，类，字典，来看个字典的例子

```python
import fire

def add(x, y):
  return x + y

def multiply(x, y):
  return x * y

if __name__ == '__main__':
  fire.Fire({
      'add': add,
      'multiply': multiply,
  })
```

运行

```bash
$ python example.py add 1 2
3
$ python example.py multiply 3 4
12
```

如果参数是类的话，跟字典传递的功能类似，即类的每个方法都可以接受命令行参数。

### 参考资料

- https://github.com/google/python-fire