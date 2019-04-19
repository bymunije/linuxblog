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
## 1.Linux下python虚拟环境 --> 可自己装package
- 创建环境：`conda create -p /home/byzhang/conda/envs/bymunije`
- 激活环境：`source activate bymunije`
- 退出环境：`source deactivate bymunije`

## 2.Jupyter
### (1).使用
```
jupyter notebook --port='20021' --ip='0.0.0.0
```
- 端口范围：20021-200030
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

## 3.Xshell直接登录服务器

``` 
ssh byzhang@100.64.166.214 22 
```

## 4.Rstudio Server
- server_ip:端口
```
100.64.166.214:20004
```
- 查看状态
```
rstudio-server status
```

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