---
title: 'Ubuntu安装Rstudio-server  '
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
---
## 安装（需要`sudo`权限）

### 1.）安装基础依赖

```
sudo apt-get install gdebi-core
sudo apt-get install libapparmor1
```

### 2.1) 下载目前最新版1.1.383

```
wget -P /home/user/software https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb
sudo gdebi /home/user/software/rstudio-server-1.1.383-amd64.deb
```

### 2.2) 下载旧版本

```
wget http://download2.rstudio.org/rstudio-server-0.97.551-amd64.deb
gdebi rstudio-server-0.97.551-amd64.deb
```

### 安装完成后，Rstudio Server会自动启动运行

```
ps -aux|grep rstudio
```

若显示`#rstudio+  1777  0.1  0.0 195676  8476 ?        Ssl  20:47   0:00 /usr/lib/rstudio-server/bin/rserver`,表明安装成功