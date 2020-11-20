---
date: 2020/11/12
comments: true
title: Ubuntu 18.04 添加新用户

tags: 
  - 技术干货
  - 小知识点
categories: Linux
---



# Ubuntu 18.04 添加新用户



太久没用Linux,每次这些基本的命令都要重新百度找，这里做个记录，方便以后查找。



## 1、创建用户



**命令：**

adduer和useradd，对应着两条删除用户的命令：deluser和userdel



两者的区别：

**adduser:** 会自动为创建的用户指定 **主目录**、**系统shell版本**，而且会在创建时输入**用户密码**。

**useradd:** 需要使用参数手动指定上述的基本设置，如果不使用任何参数，则创建的用户没有密码、主目录，并且没有指定shell版本。



### 1.1 adduser

输入命令：

```shell
sudo adduser tt
```

输出显示：

```shell
[sudo] password for mqk: 
正在添加用户"tt"...
正在添加新组"tt" (1006)...
正在添加新用户"tt" (1006) 到组"tt"...
创建主目录"/home/tt"...
正在从"/etc/skel"复制文件...
输入新的 UNIX 密码： 
重新输入新的 UNIX 密码： 
passwd：已成功更新密码
正在改变 tt 的用户信息
请输入新值，或直接敲回车键以使用默认值
    全名 []: 
    房间号码 []: 
    工作电话 []: 
    家庭电话 []: 
    其它 []: 
这些信息是否正确？ [Y/n] y
```



这样在创建用户名时，就创建了用户的主目录以及密码。

默认情况下：
adduser在创建用户时会主动调用 /etc/adduser.conf；
在创建用户主目录时默认在/home下，而且创建为 /home/用户名

如果主目录已经存在，就不再创建，但是此主目录虽然作为新用户的主目录，而且默认登录时会进入这个目录下，但是这个目录并不是属于新用户，当使用userdel删除新用户时，并不会删除这个主目录，因为这个主目录在创建前已经存在且并不属于这个用户。



为用户指定shell版本为：/bin/bash
因此常用参数选项为：

1. –home： 指定创建主目录的路径，默认是在/home目录下创建用户名同名的目录，这里可以指定；如果主目录同名目录存在，则不再创建，仅在登录时进入主目录。
2. –quiet： 即只打印警告和错误信息，忽略其他信息。
3. –debug： 定位错误信息。
4. –conf： 在创建用户时使用指定的configuration文件。
5. –force-badname： 默认在创建用户时会进行/etc/adduser.conf中的正则表达式检查用户名是否合法，如果想使用弱检查，则使用这个选项，如果不想检查，可以将/etc/adduser.conf中相关选项屏蔽。

![](https://source.acexy.cn/view/XW7p4uI)



### 1.2 useradd

一般不怎么用这个，用到了再补。





## 2、删除用户



### 2.1、deluser

只删除用户：

```she
sudo deluser tt
```

输出显示：

```shel
正在删除用户 'tt'...
警告：组"tt"没有其他成员了。
完成。
```

连同用户的主目录和邮箱一起删除：

```she
sudo deluser --remove-home tt
```

输出显示：

```she
正在寻找要备份或删除的文件...
正在删除文件...
正在删除用户 'tt'...
警告：组"tt"没有其他成员了。
完成。
```

连同用户拥有的所有文件删除：

```she
sudo deluser --remove-all-files tt
```



相关文件：

```she
/etc/passwd - 使 用 者 帐 号 资 讯，可以查看用户信息
/etc/shadow - 使 用 者 帐 号 资 讯 加 密
/etc/group - 群 组 资 讯
/etc/default/useradd - 定 义 资 讯
/etc/login.defs - 系 统 广 义 设 定
/etc/skel - 内 含 定 义 档 的 目 录
```





