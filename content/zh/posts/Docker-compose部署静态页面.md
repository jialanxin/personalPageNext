---
author: "Me"
title: "Docker-compose部署静态页面"
date: 2019-12-03T00:00:00+08:00
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
- caddy2
image: images/CuteColorIcons/icons8-docker.svg
---
之前这个个人页面是部署在S3上的，后来发现手上还闲置了一台VPS，觉得有带宽不用很浪费，就把文件都移过来了。出乎意料的是美国的VPS访问速度似乎比东京的S3还快那么一点点。

整个过程并不复杂，文件服务器使用的是golang编写的Caddy2，Caddy2还处在实验开发阶段，利用Caddyfile文件可以很简单的配置好服务。

因为想以后和其他服务做集成，所以就给项目拿docker打了个包，写Dockerfile还是不复杂的。启动部署方面，之前是直接用docker build生成镜像，再docker run启动容器的，站点文件和配置文件挂载在容器外面。后来决定使用docker-compose，因为考虑到以后要和其他服务做集成，所以现在就是先把部署文件写好推到GitHub上然后在VPS上拖下来，然后docker-compose up一站式编排部署了。

（之前这里忘记写一点，VPS上先用docker-compose down停掉之前的服务，git pull拖新的下来之后，要docker-compose build重新编译一次镜像，最后以前的镜像也是要手动清理的）

CDN用的是Cloudflare免费的，之前S3部署只用CDN，所以DNS设置的是CNAME形式，现在还要使用Cloudflare的DNS了，所以就回归A形式了。

目前还没有做好的事情包括，HTTPS还没有配置好和能不能用Github Actions来自动完成部署呢？

还在慢慢学习中，以后有新的变化会更新的。