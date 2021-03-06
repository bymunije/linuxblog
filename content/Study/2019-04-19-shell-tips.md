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
***
# <font size=6>commond</font>
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
- 注意文件保存格式在linux和window的区别

### 2. Note
- BEGIN:从第一行开始
- FS:输入字段分隔符，默认空格
- OFS:输出字段分隔符，默认空格
- ||/&&: 或/与

```
cat file.txt | awk 'BEGIN {FS="\t";OFS="\t"} {if ($20 == "%" || $20 == "%%") {$23 = $14; print $0} else if ($20 != "%" && $20 != "%%") {$23 = $22; print $0}}' > file2.txt
```

### 3.保留第一行的标题

- 可`NR==1`实现

`cat file.csv | awk -F, 'NR==1;{if($9<=-5)print$0}'> select_file.csv`

### 4.文件中添加一列一样的字符串

`awk '$0=$0"\t20191027"' file.txt`

### 5.`sort`排序时排除第一行

`awk 'NR==1{print $0;next}{print $0 | "sort -u"}'`

如果写完整应该是：

`awk '{if(NR==1) {print $0;next}} {print $0 | "sort -u"}'`

### 6.调整`txt`文件中列的顺序

`awk '{print $2,$3,$1,$4}' OF=, OFS=, 6G.txt`

***
## <font color=orange size=6>Vim</font>

### common command

- `set list`:查看分隔符
- `ctrl+v+i`: vim中输入tab
- `shift+mouse`:vim中复制

***
## <font color=orange size=6>ps</font>
### 1.查看用户所有进程
```
ps -aux | grep byzhang
```

***

***
## <font color=orange size=6>grep</font>

- `grep -w`: 精确匹配
- `grep -v`:反向选择
- `grep -i`:忽略大小写

***

## <font color=orange size=6>du</font>
### 1.查看占用磁盘大小
```
du -sh
```
***
## <font color=orange size=6>ln</font>

### **1. ln** : link files,为某一文件在另一个位置建立同步链接，包括硬链接（hard link）和 软链接（symbolic link），两种方式都不会将原本的档案复制一份，而是只占用极少的磁盘空间。

- **hard link**   
   
   + 代表一个档案可以有多个名称
   + 以文件副本的形式存在，但不占用实际空间
   + 无法对目录创建
   + 只能在同一个文件系统中创建

- **symbolic link**
   
   + 产生一个特殊的档案，档案的内容是指向另一个档案的位置
   + 以路径的形式存在，类似于windows的快捷方式
   + 可以对目录创建
   + 可以跨越不同的文件系统
   + 可以对不存在的文件名进行链接

### **2. 命令参数**



***
## <font color=orange size=6>Common Command</font>
### 1.查看文件夹下文件和目录数目

文件： `ls -l | grep '^-' | wc -l`
目录： `ls -l | grep '^d' | wc -l`

### 2.`ctrl-z`、`ctrl-c`和`ctrl-d`的区别

- `ctrl-z`：(suspend foreground process) 发送信号给前台进程组中的所有进程，常用于挂起一个进程，并没有结束进程，可以使用`fg`(前台)/`bg`(后台)恢复执行，对于`fg`恢复被挂起的进程可以使用`ctrl-z`再次挂起，而`bg`命令无法再次挂起

- `ctrl-c`：(kill foreground process) 发送信号给前台进程组中的所有进程，强制终止程序的执行

- `ctrl-d`：(terminate input,exit shell) 一个特殊的二进制值，表示EOF,作用相当于在终端输入`exit`后回车

### 3.`Vim`文件格式转换

Windows文件格式为`dos`，Linux文件格式为`unix`

- 查看文件格式：
命令行模式输入：`set ff`，显示`fileformat=dos`

- 转换文件格式：
1.dos_to_unix: `set ff=unix`
2.unix_to_dos: `set ff=dos`

- 替换文件中`^M`符号：
`tr -d '\r'`

- 中文乱码：
临时方法：打开`vim`,输入`set encoding=utf-8`
一次性方法：在`.vimrc`文件中添加`set encoding=utf-8`

### 4.内容提取

`basename`: 从文件名中去除目录和后缀

- `basename kernel/include/linux/stddef.h`得到`stddef.h`
- `basename kernel/include/linux/stddef.h .h`得到`stddef`
- `basename kernel/include/linux/stddef.h h`得到`stddef.`
- `basename kernel/include/linux/`或`bsename kernel/include/linux`得到`linux`

### 5.`shell`脚本执行显示错误`bad substitution`

这与`shell`使用的是`/bin/sh`，还是`/bin/bash`有关系


---
# <font size=6>代码</font>
---
## 1.add header
```
#!/bin/bash
for file in /home/usrname/data/Drug_combination/header/*.txt
do
	file_name_txt=`basename $file`
	file_name=${file_name_txt%.*}
	add_header=${file_name}_header.txt
	echo $add_header
	head -n 1 ${file} > ./header/add_header/${add_header}
done


cd /home/usrname/data/Drug_combination/header/add_header
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


