---
title: tar压缩解压文件
date: 2019-05-21
tags: Linux
category: 工具
description: 压缩解压文件工具`tar`的一些参数详解
---

#### tar

-x：解压

-t：查看内容

-u：更新原压缩包里的文件

-c：建立压缩档案

-r：向压缩文件末位追加文件

> 以上五个命令参数都是独立的，压缩解压必定要用到其中一个，可以和别的参数连用但只能用其中一个。

-z：有gzip属性的

-Z：有compress属性的

-j：有bz2属性的

-O：将文件解压到标准输出

-v：显示所有过程细节

> 以上几个命令参数是根据需要压缩解压可选的

**-f**参数是必须的：是用档案名字，这个参数一般是最后一个参数，后面只能跟档案名

**压缩**

tar -cf packmd.tar *.md

此命令将所有md文件达成一个名为packmd.tar的包,-c产生新包，-f指定包名。



tar -uf packmd.tar readme.md

此命令为更新packmd包里原有的readme.md文件 ，-u为更新操作



tar -tf packmd.tar

此命令将列出packmd.tar包中所有文件，-t 列出文件



tar -rf packmd.tar push.md

此命令将把push.md文件追加到packmd.tar包里面, -r添加文件



tar -xf packmd.tar

此命令是解开packmd.tar包中所有文件，-x 解压



tar -czvf pack.tar.gz dir  将dir文件夹打包成pack.tar后，用gzip压缩，生成一个gzip压缩过的包 并显示整个打包压缩过程

tar -cjvf pack.tar.bz2 dir 将dir文件夹打包成pack.tar后，用bz2压缩，生成一个bz2压缩过的包 并显示整个打包压缩过程

tar -cZvf pack.tar.Z dir 将dir文件夹打包成pack.tar后，用compress压缩，生成一个uncompress压缩过的包 并显示整个打包压缩过程



**解压**

tar -xvf pack.tar 解压tar包

tar -xzvf pack.tar.gz 解压tar.gz

tar -xjvf pack.tar.bz2 解压tar.bz2

tar -xZvf pack.tar.Z 解压tar.Z

tar -xzvf pack.tar.gz -C /etc/nginx   压缩到指定目录 -C指定目录

**其他压缩工具**

安装rar

rar a pack.rar *.md. rar格式压缩

rar e pack.rar. 解压rar



安装zip

zip md.zip *.md. zip格式压缩

unzip md.zip. 解压zip

