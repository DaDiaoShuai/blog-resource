---
title: VScode插件--Remote-Vscode的配置及使用教程
date: 2019-05-29
tags: tools
category: 工具
description: 直接管理远程服务器文件的神器!
---
> 当前系统使用的是macOS

### 安装
1. 在vscode的插件管理器里搜索`remote vscode`，然后install安装即可。
2. 在远程服务器上安装`rmate`
``` sh
wget -O /usr/local/bin/rmate https://raw.github.com/aurora/rmate/master/rmate && chmod a+x /usr/local/bin/rmate
```

### 配置

1. `F1`或者`cmd+shift+p`，调出命令窗口输入`user setting`
2. 在设置页面最上方的搜索框里输入`remote vscode`，勾选默认配置。

### 使用
1. 在本地vscode，调出命令窗口，输入`Remote Start Server`, 回车。
2. 在本地终端输入，`ssh -R 52698:127.0.0.1:52698 root@your.remote`
3. 在远程终端, `rmate -p 52698 PATH/TO/YOUR/FILE`，然后就能在你本地的vscode中出现你要编辑的文件啦，并且实时同步到远程服务器上。

是不是很得劲儿呢~