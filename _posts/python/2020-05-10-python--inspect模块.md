---
layout:     post   				    # 使用的布局（不需要改）
title:      python--inspect模块				# 标题 
subtitle:  https://www.cnblogs.com/yaohong/p/8874154.html #副标题
date:       2020-05-10 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
  - Python
---

# python--inspect模块

**目录**

- [一、type and members](https://www.cnblogs.com/yaohong/p/8874154.html#_label0)
- [二、Retrieving source code](https://www.cnblogs.com/yaohong/p/8874154.html#_label1)
- [三、class and functions](https://www.cnblogs.com/yaohong/p/8874154.html#_label2)
- [四、The interpreter stack](https://www.cnblogs.com/yaohong/p/8874154.html#_label3)

 

**正文**

inspect模块主要提供了四种用处：

　　1.对是否是模块、框架、函数进行类型检查

　　2.获取源码

　　3.获取类或者函数的参数信息

　　4.解析堆栈

 

## 一、type and members

`1. inspect.``getmembers`(object[, predicate])

第二个参数通常可以根据需要调用如下16个方法；

返回值为object的所有成员，以（name,value）对组成的列表

1. inspect.ismodule(object)： 是否为模块
2. inspect.isclass(object)：是否为类
3. inspect.ismethod(object)：是否为方法（bound method written in python）
4. inspect.isfunction(object)：是否为函数(python function, including lambda expression)
5. inspect.isgeneratorfunction(object)：是否为python生成器函数
6. inspect.isgenerator(object):是否为生成器
7. inspect.istraceback(object)： 是否为traceback
8. inspect.isframe(object)：是否为frame
9. inspect.iscode(object)：是否为code
10. inspect.isbuiltin(object)：是否为built-in函数或built-in方法
11. inspect.isroutine(object)：是否为用户自定义或者built-in函数或方法
12. inspect.isabstract(object)：是否为抽象基类
13. inspect.ismethoddescriptor(object)：是否为方法标识符
14. inspect.isdatadescriptor(object)：是否为数字标识符，数字标识符有`__get__` 和`__set__属性； 通常也有__name__和__doc__属性`
15. inspect.isgetsetdescriptor(object)：是否为getset descriptor
16. inspect.ismemberdescriptor(object)：是否为member descriptor

inspect的getmembers()方法可以获取对象（module、class、method等）的如下属性： 

| Type      | Attribute           | Description                                                  | Notes |
| --------- | ------------------- | ------------------------------------------------------------ | ----- |
| module    | __doc__             | documentation string                                         |       |
|           | __file__            | filename (missing for built-in modules)                      |       |
| class     | __doc__             | documentation string                                         |       |
|           | __module__          | name of module in which this class was defined               |       |
| method    | __doc__             | documentation string                                         |       |
|           | __name__            | name with which this method was defined                      |       |
|           | im_class            | class object that asked for this method                      | (1)   |
|           | im_func or __func__ | function object containing implementation of method          |       |
|           | im_self or __self__ | instance to which this method is bound, or `None`            |       |
| function  | __doc__             | documentation string                                         |       |
|           | __name__            | name with which this function was defined                    |       |
|           | func_code           | code object containing compiled function [bytecode](https://docs.python.org/release/2.7.2/glossary.html#term-bytecode) |       |
|           | func_defaults       | tuple of any default values for arguments                    |       |
|           | func_doc            | (same as __doc__)                                            |       |
|           | func_globals        | global namespace in which this function was defined          |       |
|           | func_name           | (same as __name__)                                           |       |
| generator | __iter__            | defined to support iteration over container                  |       |
|           | close               | raises new GeneratorExit exception inside the generator to terminate the iteration |       |
|           | gi_code             | code object                                                  |       |
|           | gi_frame            | frame object or possibly None once the generator has been exhausted |       |
|           | gi_running          | set to 1 when generator is executing, 0 otherwise            |       |
|           | next                | return the next item from the container                      |       |
|           | send                | resumes the generator and “sends” a value that becomes the result of the current yield-expression |       |
|           | throw               | used to raise an exception inside the generator              |       |
| traceback | tb_frame            | frame object at this level                                   |       |
|           | tb_lasti            | index of last attempted instruction in bytecode              |       |
|           | tb_lineno           | current line number in Python source code                    |       |
|           | tb_next             | next inner traceback object (called by this level)           |       |
| frame     | f_back              | next outer frame object (this frame’s caller)                |       |
|           | f_builtins          | builtins namespace seen by this frame                        |       |
|           | f_code              | code object being executed in this frame                     |       |
|           | f_exc_traceback     | traceback if raised in this frame, or `None`                 |       |
|           | f_exc_type          | exception type if raised in this frame, or `None`            |       |
|           | f_exc_value         | exception value if raised in this frame, or `None`           |       |
|           | f_globals           | global namespace seen by this frame                          |       |
|           | f_lasti             | index of last attempted instruction in bytecode              |       |
|           | f_lineno            | current line number in Python source code                    |       |
|           | f_locals            | local namespace seen by this frame                           |       |
|           | f_restricted        | 0 or 1 if frame is in restricted execution mode              |       |
|           | f_trace             | tracing function for this frame, or `None`                   |       |
| code      | co_argcount         | number of arguments (not including * or ** args)             |       |
|           | co_code             | string of raw compiled bytecode                              |       |
|           | co_consts           | tuple of constants used in the bytecode                      |       |
|           | co_filename         | name of file in which this code object was created           |       |
|           | co_firstlineno      | number of first line in Python source code                   |       |
|           | co_flags            | bitmap: 1=optimized `|` 2=newlocals `|` 4=*arg `|`8=**arg    |       |
|           | co_lnotab           | encoded mapping of line numbers to bytecode indices          |       |
|           | co_name             | name with which this code object was defined                 |       |
|           | co_names            | tuple of names of local variables                            |       |
|           | co_nlocals          | number of local variables                                    |       |
|           | co_stacksize        | virtual machine stack space required                         |       |
|           | co_varnames         | tuple of names of arguments and local variables              |       |
| builtin   | __doc__             | documentation string                                         |       |
|           | __name__            | original name of this function or method                     |       |
|           | __self__            | instance to which a method is bound, or `None`               |       |

 

2. `inspect.``getmoduleinf``o`(path)： 返回一个命名元组<named tuple>(name, suffix, mode, module_type)

　　name：模块名（不包括其所在的package）

   suffix：

   mode：open()方法的模式，如：'r', 'a'等

   module_type: 整数，代表了模块的类型

3. `inspect.``getmodulename`(path)：根据path返回模块名（不包括其所在的package）

 

## 二、Retrieving source code

​	1.`insp``ect.``getdoc`(object)： 获取object的documentation信息

2. `inspect.``getcomments`(object)

3. `inspect.``getfile`(object): 返回对象的文件名

4. `inspect.``getmodule`(object)：返回object所属的模块名

5. `inspect.``getsourcefile`(object)： 返回object的python源文件名；object不能使built-in的module, class, mothod

6. `inspect.``getsourcelines`(object)：返回object的python源文件代码的内容，行号+代码行

7. `inspect.``getsource`(object)：以string形式返回object的源代码

8. `inspect.``cleandoc`(doc)：

 

[回到顶部](https://www.cnblogs.com/yaohong/p/8874154.html#_labelTop)

## 三、class and functions

1. `inspect.``getclasstree`(classes[, unique])

2. `inspect.``getargspec`(func)

3. `inspect.``getargvalues`(frame)

4. `inspect.``formatargspec`(args[, varargs, varkw, defaults, formatarg, formatvarargs, formatvarkw, formatvalue, join])

5. `inspect.``formatargvalues`(args[, varargs, varkw, locals, formatarg, formatvarargs, formatvarkw, formatvalue, join])

6. `inspect.``getmro`(cls)： 元组形式返回cls类的基类（包括cls类），以method resolution顺序;通常cls类为元素的第一个元素
7. 7.` inspect.``getcallargs`(func[, *args][, **kwds])：将args和kwds参数到绑定到为func的参数名；对bound方法，也绑定第一个参数（通常为self）到相应的实例；返回字典，对应参数名及其值；

```
>>> from inspect import getcallargs
>>> def f(a, b=1, *pos, **named):
...     pass
>>> getcallargs(f, 1, 2, 3)
{'a': 1, 'named': {}, 'b': 2, 'pos': (3,)}
>>> getcallargs(f, a=2, x=4)
{'a': 2, 'named': {'x': 4}, 'b': 1, 'pos': ()}
>>> getcallargs(f)
Traceback (most recent call last):
...
TypeError: f() takes at least 1 argument (0 given)
```

## 四、The interpreter stack

1. `inspect.``getframeinfo`(frame[, context])

2. `inspect.``getouterframes`(frame[, context])

3. `inspect.``getinnerframes`(traceback[, context])

4. `inspect.``currentframe`()

5. `inspect.``stack`([context])

6. `inspect.``trace`([context])

 

