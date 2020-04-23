---
layout:     post   				    # 使用的布局（不需要改）
title:      Ubuntu添加用户并赋予sudo权限				# 标题 
#subtitle:     #副标题
date:       2020-04-05 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
  - Linux
---

# Ubuntu添加用户并赋予sudo权限

### 创建用户

```
# 在root用户下不用写sudo
sudo adduser ancy  # 在/home 下会自动创建同名文件夹
passwd ancy       # 设置密码，上个命令有时会直接让输入密码，就不需要执行这一步了
```

### 删除用户

```
sudo userdel ancy
```

### 添加sudo权限

- `su -`切换到root

- `vim /etc/sudoers` ，在`root ALL=(ALL) ALL`的下一行添加：

  ```
  # sudo时需要输入密码
  ancy  ALL=(ALL)   ALL
  
  # sudo时不需要输入密码
  ancy ALL=(ALL) NOPASSWD: ALL
  ```

- 按`Esc`，再输入`:wq!`保存文件，要加`!`，不然保存会出问题