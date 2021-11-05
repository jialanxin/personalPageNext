---
author: "Me"
title: "为Caddy2设置HTTPS"
date: 2020-03-06T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- caddy2
image: images/CuteColorIcons/icons8-security-ssl-96.png
---
记录一下为Caddy2设置HTTPS和Cloudflare Origin CA的步骤。

1. 首先在Cloudflare TLS申请Origin CA。下载证书和私钥保存在本地。（一定要注意把私钥和证书写进gitignore文件里，上传到开源库就不好了）
2. 将证书和私钥上传到服务器，修改Caddyfile，加入tls设置项，写入证书和私钥的地址。
3. 开放docker-compose的80和443端口。（一开始把443写成433，导致521错误，sigh~）
4. 将Cloudflare的设置改为严格HTTPS
后续还有一步将HTTP重定向至HTTPS，暂时没找到方法做。吐槽一句，Caddy2的资料还是太少了~