---
date: 2020/11/18
comments: true
title: 云服务器Ubuntu18.04安装jdk

tags: 
  - java
  - 小知识点
  - 云服务器
categories: Linux
---



# 云服务器Ubuntu18.04安装jdk



linux安装java jdk有几种方式，这里讲下我用的方式。就是下载好jdk压缩包，然后解压包再添加好环境变量。



### 1、下载压缩包

https://www.injdk.cn/

这个网址有java jdk 的oracle版和各个openjdk发行版。因为之前刚在windows 的子系统WSL Ubuntu18.04 上安装了jdk,所以我直接把之前下载到windows电脑上的文件上传到了服务器。

我在 user(自己的用户名)目录下新建了 jdk 文件夹。

```shell
mkdir jdk
```

然后把文件放到 jdk 目录下

![image-20201118171805737](https://gitee.com/ericw5200/image/raw/master/img/image-20201118171805737.png)



### 2、然后解压文件

```shell
tar -xzfv zulu8.48.0.53-ca-jdk8.0.265-linux_x64.tar.gz -C /home/ericw/jdk
```



更改解压出来的文件夹名：

```shell
mv zulu8.48.0.53-ca-jdk8.0.265-linux_x64/ jdk8.0.265
```



### 3、配置环境变量

打开文件:

```shell
sudo vim ~/.bashrc
```



在最后添加：

```shell
#配置环境变量
export JAVA_HOME=/home/ericw/jdk/jdk8.0.265  ## 这里要注意目录要换成自己解压的jdk 目录
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
export PATH=${JAVA_HOME}/bin:$PATH 
```

然后保存退出：

```shell
:wq
```



更新配置文件：

```shell
source ~/.bashrc
```



全部完成，可以查看版本信息验证一下：

![jdk安装完成](https://gitee.com/ericw5200/image/raw/master/img/jdk%E5%AE%89%E8%A3%85%E5%AE%8C%E6%88%90.png)

