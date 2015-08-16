# Maintainer: Anntoin Wilkinson <anntoin gmail com>
# Contributor: Nick B <Shirakawasuna at gmail _dot_ com>

pkgname=gunroar
pkgver=0.15
pkgrel=9
pkgdesc="An addictive game by Kenta Cho.  Navigate your abstract battleship and destroy enemies!"
arch=('i686' 'x86_64')
url="http://www.asahi-net.or.jp/~cs8k-cyu/windows/gr_e.html"
license=('custom')
depends=('glu' 'sdl_mixer') 
makedepends=('gdc1')
source=('http://abagames.sakura.ne.jp/windows/gr0_15.zip'
		'http://ftp.de.debian.org/debian/pool/main/g/gunroar/gunroar_0.15.dfsg1-5.debian.tar.gz')
md5sums=('a7ba4b75ff9208131d391f3a5243b5cf'
         '83162972b7b9cf0d4634c8ef4bb92bdc')

prepare() {
  cd $srcdir/gr

  _patchdir='../debian/patches'
  cat $_patchdir/series | egrep -v '^#|^\ #' | sed "s:^:$_patchdir/:" | xargs -n1 patch -p1 -i

  sed -i 's:\/games::' ./src/abagames/util/sdl/{sound,texture}.d
  sed -i 's:\/games:\/bin:' ../debian/$pkgname.desktop
  sed -i 's:gdmd-v1:gdmd1:' Makefile
  sed -i 's:gdc-v1:gdc1:' Makefile
}

build() {
  cd $srcdir/gr
  make
}

package() {
  cd $srcdir/gr

  # Install binary
  install -D -m755 $pkgname $pkgdir/usr/bin/$pkgname

  # Install other resources
  find {images,sounds} -type f -exec install -Dm644 {} $pkgdir/usr/share/$pkgname/{} \;

  # Install man page and debian copyright license
  install -D -m644 ../debian/$pkgname.6 $pkgdir/usr/share/man/man6/$pkgname.6
  install -D -m644 ../debian/copyright $pkgdir/usr/share/licenses/$pkgname/copyright

  # Install desktop file and icon
  install -D -m644 ../debian/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop
  install -D -m644 ../debian/$pkgname.xpm $pkgdir/usr/share/pixmaps/$pkgname.xpm
}
# vim:set ts=2 sw=2 et:
