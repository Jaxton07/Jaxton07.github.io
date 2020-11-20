---
date: 2020/11/13
comments: true
title: Win10子系统迁移安装目录到非系统盘

tags: 
  - 技术干货
  - 小知识点
categories: Linux
---



# Win10子系统迁移安装目录到非系统盘



​		因为电脑C盘吃紧，但是win10默认从Microsoft安装的软件都是在C盘的，安装完wsl之后，还要更新软件安装新软件之类的，这又要占用C盘空间，于是想把WSL的安装位置迁移到非系统盘。

​		之前其实就做过一次，这次在另一台电脑上弄的时候，发现操作好像和之前不一样，网上的都是要下一个 LxRunOffline.exe 的软件来辅助转移。有点疑惑，不知道两个的目的是不是一样，或者两个的操作是不是一个意思，主要是一开始用LxRunOffline.exe迁移失败了，最后wsl拒绝访问。然后重新装了WSL，用第一次的方法操作成功。所以不是太清楚这两个具体有哪些区别，但是目的达到了，因为迁移之后WSL安装的软件就没有安装在C盘了。



### 1、查看WSL分发版本

用管理员权限打开 Windows PowerShell ，输入命令：

```shell
wsl -l --all -v
```

显示如下：

```shell
NAME	STATE	VERSION
Ubuntu18.04 Runing 2
```



### 2、导出分发版为**tar**文件到D盘

```shell
wsl --export Ubuntu-18.04 d:\wsl-ubuntu18.04.tar		   #看清楚版本 
```



### 3、注销当前分发版

```shell
wsl --unregister Ubuntu-18.04
```



### 4、重新导入并安装WSL到新的目录下

```shell
# 前面是新目录路径，后面是导出的tar文件的路径
wsl --import Ubuntu-18.04 d:\wsl-ubuntu18.04 d:\wsl-ubuntu18.04.tar --version 2
```



### 5、设置默认登陆用户为安装时用户名

```shell
ubuntu1804 config --default-user Username		#注意前面的版本号，最后Username写自己的用户名
```



### 6、删除tar文件（可选）

```shell
del d:\wsl-ubuntu18.04.tar
```













