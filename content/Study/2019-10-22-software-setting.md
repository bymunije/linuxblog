---
title: Software Setting
author: Bymunije
date: '2019-10-22'
slug: software-setting
categories:
  - Study
tags:
  - R
  - Python
  - Linux
  - Github
description: ''
featured: ''
featuredalt: ''
featuredpath: ''
linktitle: ''
type: post
---
# Sublime Text3

## 1. Tab自动转换为空格

- 打开`Preferences -> Settings - User`
- 添加代码如下：
```
"tab_size": 4,
"translate_tabs_to_spaces": true
```

## 2. 个性化设置
```
{
	"color_scheme": "Packages/Predawn/predawn.tmTheme",
	"font_face": "Microsoft Yahei Mono",
	"font_size": 11,
	"highlight_line": true,
	"highlight_modified_tabs": true,
	"ignored_packages":
	[
	],
	"line_padding_top": 3,
	"show_encoding": true,
	"show_line_endings": true,
	"theme": "predawn-DEV.sublime-theme",
	"word_wrap": true,
	"tab_size": 4,
	"translate_tabs_to_spaces": true
}
```

# Visual Studio Code

## 1.配置远端服务器

1.[官网](https://code.visualstudio.com/)下载安装。安装后默认为英文界面，可在扩展按钮搜索`Chinese`，选择第一个`Chinese (Simplified) Language Pack for Visual Studio Code`，重启后软件即可变成中文
2.在扩展按钮搜索`Remote Development`,可自动安装`Remote-SSH`、`Remote-Containers`、`Remote-WSL`等依赖插件
3.连接远程服务器使用的是`Remote-SSH`，连接时本地需要SSH客户端，比如`OpenSSH`。
4.在左侧点击`Remote-SSH`图标，然后在`SSH TARGETS`处点击设置，在弹出的窗口中选择配置文件的地址，一般选择第一个`C:\Users\zhang\.ssh\config`编辑并保存文件，其中
- `Host`：填服务器名称
- `HostName`:连接的远程服务器的IP
- `User`:登录远程服务器的用户名
5.左边会出现上一步设置的服务器名称，点击选择`Connect to Host in Current Window` 即可开始连接,若左下角出现绿色的`SSH: <Host>`的标识，即表示已成功连接到了远程主机

## 2.配置SSH密钥登录

1. 本地打开`cmd`或`git bash`，输入`ssh-keygen`后一路回车，会在用户目录下的`.ssh` 文件夹内生成`id_rsa`和`id_rsa.pub`两个文件，分别对应为私钥和公钥
2. 将`id_rsa.pub`文件中的内容复制到远程主机用户目录下`.ssh`文件夹内名为 `authorized_keys`的文件中
3.在左下角的设置的扩展中选择`Remote-SSH`，然后勾选`Remote.SSH:Show Login Terminal`
