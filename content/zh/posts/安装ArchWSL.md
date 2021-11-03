---
author: "Me"
title: "安装ArchWSL"
date: 2020-03-02T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- archlinux
- wsl
image: images/CuteColorIcons/icons8-console-96.png
---
记录一下安装ArchWSL的步骤，基于Windows 10 20H1 版本的WSL2。

1. 激活Windows的相关设置，这部分略过，可以看微软的文档。
2. Github上下载[yuk7/ArchWSL](https://github.com/yuk7/ArchWSL)，完成软件安装。安装包的命名决定了最后实例的命名。
3. 由于后续yay不能用root用户，需要设置好root用户的密码和添加新用户，最后设置默认用户。参见yuk7/ArchWSL的wiki部分。
4. 修改/etc/pacman.d/mirrorlist，随后sudo pacman-key --init和sudo pacman-key --population激活初始key。
5. sudo pacman -Syyu base-devel刷新软件列表，安装base-devel软件包。
6. 安装yay，git clone ，cd ，最后makepkg -sic。
7. yay安装pacvis，可视化依赖关系。
8. yay安装openssh，生成密钥使用ssh-keygen。