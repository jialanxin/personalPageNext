---
author: "Me"
title: "Docker-compose部署Aria2和Filebrowser"
date: 2019-12-23T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- docker-compose
- docker
- aria2
- Filebrowser
image: images/CuteColorIcons/icons8-utorrent.svg
---
之前用了一个别人的单docker容器的Caddy-AriaNg-Aria2-Filebrowser的镜像（[链接](https://www.moerats.com/archives/750/)）。但是这镜像好久没更新了，外加caddy升级到了caddy2，所以决定拿docker-compose编排自己的服务。

主要由三个容器组成：aria2c，caddy2+AriaNg，filebrowser。aria2c暴露rpc和bt端口，caddy2部署AriaNg前端，filebrowser提供预览和下载服务，aria2c和filebrowser通过数据卷共享文件。

测试过程中遇到一些问题，包括不得不加的depends_on参数，我认为三个容器之间没有显著的前后依赖关系，但是不加就是启动不起来。一开始aria2c下bt没速度，我从原来那个容器里把dht.dat文件取了出来（原来的默认位置在/root/.cache/aria2），放到新容器里面，然后还在前端改了两个参数（[链接](http://www.senra.me/solutions-to-aria2-bt-metalink-download-slowly/)），又开了一个conf里没有但是要用的端口（AriaNg里常用的都有解释），才有的下载速度。

后续还有些工作要做的，但是也可能懒就不弄了。比如把filebrowser反向代理到caddy节省一个端口。还有改一下aria2.conf的参数，还有更新bt-tracker。