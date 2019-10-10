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
4.推荐插件
`Codefolding`: 代码折叠
`Collapsible Headings`：标题折叠
`Table of Contents(2)`:目录定位
`Code prettify`：自动整理代码，需安装`yapf` 
`Hinterland`：代码自动补全 

### (5). cell代码自动换行

打开根目录`.jupyter/nbconfig/notebook.json`文件，添加如下配置：
```
"MarkdownCell": {
    "cm_config": {
      "lineWrapping": true
    }
  },
  "CodeCell": {
    "cm_config": {
      "lineWrapping": true
    }
  }
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

## 5.Conda创建python虚拟环境 --> 可自己装package

 可参考[这里](https://blog.csdn.net/lyy14011305/article/details/59500819)
 
 1、在所在系统中安装Anaconda如下，若不需要直接跳过,然后在命令行输入`conda -V`检验是否安装以及当前conda的版本
 
- 1).下载需要的anaconda版本并上传到服务器目录，[下载地址：](https://repo.anaconda.com/archive/)

- 2).`cd`到anaconda安装包目录下：

```
bash Anaconda3-5.0.1-Linux-x86_64.sh
```

- 3).按`enter`浏览完协议以后，输入`yes`同意协议,在选择安装路径的时候，按`enter`可安装在默认目录下，或者直接输入想要安装的目录回车，然后提示是否把anaconda加入到系统环境变量中，输入`yes`，最后提示`Do you wish to proceed with the installation of Microsoft VSCode? [yes|no]`，输入`no`，完成后即可运行conda指令

- 4).修改环境变量使用anaconda的python，打开用户目录下的`.bashrc`,添加

```
export PATH="/home/usrname/software/anaconda3/bin:$PATH"
export PYTHONPATH="/home/usrname/software/anaconda3/bin/python"
```

其中`/home/usrname/software/anaconda3/bin`为实际安装目录，然后运行`source  .bashrc`

2、conda常用的命令

    1）`conda list` 查看安装了哪些包

    2）`conda env list` 或 `conda info -e` 查看当前存在哪些虚拟环境

    3）`conda update conda` 检查更新当前conda
 
    4）`source activate your_name` 激活环境

    5）`source deactivate your_name` 退出环境

    6）`conda info --e`查看当前版本分支，多python环境可参考[这里](http://www.afox.cc/archives/390)

3、创建python虚拟环境

     使用 `conda create -n your_env_name python=X.X`（2.7、3.6等)命令创建python版本为X.X、名字为`your_env_name`的虚拟环境

4、使用激活(或切换不同python版本)的虚拟环境

    打开命令行输入`python --version`可以检查当前python的版本

    使用如下命令激活虚拟环境(即将python的版本改变)

    `Linux:  source activate your_env_name(虚拟环境名称)/conda activate your_env_name(虚拟环境名称)`

    `Windows: activate your_env_name(虚拟环境名称)`

5、对虚拟环境中安装额外的包

    使用命令`conda install -n your_env_name [package]`即可安装`package`到`your_env_name`中

6、关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)

   使用如下命令:

   `Linux: source deactivate/conda deactivate`

   `Windows: deactivate`

7、删除虚拟环境

   使用命令`conda remove -n your_env_name(虚拟环境名称) --all`， 即可删除

8、删除环境中的某个包

   使用命令`conda remove --name your_env_name  package_name` 即可

9. 避免退出虚拟环境时进入`base`的虚拟环境

  将`auto_activate_base: false`添加到根目录下的`.condarc`中

