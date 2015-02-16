# Maintainer: Voobscout <voobscout+aur@gmail.com>
pkgname=xorg-xfstt
pkgver=1.9.1
pkgrel=1
pkgdesc="X Font Server TrueType"
arch=('i686' 'x86_64')
license=('GPL2')
makedepends=('git' 'pkg-config' 'autoconf' 'automake' 'gettext')
url="http://www.hadrons.org/software/xfstt"
provides=('xorg-xfstt')
optdepends=('xorg-server')
source=('git://git.hadrons.org/git/xfstt.git'
        'xfstt.service'
       )
sha256sums=('SKIP'
            '9e829e03e2ca6b1bb552dbbf3f361579474f7a5e013f03de8213e4148a58f07f'
           )

pkgver() {
	cd ${srcdir}/${pkgname%%-*}
	git describe --always | sed 's/-/./g'
}

install=xfstt.install
options=(!strip)

build() {

  cd ${srcdir}/xfstt

  msg "Preparing XFSTT sources..."
  autoreconf -Wall -f -i

  msg "Configuring XFSTT..."
  ./configure --prefix=/usr

  msg "Compiling XFSTT... "
  make

}

package() {
  msg "Installing XFSTT"
  cd ${srcdir}/xfstt
  make DESTDIR=${pkgdir} install

  msg2 "Installing systemd xfstt unit"
  install -Dm 0644 ${srcdir}/xfstt.service ${pkgdir}/usr/lib/systemd/system/xfstt.service
}
# vim:set ts=2 sw=2 et:
