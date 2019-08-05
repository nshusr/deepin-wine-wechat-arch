# Maintainer: CountStarlight <countstarlight@gmail.com>

pkgname=deepin-wine-wechat
pkgver=2.6.8.65
wechat_installer=WeChatSetup
deepinwechatver=2.6.2.31deepin0
pkgrel=1.1
pkgdesc="Tencent WeChat (com.wechat) on Deepin Wine For Archlinux"
arch=("x86_64")
url="https://weixin.qq.com/"
license=('custom')
depends=('p7zip' 'deepin-wine' 'xorg-xwininfo' 'wqy-microhei')
conflicts=('deepin-wechat')
install="deepin-wine-wechat.install"
_mirror="https://mirrors.ustc.edu.cn/deepin"
source=("$_mirror/pool/non-free/d/deepin.com.wechat/deepin.com.wechat_${deepinwechatver}_i386.deb"
  "https://dldir1.qq.com/weixin/Windows/${wechat_installer}.exe"
  "run.sh"
  "reg.patch")
md5sums=('c66a173fe6817afd898e0061d9eaf42e'
  '55704ea3ffe49ca189a0c1ade1e4d350'
  'f0fa8651097bc5a311d35dfe23707d59'
  '9c9d51ff585ff630473ce827159a8230')
PKGEXT='.pkg.tar'  # do NOT compress package to save time

build() {
  msg "Extracting DPKG package ..."
  mkdir -p "${srcdir}/dpkgdir"
  tar -xvf data.tar.xz -C "${srcdir}/dpkgdir"
  desktop_file="${srcdir}/dpkgdir/usr/share/applications/deepin.com.wechat.desktop"
  sed "s/\(Categories.*$\)/\1Network;/" -i "${desktop_file}"
  sed "s/\(StartupWMClass\).*$/\1=wechat/" -i "${desktop_file}"  # for themed icons
  cat <<- 'EOF' >> "${desktop_file}"
	Actions=Reinstall;
	
	[Desktop Action Reinstall]
	Exec=sh -c "rm -f ~/.deepinwine/Deepin-WeChat/reinstalled; exec /opt/deepinwine/apps/Deepin-WeChat/run.sh"
	Name=Reinstall WeChat
EOF
  msg "Extracting Deepin Wine WeChat archive ..."
  7z x -aoa "${srcdir}/dpkgdir/opt/deepinwine/apps/Deepin-WeChat/files.7z" -o"${srcdir}/deepinwechatdir"
  msg "Removing original outdated WeChat directory ..."
  rm -r "${srcdir}/deepinwechatdir/drive_c/Program Files/Tencent/WeChat"
  msg "Patching reg files ..."
  patch -p1 -d "${srcdir}/deepinwechatdir/" < "${srcdir}/reg.patch"
  msg "Creating font file link ..."
  ln -sf "/usr/share/fonts/wenquanyi/wqy-microhei/wqy-microhei.ttc" "${srcdir}/deepinwechatdir/drive_c/windows/Fonts/wqy-microhei.ttc"
  msg "Repackaging app archive ..."
  7z a -t7z -r "${srcdir}/files.7z" "${srcdir}/deepinwechatdir/*"
}

package() {
  msg "Preparing icons ..."
  install -d "${pkgdir}/usr/share"
  cp -a ${srcdir}/dpkgdir/usr/share/* "${pkgdir}/usr/share/"
  msg "Copying WeChat to /opt/deepinwine/apps/Deepin-WeChat ..."
  install -d "${pkgdir}/opt/deepinwine/apps/Deepin-WeChat"
  install -m644 "${srcdir}/files.7z" "${pkgdir}/opt/deepinwine/apps/Deepin-WeChat/"
  install -m755 "${srcdir}/run.sh" "${pkgdir}/opt/deepinwine/apps/Deepin-WeChat/"
  install -m644 "${srcdir}/${wechat_installer}.exe" "${pkgdir}/opt/deepinwine/apps/Deepin-WeChat/"
}
