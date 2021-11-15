---
author: "Me"
title: "创建一个AUR包"
date: 2020-04-13T00:00:00+08:00
description: ""
draft: false
hideToc: false
enableToc: false
enableTocContent: false
author: Me
authorEmoji: 🤖
tags: 
- archlinux
---
Archlinux的一大特色就是各种各样的aur包，安装和卸载都比较方便。今天找命令行下有什么好翻译工具的时候找到了[AFC163/fanyi](https://github.com/afc163/fanyi)这个项目，而且也没有人在aur里打过包，所以我来试一次打包了。
```bash
# Maintainer: lstnbl <******@****.**>
_npmname=fanyi
pkgname=node-$_npmname
pkgver=4.2.0
pkgrel=1
pkgdesc="A CN and US translate tool in your command line."
arch=('any')
url="https://github.com/afc163/fanyi"
license=('MIT')
depends=('nodejs' 'festival')
makedepends=('npm')
source=(https://github.com/afc163/$_npmname/archive/v$pkgver.tar.gz)
noextract=("v$pkgver.tar.gz")
sha256sums=('SKIP')
package() {
    npm install \
        --user root --global \
        --prefix "$pkgdir/usr" \
        "$srcdir"/v$pkgver.tar.gz
    find "$pkgdir/usr" -type d -exec chmod 755 '{}' +
    install -Dm0644 "$pkgdir/usr/lib/node_modules/$_npmname/LICENSE" \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
```
整个PKGBUILD文件如图，前几行申明一些名称和版本信息。 depends和 makedepends是运行和构建时的依赖。 source为代码源，默认是curl下载，也可以指明git下载。 noextract不会自动解压压缩包。 hash和由于作者没有提供，只能跳过。 package()函数表示打包阶段，第一步，npm安装所有的依赖到fakeroot下的 usr/bin和 usr/lib；第二步给权限，暂时还看不懂；第三步安装协议到fakeroot下。makepkg -s执行打包命令并安装好所有依赖，yay -U 包名安装到系统。

然后是上传到aur仓库。详细过程见[AUR纯萌新向教学（3）——提交软件包到AUR](https://blog.yoitsu.moe/arch-linux/aur_sumbiting_guidebook.html)
