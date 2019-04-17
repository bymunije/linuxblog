---
title: Blogdown+Hugo+Github+Netlify构建blog
author: Bymunije
date: '2019-04-17'
slug: blogdown-hugo-github-netlify构建blog
categories:
  - Study
tags:
  - R
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
# 软件准备

- 安装R(https://www.r-project.org/)
- 安装rstudio(https://www.rstudio.com/)
- 安装git(https://git-scm.com/)

# Rstudio配置

安装好上述软件后，需要对Rstudio进行简单的配置：

- ```Tools -> Global Options -> Sweave -> Weave Rnw files using:knitr```
- ```Tools -> Global Options -> Sweave -> Typeset LaTex into PDF using:XeLaTeX```,这两个是生成PDF文件用的，中文用户最好选择XeLaTeX

- ```Tools -> Global Options -> Git/SVN -> Git executable```

# 安装blogdown和hugo

## 安装blogdown：

```
install.packages('blogdown')
```

## 安装hugo：

```
blogdown::install_hugo()
```
如果报错，可以直接安装开发版：
```
install.packages("devtools")
devtools::install_github("rstudio/blogdown")
```
如果还是报错，就手动下载安装：
```
blogdown:::install_hugo_bin("d:/hugo.exe")
```
# Github新建一个仓库
<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/2.PNG" alt="" width="400px" height="300px"/>

# blogdown建站

## 1.创建项目

回到Rstudio，```File -> New Project -> Version Control -> Git```，然后填写```Repository URL```,```Project directory name```会自动生成，选择一个合适的文件夹存放，点击```Create Project```创建项目

### 设置gitignore

打Rstudio右下角的```Files```标签，点击```.gitignore```文件，因为有些文件不需要啊上传到github, 比如public，是hugo渲染后的网页， 本地预览即可，因为在Netlify部署的时候会重新渲染
```
.Rproj.user
.Rhistory
.RData
.Ruserdata
blogdown
.DS_Store
public/
```
## 2.初始化blogdown

打开```Rstudio,File -> New Project -> New Directory -> Website using blogdown```，因为已经安装了hugo，所以去掉hugo选项,主题可以修改，点击```Create Project```创建项目

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/1.png" alt="" width="400px" height="300px"/>

## 3.本地项目同步到github仓库
```
cd <本地项目目录>
git init
git add .
git commit -m "first comment"
git remote add origin https://github.com/<github帐号>/<仓库名称>
git remote -v
git pull origin master --allow-unrelated-histories
git push -u origin master
```

## 4.本地运行网站

点击Rstudio菜单```Help```下面的```Addins->Serve Site```，可能会提示安装几个包例如shiny、miniUI等，点击yes安装ok,，其实点击这个跟在console里面输入```blogdown::serve_site()```是一样的：

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/3.png" alt="" width="400px" height="300px"/>

# 设置Netlify

## 1.注册Netlify

打开Netlify(https://app.netlify.com/signup)      主页,直接在 ```Sign up with one of the following```下面选择GitHub

## 2.绑定Github

登录Netlify后，点击导航栏```Sites```，再点击右上角```New site from Git```，再点击Github进行下列操作：

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/4.png" alt="" width="400px" height="300px"/>

点击```deploy site```生成网站

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/5.png" alt="" width="400px" height="300px"/>

# 更新博客内容
打开Rstudio，```Rstudio,File -> New Project -> exist Directory -> blogdown dictionary```，点击右上角Git标签，点击commit，选择更新内容，填写```commit message```点击```commit -> push```

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/7.jpeg" alt="" width="400px" height="300px"/>

# Quenstion:
#### 1.git在github远程创建仓库后, 利用gitbash进行提交本地文件的时候出现如下错误：

<img src="/post/2019-04-17-blogdown-hugo-github-netlify构建blog_files/8.png" alt="" width="700px" height="250px"/>

解决办法1:

```
1: 进行push前先将远程仓库pull到本地仓库
$ git pull origin master    #git pull --rebase origin master
$ git push -u origin master

2: 强制push本地仓库到远程 (这种情况不会进行merge, 强制push后远程文件可能会丢失 不建议使用此方法)
$ git push -u origin master -f

3: 避开解决冲突, 将本地文件暂时提交到远程新建的分支中
$ git branch [name]
# 创建完branch后, 再进行push
$ git push -u origin [name] 
```
解决办法2:
```
git pull --rebase origin master 
git push -u origin master
```
解决办法3:
```
git fetch origin master:tmp
git rebase tmp
git push origin HEAD:master
git branch -D tmp
```
#### 2.Rstudio push 每次需要输入用户名和密码

解决办法：

1.git bash进入你的项目目录，输入```git config --global credential.helper store```,然后会在本地生成一个文本，记录账号和密码

2.使用上述的命令配置好之后，再操作一次git pull，它会提示你输入账号密码，之后就不需要再次输入密码

#### 3. 设置Git

(1).设置用户名和email。

```
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"
```
Home目录下会新建一个.gitconfig文件

(2).GitHub账号添加SSH Keys

以公钥认证方式访问SSH协议的Git服务器时无需输入口令，而且更安全。（访问HTTP协议的Git服务器时，比如提交修改，每次都需要输入口令）

- 创建SSH key

```ssh-keygen -t rsa -C "youremail@163.com"```
系统会提示key的保存位置（一般是~/.ssh目录）和指定口令，保持默认，连续三次回车即可。

- Copy SSH Key

用vim打开文件```id_rsa.pub```文件内的内容，粘帖到github帐号管理的添加SSH key界面中

```vim ~/.ssh/id_rsa.pub```
- 添加到GitHub

登录github-> Accounting settings图标-> SSH key-> Add SSH key-> 填写SSH key的名称，然后将拷贝的```~/.ssh/id_rsa.pub```文件内容粘帖-> add key”按钮添加。

- 测试

ssh -T git@github.com