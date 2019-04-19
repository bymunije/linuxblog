---
title: Github push
author: Bymunije
date: '2019-04-19'
slug: github-push
categories:
  - Study
tags:
  - Github
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
## 上传本地文件到GitHub
### 第一步：建立git仓库
1)cd到你的本地项目根目录下(或者cd加空格再把项目的文件夹直接拖进终端里,然后回车)

(2)执行git的初始化命令

```
git init
```
### 第二步：将项目的所有文件添加到仓库中

```
git add filename
```
### 第三步：将add的文件commit到仓库

```
git commit -m "创建仓库"
```
### 第四步：在github上创建Repository,拿到仓库的https地址

### 第五步：将本地的仓库关联到github上

```
git remote add origin https://github.com/china-dywade/wade.git…
```
后面的https链接地址即第四步的仓库url地址，如果不报错,进行下一步

如果提示出错信息

```
fatal: remote origin already exists.
```


1、先输入`git remote rm origin`
2、再输入`git remote add origin https://github.com/china-dywade/wade.git`
就不会报错了
3、如果输入`git remote rm origin`还是报错`error: Could not remove config section 'remote.origin'`. 我们需要修改gitconfig文件的内容

4、找到github的安装路径

5、找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！
### 第六步：上传github之前，先pull
执行如下命令：`git pull origin master`,如果不报错,进行下一步就好

- 如果是新建的项目，pull的时候报错`fatal: Couldn't find remote ref master`，是这个项目还没有文件，直接把本地修改的上传就可以了，不需要pull

- 如果出现报错 `fatal: Couldn't find remote ref master`或者`fatal: 'origin' does not appear to be a git repository`以及`fatal: Could not read from remote repository`请重新执行 `git remote add origin https://github.com/china-dywade/wade.git`直到不报错为止。

### 第七步，上传代码到github远程仓库

`git push -u origin master`执行完后，如果没有异常，等待执行完就上传成功了，中间可能会让你输入Username和Password，输入github的账号和密码就行了
