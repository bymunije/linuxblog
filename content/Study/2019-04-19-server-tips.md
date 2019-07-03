---
title: Server Tips
author: Bymunije
date: '2019-04-19'
slug: server-tips
categories:
  - Study
tags:
  - Linux
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
# <font color=orange size=6>Server</font>

## 1.Jupyter
### (1).使用
```
jupyter notebook --port='20021' --ip='0.0.0.0'
```
- 端口范围：
  SS4:20021-200030
  SS1:30021-300030
- ip: server IP

### (2). 设置theme
``` 
jt -t monokai -f fira -fs 13 -cellw 90% -ofs 11 -dfs 11 -T -N 
```
- fira: 字体
- -T： 标题栏

### (3). 更改主题后输出显示不全
打开custom.css文件：
```
div.output_area {
display: -webkit-box;
padding: 13px;
}
```
### (4). 安装Nbextensions标签页
1.安装nbextensions
```
pip install jupyter_contrib_nbextensions -i https://pypi.mirrors.ustc.edu.cn/simple
jupyter contrib nbextension install --user
```
2.安装nbextensions_configurator
```
pip install --user jupyter_nbextensions_configurator 
jupyter nbextensions_configurator enable --user
```
3.显示nbextensions
```
python -m pip install --user jupyter_contrib_nbextensions
```

## 2.Xshell直接登录服务器

``` 
ssh byzhang@100.64.166.214 22 
```

## 3.Rstudio Server
- server_ip:端口
  - SS1:20004
    SS4:20014
  
```
100.64.166.214:20004
```
- 查看状态

```
rstudio-server status
```
## 4.Vim配置

打开`/home/`下的`.vimrc`,配置如下：

```
  syntax on                   " 自动语法高亮
  set number                  " 显示行号
  set cursorline              " 突出显示当前行
  set ruler                   " 打开状态栏标尺
  set statusline=[%F]%y%r%m%*%=[Line:%l/%L,Column:%c][%p%%]
  set tabstop=4               " 设定 tab 长度为 4
  set expandtab               " 输入tab自动转为空格
  filetype plugin indent on   " 开启插件
  set ignorecase smartcase    " 搜索时忽略大小写，但在有一个或以上大写字母时仍保持对大小写敏感
  set incsearch               " 输入搜索内容时就显示搜索结果
  set hlsearch                " 搜索时高亮显示被找到的文本
  set mouse=a                 " 设置鼠标定位
  set bg=dark                 " 显示不同的底色色调
  set showmode                " 左下角那一行的状态
  set autoindent              " 自动缩排
  set backspace=2             " 可随时用退格键删除
  set ff=unix                 " 使用unix换行符
  set listchars=eol:$,tab:>-,trail:~,extends:>,precedes:- " 文本高亮和tab
  
 ```
 
- 设置vim中鼠标定位后，可通过`shift`+ 鼠标复制，可参考[这里](https://blog.csdn.net/sinkary/article/details/7531747)

***
# <font color=orange size=6>cmd</font>
## 1.传输文件
```
scp byzhang@100.64.166.214:/home/byzhang/data/cell_line/split_wild_mut/split_mut_wild/split_mut_wild_all.txt C:/Users/zhang/Desktop/试试/
```
- byzhang@100.64.166.214: 服务器

***
## <font color=orange size=6>awk</font>
### 1.Summary
- $0：整行
- 从1开始计数
- 只能有一对单引号
- 语句结束加分号(;)

### 2. Note
- BEGIN:从第一行开始
- FS:输入字段分隔符，默认空格
- OFS:输出字段分隔符，默认空格
- ||/&&: 或/与

```
cat file.txt | awk 'BEGIN {FS="\t";OFS="\t"} {if ($20 == "%" || $20 == "%%") {$23 = $14; print $0} else if ($20 != "%" && $20 != "%%") {$23 = $22; print $0}}' > file2.txt
```
***
## <font color=orange size=6>Vim</font>

### 1.set list:查看分隔符

***
## <font color=orange size=6>ps</font>
### 1.查看用户所有进程
```
ps -aux | grep byzhang
```

***
## <font color=orange size=6>du</font>
### 1.查看占用磁盘大小
```
du -sh
```

***
## <font color=orange size=6>Common code</font>
### 1.查看文件夹下文件数目
```
  ls -l | grep '^-' | wc -l
```
