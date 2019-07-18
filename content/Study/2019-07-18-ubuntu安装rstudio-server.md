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
### 2.) 下载目前最新版1.1.383

```
wget -P /home/user/software https://download2.rstudio.org/rstudio-server-1.1.383-amd64.deb
sudo gdebi rstudio-server-1.1.383-amd64.deb
```