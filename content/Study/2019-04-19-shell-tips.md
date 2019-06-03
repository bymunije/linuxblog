---
title: shell tips
author: Bymunije
date: '2019-04-19'
slug: shell-tips
categories:
  - Study
tags: 
  - Shell
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
# 代码
## 1.add header
```
#!/bin/bash
for file in /home/byzhang/data/Drug_combination/header/*.txt
do
	file_name_txt=`basename $file`
	file_name=${file_name_txt%.*}
	add_header=${file_name}_header.txt
	echo $add_header
	head -n 1 ${file} > ./header/add_header/${add_header}
done


cd /home/byzhang/data/Drug_combination/header/add_header
paste SL_score_first_modify_header.txt Cancer_Mutation_Score_Modify_header.txt cancer_gene_sensus_TSG_header.txt Drug_Target_inhibitor_all_deduplication_header.txt | tr -d "\r" > add_header.txt 
```
```
#!/bin/bash
for file in ./no_header_wt/*.txt
do
	 file_name=${file##.*/}
	 #split_mut_wild_wt_PTGS2+TP53_Valdecoxib-341.txt
	 before=${file_name%-*}
	 #split_mut_wild_wt_TOP1+TP53_Topotecan
	 Index_txt=${file_name##s*-}
	 #split_mut_wild_wt_TOP1+TP53_Topotecan-
	 Index=_${Index_txt%.*t}
	 #number
	 withHeader="_withHeader.txt"
	 add_withHeader="$before$Index$withHeader"
	 # echo ${file_name} , ${before} , ${Index} , ${add_withHeader}
	cat split_mut_wild_selected_GDSC_header.txt ${file} > ./split_every_drug_wt_withHeader/${add_withHeader}
done
```
# Conda创建python虚拟环境 --> 可自己装package

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
export PATH=/home/byzhang/software/anaconda3/bin:$PATH
export PYTHONPATH="/home/byzhang/software/anaconda3/bin/python"
```

其中`/home/byzhang/software/anaconda3/bin`为实际安装目录，然后运行`source  .bashrc`

2、conda常用的命令

    1）`conda list` 查看安装了哪些包

    2）`conda env list` 或 `conda info -e` 查看当前存在哪些虚拟环境

    3）`conda update conda` 检查更新当前conda
 
    4）`source activate your_name` 激活环境

    5）`source deactivate your_name` 退出环境

3、创建python虚拟环境

     使用 `conda create -n your_env_name python=X.X`（2.7、3.6等)命令创建python版本为X.X、名字为`your_env_name`的虚拟环境

4、使用激活(或切换不同python版本)的虚拟环境

    打开命令行输入`python --version`可以检查当前python的版本

    使用如下命令激活虚拟环境(即将python的版本改变)

    `Linux:  source activate your_env_name(虚拟环境名称)`

    `Windows: activate your_env_name(虚拟环境名称)`

5、对虚拟环境中安装额外的包

    使用命令`conda install -n your_env_name [package]`即可安装`package`到`your_env_name`中

6、关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)

   使用如下命令:

   `Linux: source deactivate`

   `Windows: deactivate`

7、删除虚拟环境

   使用命令`conda remove -n your_env_name(虚拟环境名称) --all`， 即可删除

8、删除环境中的某个包

   使用命令`conda remove --name your_env_name  package_name` 即可

