---
author: "Me"
title: "用Github actions发布博客之踩坑"
date: 2020-04-07T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- Github actions
image: images/CuteColorIcons/icons8-github.svg
---
想用github actions的缘由是，一直以来，博客的编写和部署是分在两个仓库里进行的，中间涉及到编译出的站点文件的拷贝工作。每次都会变化的js文件把部署仓库的git撑的好大。采用github actions之后就只需要把代码推送上去，就直接得到最后的docker镜像了。

怎么操作没什么好说的，看官方文档，还有大量的示例可以用。只把我遇到的一些坑记录一下。

首先是 nuxt generate得到了 dist文件夹，在使用 actions/upload-artifact之后得到的是一个zip压缩包，在接下来的步骤中使用 actions/download-artifact时会自动解包成文件夹。我以为下载时还是压缩包，还用了unzip，结果目录下没有这个压缩包

第二个坑是我忘记了docker image的名字必须是小写字母

第三个坑是我不太会用 DockerPublish这个action，显示登陆不到dockerhub，后来是用命令里的 docker login -u username -p password才上传到dockerhub的。username和password要提前在serect里写好，才不会在脚本里显示出来

第四个坑是因为调试，访问了网站太多遍，导致cloudflare缓存了一部分过期的html和js，导致加载js的时候404，html是缓存的，js却命中了主机，当然是找不到文件的。

在使用github actions之后，一部分的配置命令从 Dockerfile转移到了 action.yml里，例如下载caddy之类的，镜像编写变得简单了。部署的时候不是每一次都要重新build了，直接pull新镜像就可以了。当然了https的证书是挂在镜像外面的。