---
author: "Me"
title: "创建Rss订阅"
date: 2020-04-08T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- Rss
- js
image: images/CuteColorIcons/icons8-rss-96.png
---
写心得嘛，不搞点Rss，能让阅读器收到更新，就总觉得差了点什么，比不上别人用Wordpress和typecho的，现在终于会搞了！

主要使用的是nuxt社区的插件@nuxtjs/feed。过程不复杂，跟着指引写就完事了。过程中还遇到了插件里的bug，官方示例里的一个是不能用的，还是看issue才发现有同道中人。

最后就是在布局左上角加一个rss按钮，这时候要注意，xml页面不再受vue-router管理，不能用nuxt的to属性，需要回归到原始的href属性。