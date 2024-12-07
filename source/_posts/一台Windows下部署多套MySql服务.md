---
title: 一台Windows下部署多套MySql服务
date: 2024-12-06 14:20:41
tags: MySql
categories: 数据库
---

## 1.基础环境

Windows 11

MySql 8.0.39



## 2.安装包下载

https://www.mysql.com/downloads/



{% asset_img download1.png 下载%}



{% asset_img download2.png 下载%}



## 3.安装

### 3.1 解压文件

解压至 C:\MySql\mysql-8.0.39-winx64 (提示: 不建议使用C盘解压)

解压后目录内容如下:

{% asset_img image-20241206145453046.png 下载%}

### 3.2 创建my.ini文件

可以看到没有my.ini的配置文件,需要在当前目录下进行手动创建

**my.ini 是 MySQL 数据库服务器的配置文件。它包含了一系列的配置选项，用于控制 MySQL 服务器的行为，例如服务器的启动参数、存储引擎设置、字符集设置、日志记录选项等诸多方面。**

```ini
[mysql]
# 设置mysql客户端默认字符集为中文
default-character-set=utf8
[mysqld]
#设置端口
port = 3309
# 设置mysql的安装目录
basedir=C:\MySql\mysql-8.0.39-winx64
# 设置mysql数据库的数据的存放目录
datadir=C:\MySql\mysql-8.0.39-winx64\data
# 允许最大连接数
max_connections=200
# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
explicit_defaults_for_timestamp=true
```

### 3.3 安装服务

切换到bin文件夹 (C:\MySql\mysql-8.0.39-winx64\bin)

输入mysqld install MySql_3309 

**MySql_3309是服务名称,可以自定义更改**

{% asset_img image-20241206163654369.png %}

可以看到服务已经被安装成功

{% asset_img image-20241206164726824.png %}

如果没有启动,右键启动即可

### 3.4初始化数据库

输入mysqld --initialize --console

{% asset_img image-20241206164213872.png %}



### 3.5修改数据库密码

使用mysql -u root -p 命令修改报错了，可能是环境问题

所以直接使用了Navacat工具

测试连接

{% asset_img image-20241206164336454.png %}

再次点击数据库连接会提示密码过期,输入新密码。

{% asset_img image-20241206164455230.png %}









**多台部署把文件拷贝至其他文件夹,重复执行此步骤即可。**
