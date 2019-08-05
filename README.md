在Archlinux及衍生发行版上运行微信(WeChat)
=======

**本分支：采用 `deepin-wine` 而非原版 `wine`；以下徽章来自母分支，小心混淆**

<p align="center">
  <a href="https://travis-ci.org/countstarlight/deepin-wine-wechat-arch">
    <img src="https://travis-ci.org/countstarlight/deepin-wine-wechat-arch.svg?branch=master" alt="Build Status">
  </a>
  <a href="https://pc.weixin.qq.com/">
    <img src="https://img.shields.io/badge/WeChat-2.6.8.65-blue.svg" alt="WeChat Version">
  </a>
  <a href="https://aur.archlinux.org/packages/deepin-wine-wechat/">
    <img src="https://img.shields.io/aur/version/deepin-wine-wechat.svg" alt="AUR Version">
  </a>
  <a href="https://github.com/countstarlight/deepin-wine-wechat-arch/releases">
    <img src="https://img.shields.io/github/downloads/countstarlight/deepin-wine-wechat-arch/total.svg" alt="GitHub Release">
  </a>
  <a href="https://github.com/countstarlight/deepin-wine-wechat-arch/issues">
    <img src="https://img.shields.io/github/issues/countstarlight/deepin-wine-wechat-arch.svg" alt="GitHub Issues">
  </a>
</p>

Deepin打包的微信(WeChat)容器移植到Archlinux，**本分支依赖`deepin-wine`**，包含定制的注册表配置，微信安装包替换为官方最新

<!-- TOC -->

- [安装](#安装)
    - [从 AUR 安装](#从-aur-安装)
    - [从 GitHub Release 安装](#从-github-release-安装)
    - [从源码安装](#从源码安装)
- [常见问题](#常见问题)
- [感谢](#感谢)
- [更新日志](#更新日志)

<!-- /TOC -->

## 安装

`deepin-wine-wechat`依赖AUR或`archlinuxcn`仓库中的`deepin-wine`，可编辑`/etc/pacman.conf`，加入`archlinuxcn`仓库，例如：

```cong
# Add to the end of `pacman.conf`

[archlinuxcn]
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
```

### 从源码安装

```shell
 # 如想使用本分支，请将链接中的 `.../countstarlight/...` 改为 `.../bryango/...`
 git clone https://github.com/countstarlight/deepin-wine-wechat-arch.git

 cd deepin-wine-wechat-arch
 makepkg -si
```

* 运行应用菜单中创建的WeChat，开始安装
* 安装完可直接启动

## 常见问题

- [ ] 1.不能视频通话
- [ ] 2.不能截图
- [x] 3.在 2k/4k 屏幕下字体和图标都非常小, 参见[issue1](https://github.com/countstarlight/deepin-wine-tim-arch/issues/1)
- [x] 4.使用全局截图快捷键和解决Gnome上窗口化问题，参见[issue2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2)

## 感谢

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)

## 更新日志

* 2019-07-25 WeChat-2.6.8.65
* 2019-06-02 WeChat-2.6.8.52
* 2019-05-29 WeChat-2.6.8.51
* 2019-04-03 WeChat-2.6.7.57
* 2019-01-03 WeChat-2.6.2
