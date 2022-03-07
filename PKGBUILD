# Maintainer: Laurent Carlier <lordheavym@gmail.com>
# Contributor: K. Hampf <khampf@users.sourceforge.net>
# Contributor: Skunnyk <skunnyk@archlinux.fr>

pkgname=playonlinux
pkgver=4.4
pkgrel=1
pkgdesc="GUI for managing Windows programs under linux"
url="https://www.playonlinux.com/"
license=('GPL')
depends=('wine' 'imagemagick' 'xterm' 'python-wxpython-dev' 'cabextract' 'unzip' 'mesa-utils' 'gnupg'
         'icoutils' 'xdg-user-dirs' 'libxmu' 'netcat' 'wget' 'p7zip' 'jq' 'perl' 'python-natsort')
arch=('x86_64')
source=(https://www.playonlinux.com/script_files/PlayOnLinux/${pkgver/.0/}/PlayOnLinux_${pkgver/.0/}.tar.gz
        PlayOnLinuxUrlHandler.desktop)
options=(!strip)
sha256sums=('aaeedec5249df3ffd56cd8b3e3e06ea7117828ffc868eb2653d232c48e488058'
            '304d8e998d271383c44acdf386c4664cd65463d5f7f5e3c1c7563fbd8f71a6a8')

package() {
  cd "$srcdir/$pkgname"

  sed -i "s/libexec/bin/g" Makefile
  sed -i "s/python2/python/g" Makefile

  make PREFIX=/usr
  make DESTDIR="${pkgdir}" install

  install -d "${pkgdir}"/usr/share/playonlinux/lang
  mv -v "${pkgdir}"/usr/share/locale "${pkgdir}"/usr/share/playonlinux/lang/locale
  chmod 755 "${pkgdir}"/usr/share/playonlinux/lang

  install -m755 "${srcdir}"/PlayOnLinuxUrlHandler.desktop "${pkgdir}"/usr/share/applications/PlayOnLinuxUrlHandler.desktop
  install -m755 playonlinux-url_handler "${pkgdir}"/usr/bin/playonlinux-url_handler
  sed -i "s/python /python2 /g" "$pkgdir"/usr/{bin,share/playonlinux}/playonlinux-url_handler

#  sed -i "s/ %F//g" $pkgdir/usr/share/applications/playonlinux.desktop
}
