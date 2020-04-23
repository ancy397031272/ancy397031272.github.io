---
layout:     post
title:      docker下搭建JupyterNotebook远程登录
subtitle:   
date:       2020-03-26
author:     Ancy
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
  - Docker
---
# docker下搭建JupyterNotebook远程登录

假设你的docker启动方式为：

    docker run -it --runtime=nvidia  -p docker的端口:主机端口  pytorch /bin/bash (可以有多个-p)


1、生成notebook 配置文件：jupyter notebook --generate-config

2、生成密码：jupyter notebook password

3、修改刚刚生成的配置文件~/.jupyter/jupyter_notebook_config.py

    #把前面的#去掉
    c.NotebookApp.ip = '*'    #允许所有ip访问  补充:报错 No address associated with 
    c.NotebookApp.open_browser = False    #不打开浏览器
    c.NotebookApp.port = 8888             #端口为8888
    #这里的密码就是上边我们生成的那一串
    #c.NotebookApp.password = u'sha1:1e39d24dcd6c:b265321ca0c4cb798888bcb69b0024983a8ac439'
    #允许远程访问
    c.NotebookApp.allow_remote_access = True

4.、输入jupyter lab启动jupyter服务即可： jupyter lab --allow-root

5、本机浏览器输入： 192.168.16.6：docker的端口

