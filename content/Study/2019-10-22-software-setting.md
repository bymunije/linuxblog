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

1. [官网](https://code.visualstudio.com/)下载安装。安装后默认为英文界面，可在扩展按钮搜索`Chinese`，选择第一个`Chinese (Simplified) Language Pack for Visual Studio Code`，重启后软件即可变成中文
2. 在扩展按钮搜索`Remote Development`,可自动安装`Remote-SSH`、`Remote-Containers`、`Remote-WSL`等依赖插件
3. 连接远程服务器使用的是`Remote-SSH`，连接时本地需要SSH客户端，比如`OpenSSH`
4. 在左侧点击`Remote-SSH`图标，然后在`SSH TARGETS`处点击设置，在弹出的窗口中选择配置文件的地址，一般选择第一个`C:\Users\zhang\.ssh\config`编辑并保存文件，其中
- `Host`：填服务器名称
- `HostName`:连接的远程服务器的IP
- `User`:登录远程服务器的用户名
5. 左边会出现上一步设置的服务器名称，点击选择`Connect to Host in Current Window` 即可开始连接,若左下角出现绿色的`SSH: <Host>`的标识，即表示已成功连接到了远程主机

## 2.配置SSH密钥登录
   
1. 本地打开`cmd`或`git bash`，输入`ssh-keygen`后一路回车，会在用户目录下的`.ssh` 文件夹内生成`id_rsa`和`id_rsa.pub`两个文件，分别对应为私钥和公钥
2. 将`id_rsa.pub`文件中的内容复制到远程主机用户目录下`.ssh`文件夹内名为 `authorized_keys`的文件中
3. 在左下角的设置中选择扩展，然后选择`Remote-SSH`,然后勾选`Remote.SSH:Show Login Terminal`即可

## 3.推荐的插件

1). `Chinese (Simplified) Language Pack for Visual Studio Code`: 界面语言为中文
2). `Remote Development(Remote SSH)`: 连接远端服务器
3). `Sublime Text Keymap and Settings Importer`： sublime快捷键
4). `Python for VSCode`： 运行python
5). `Beautiful`: 格式化代码的工具
6). `Path Intellisense`: 自动路径补全,默认不带这个功能
7). `Vscode-icons 让vscode`: 资源目录加上图标、必备
8). `Auto-Open Markdown Preview markdown`: 文件自动开启预览
9). `Setting Sync`: 在不同电脑同步你的配置和插件
10). `VS Code SFTP`: 直接编辑远端linux文件,具体配置可参考[这里](https://www.jianshu.com/p/0724921285d4)

## 4.`VS Code SFTP`本地文件同步服务器

快捷键`Ctrl+shift+P`打开指令窗口，输入`sftp:config`回车，会在当前工程的`.vscode`文件夹下生成`sftp.json`文件，其中需要修改`name、host、port、username、password、remotePath`
- `name`：服务器名称，自定义
- `host`：服务器IP
- `port`：服务器端口
- `username`：用户名
- `password`：密码
- `remotePath`：服务器目录
本地文件修改之后保存，即可同步到服务器

# Dokan + SSHFS(WinSSHFS)文件系统

1. [Dokan](https://github.com/dokan-dev/dokany/releases)是用户态的文件系统驱动，可称之为`fuse for windows`,可以用来开发虚拟磁盘，即在 “我的电脑” 中虚拟出一个硬盘，也可以是可移动磁盘或者网络硬盘

2. SSHFS是基于`FUSE`构建的`SSH` 文件系统客户端程序，通过它远程主机的配置无需作任何改变，即可透过`SSH` 协议来挂载远程文件系统

3. 配置[WinSSHFS](https://github.com/feo-cz/win-sshfs/releases)可参考下图.点击`Add`，输入要链接的服务器的名称、IP地址、端口、用户名、密码等信息，选择好要挂载的目录，点击`save`和`mount`

- `Drive Name`: 服务器名称（自定义）
- `Host`: 服务器IP地址
- `Port`: 端口
- `Username`: 用户名
- `Password`: 密码

<img src="/Study/2019-10-22-software-setting_files/WinSSHFS.jpg" alt="WinSSHFS" width="400px" height="200px"/>

4. 当出现`could not connect Version error`错误时，`Dakan`版本需为`1.2.0.1000`




