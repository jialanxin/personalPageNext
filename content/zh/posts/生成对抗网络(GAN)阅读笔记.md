---
author: "Me"
title: "生成对抗网络(GAN)阅读笔记"
date: 2021-11-10T15:22:06+08:00
description: "Generative Adversarial Nets"
draft: false
hideToc: false
enableToc: true
enableTocContent: true
author: Me
authorEmoji: 🤖
tags: 
- 机器学习
- GAN
libraries:
- mathjax
---
真实世界中通常可以由少部分输入参数，通过复杂的函数变换，得出千奇百怪的输出。
GAN的生成器可以去近似拟合这种函数变换的概率分布，而非求出函数本身，从而能够做到由随机的输入参数，得到相似的输出。但GAN并不能由输出，反推输入参数是什么形式。GAN也不能由真实世界确定的输入，得到真实世界相同的输出，GAN只能把握输出的概率分布而已。

GAN的算法是先生成一些假样本$G(z)$，然后混入一些真实的样本$x$，去优化辨别分类器$D$的损失函数$log(D(x))+log(1-D(G(z)))$，使得值上升一些。下一步再生成一些假样本$G(z')$，去优化生成器$G$的损失函数$log(1-D(G(z')))$，使得值下降一些。在训练过程中不能在一步内将辨别器的能力提升的太高或太低，这样都会影响生成器的进化。如何优化对抗和判断对抗收敛是GAN的难点。