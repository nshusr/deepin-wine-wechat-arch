在Archlinux及衍生发行版上运行微信 (WeChat)
=======

**本分支：采用 `deepin-wine5` 而非原版 `wine`；以下徽章来自母分支，小心混淆**

<p align="center">
  <a href="https://travis-ci.org/countstarlight/deepin-wine-wechat-arch">
    <img src="https://travis-ci.org/countstarlight/deepin-wine-wechat-arch.svg?branch=master" alt="Build Status">
  </a>
  <a href="https://pc.weixin.qq.com/">
    <img src="https://img.shields.io/badge/WeChat-2.9.5.56-blue.svg" alt="WeChat Version">
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

Deepin 打包的微信 (WeChat) 容器移植到 Archlinux，**本分支依赖 `deepin-wine`**，包含定制的注册表配置，微信安装包替换为官方最新。

<!-- TOC -->

- [安装](#安装)
- [兼容性记录](#兼容性记录)
- [常见问题及解决](#常见问题及解决)
- [感谢](#感谢)
- [更新日志](#更新日志)

<!-- /TOC -->

## 安装

`deepin-wine-wechat` 依赖AUR中的 `deepin-wine5`，可从 AUR 或 https://github.com/abcfy2/deepin-wine5-aur 获取。

### 从源码安装

```shell
 git clone https://github.com/bryango/deepin-wine-wechat-arch.git

 cd deepin-wine-wechat-arch
 makepkg -si
```

* 运行应用菜单中创建的WeChat，开始安装

  **注意：安装微信时不需要修改安装路径，如果修改默认路径，要对应修改 `deepin-wine-wechat` 的启动脚本：**

  `/opt/deepinwine/apps/Deepin-WeChat/run.sh`

  ```bash
  env WINEPREFIX="$WINEPREFIX" WINEDEBUG=-msvcrt $WINE_CMD "c:\\Program Files\\Tencent\\WeChat\\WeChat.exe" &
  ```

  改为修改后的安装路径，否则只有安装后第一次能够运行

* 安装完可直接启动

  **注意：登录后请在 `设置` 里关闭微信的 `自动更新`，微信启动时会检查更新并加载自动更新程序，由于默认屏蔽了微信的自动更新程序，会导致找不到更新程序而不能启动**

## 兼容性记录

|   微信    |  wine   | 兼容性 |                             备注                             | deepin-wine | 兼容性 |                             备注                             |
| :-------: | :-----: | :----: | :----------------------------------------------------------: | :---------: | :----: | :----------------------------------------------------------: |
| 2.9.5.56  |  5.13   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |  2.18_24-3  |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |
| 2.9.5.41  |  5.11   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |  2.18_22-3  |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |
| 2.9.0.123 |   5.7   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |  2.18_22-3  |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |
| 2.9.0.114 |   5.6   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |             |        |                                                              |
| 2.9.0.112 |   5.5   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |             |        |                                                              |
| 2.8.0.133 |   5.3   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |             |        |                                                              |
| 2.8.0.112 | 5.0-rc4 |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |             |        |                                                              |
| 2.8.0.106 |  4.19   |  部分  | 发送图片有问题: [#42](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/42) |             |        |                                                              |
| 2.7.1.88  |  4.19+  |  支持  |                                                              |             |        |                                                              |
| 2.7.1.88  |  4.18   |  部分  |                      不能使用中文输入法                      |             |        |                                                              |
| 2.7.1.85  |  4.18   |  部分  |                      不能使用中文输入法                      |  2.18_18-2  |   ?    |                                                              |
| 2.7.1.82  |  4.18   |  部分  |                      不能使用中文输入法                      |  2.18_18-2  | 不支持 |                             闪退                             |
| 2.7.1.82  |  4.17   |  部分  |                      不能使用中文输入法                      |  2.18_18-2  | 不支持 |                             闪退                             |
| 2.6.8.65  |  4.16   |  支持  |                                                              |  2.18_18-2  |  支持  |                                                              |

## 常见问题及解决

### 修复 `deepin-wine` 字体渲染发虚

kde桌面参考：[deepin-wine-wechat-arch#36](https://github.com/countstarlight/deepin-wine-wechat-arch/issues/36)

deepin 桌面：

```bash
yay -S lib32-freetype2-infinality-ultimate
```

**注意：切换到 `deepin-wine` 后，对 `wine` 的修改，如更改dpi，都改为对 `deepin-wine` 的修改**

### 高分辨率屏幕支持

在 `winecfg` 的Graphics选项卡中修改dpi，如 修改为`192`

对于 `deepin-wine`：

```bash
env WINEPREFIX="$HOME/.deepinwine/Deepin-WeChat" deepin-wine winecfg
```

### 使用全局截图快捷键

使用全局截图快捷键和解决Gnome上窗口化问题，参见[issue2](https://github.com/countstarlight/deepin-wine-tim-arch/issues/2).

### 消除阴影边框

微信窗口不在最上方时，在其他窗口上会显示一个阴影边框。

参照[切换到 `deepin-wine`](#切换到-deepin-wine) 解决，或者使用[shadow.exe](shadow.exe)，在微信启动时运行，自动消除这个阴影边框。

> 根据[“用山寨方法解决wine运行微信残留阴影窗口的问题”](https://blog.kangkang.org/index.php/archives/397)，对原程序稍做修改编译出的 [shadow.exe](shadow.exe)，源码文件为 [shadow.cpp](shadow.cpp)

你也可以自行编译这个程序：

```bash
# 安装windows交叉编译工具链
yay -S mingw-w64-gcc

# 编译
i686-w64-mingw32-g++ -municode -m32 -static -s shadow.cpp -o shadow
```

对于 `v2.8.0.133-2` 及之前的版本，不自带这个程序，可以自行将 [shadow.exe](shadow.exe) 放置到 `~/.deepinwine/Deepin-WeChat/drive_c/shadow.exe`

并参照 [run.sh](run.sh) 在 `/opt/deepinwine/apps/Deepin-WeChat/run.sh` 中加入如下几行：

```diff
CallApp()
{
	if [ ! -f "$WINEPREFIX/reinstalled" ]
	then
		touch $WINEPREFIX/reinstalled
-		env WINEDLLOVERRIDES="winemenubuilder.exe=d" WINEPREFIX="$WINEPREFIX" $WINE_CMD $APPDIR/$WECHAT_INSTALLER-$WECHAT_VER.exe
+		env WINEDLLOVERRIDES="winemenubuilder.exe=d" WINEPREFIX="$WINEPREFIX" $WINE_CMD $APPDIR/$WECHAT_INSTALLER-$WECHAT_VER.exe &
	else
        #Support use native file dialog
        export ATTACH_FILE_DIALOG=1

        env WINEPREFIX="$WINEPREFIX" WINEDEBUG=-msvcrt $WINE_CMD "c:\\Program Files\\Tencent\\WeChat\\WeChat.exe" &
	fi
+	# run 'shadow.exe' if process not exist
+	if [[ -z "$(ps -e | grep -o 'shadow.exe')" ]]; then
+		env WINEPREFIX="$WINEPREFIX" WINEDEBUG=-msvcrt $WINE_CMD "c:\\shadow.exe" &
+	fi
}
```

## 感谢

* [Wuhan Deepin Technology Co.,Ltd.](http://www.deepin.org/)

## 更新日志

* 2020-07-20 WeChat-2.9.5.56
* 2020-07-02 WeChat-2.9.5.41
* 2020-05-10 WeChat-2.9.0.123
* 2020-04-24 WeChat-2.9.0.114
* 2020-04-20 WeChat-2.9.0.112
* 2020-03-08 WeChat-2.8.0.133
* 2020-02-10 WeChat-2.8.0.121
* 2020-01-20 WeChat-2.8.0.116
* 2020-01-10 WeChat-2.8.0.112
* 2020-01-04 WeChat-2.8.0.106
* 2019-11-07 WeChat-2.7.1.88
* 2019-10-23 WeChat-2.7.1.85
* 2019-10-19 WeChat-2.7.1.82
* 2019-07-25 WeChat-2.6.8.65
* 2019-06-02 WeChat-2.6.8.52
* 2019-05-29 WeChat-2.6.8.51
* 2019-04-03 WeChat-2.6.7.57
* 2019-01-03 WeChat-2.6.2
