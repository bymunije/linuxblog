---
title: Ubuntu安装Rstudio server
author: Bymunije
date: '2019-07-18'
slug: ubuntu安装rstudio-server
categories:
  - Study
tags:
  - Linux
  - R
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
## 1.安装

### 1.1) 要求
- RStudio Server v1.1的最低版本要求是Ubuntu version 12.04
- 已经安装R
- 需要`sudo`权限

### 1.2）安装基础依赖

```
sudo apt-get install gdebi-core
sudo apt-get install libapparmor1
```

### 1.3.1) 下载目前最新版1.1.383

```
wget -P /home/user/software https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb
sudo gdebi /home/user/software/rstudio-server-1.1.383-amd64.deb
```

### 1.3.2) 下载旧版本

```
wget http://download2.rstudio.org/rstudio-server-0.97.551-amd64.deb
gdebi rstudio-server-0.97.551-amd64.deb
```
安装完成后，Rstudio Server会自动启动运行

### 1.4) 查看Rstudio-server是否在运行

```
ps -aux|grep rstudio
```

若显示`rstudio+  1777  0.1  0.0 195676  8476 ?        Ssl  20:47   0:00 /usr/lib/rstudio-server/bin/rserver`,表明安装成功

## 2.配置

配置文件主要有两个，分别是 `/etc/rstudio/rserver.conf `, `/etc/rstudio/rsession.conf`

### 2.1) 设置端口
`sudo vi /etc/rstudio/rserver.conf`打开配置文件，在文件中添加`www-port=31111`并保存，端口需为有效端口

### 2.2）重启服务器

```
sudo rstudio-server restart
```

## 3.网页登录

打开浏览器，在地址栏输入`http://youIP:端口`, 然后输入登录服务器时的用户名和密码

<img src="/Study/2019-07-18-ubuntu安装rstudio-server_files/登录.jpg" alt="登录界面" width="400px" height="300px"/>

## 4.常用命令
- 查看是否安装正确 `sudo rstudio-server verify-installation`
- 查看状态 `sudo rstudio-server status`
- 查看服务端ip地址 `ifconfig`
